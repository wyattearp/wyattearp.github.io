---
layout: post
title: "MCPlacebo: Does Ghidra MCP Actually Make an Agent Better at RE?"
description: "Testing whether handing an LLM agent a Ghidra MCP server beats just giving it a shell and letting it use gdb/radare2/binutils like a person would"
category: 
tags: [technology, ghidra, reverse-engineering, llm, mcp]
---

A curious thing happened a while ago, the full details of which I can't get into for one reason or another; however, multiple people said the same basic thing to me (paraphrased):

*"You don't need to use MCP; command line tools out perform the MCP connection for reverse engineering tasks."*

When I pressed on this, if there was actual data to support this, if there was merit to it, the answer I got was that it was "vibes." This was interesting to me because the same answer came from multiple people in the industry and when you look around, there's no shortage of people pushing some MCP ... something.
And that something will magically solve all of our reverse engineering problems, convince us we all need to get new jobs outside of the cyber bullet mines, and generally just be far better than anything. So I wanted to know if that's reasonably true given the fuzzy-nature of AI anyway. After all, if a tool can improve reverse engineering throughput by even 1x there's potential value, which is wild because it feels like the first time in my entire career that we've had the ability to answer demand.

The goal here isn't to say "MCP is worthless! Stop buying snake oil!!!" - it's more focused than that.
To me the question is simple - is MCP for reverse engineering tasks a placebo?
If it's a placebo, the agent is doing fine because it's a capable model with a shell, not because the MCP server taught it anything a `file`/`objdump`/`gdb` combo couldn't, right? Maybe stated more clearly:

*"An agent with access to a MCP system **WILL CONSISTENTLY** outperform the same agent restricted to coreutils + binutils + gdb + radare2 on a set of small RE tasks."*

Sadly I don't have infinite tokens to solve this side quest, but here's what I got over a weekend's worth of execution. Full disclosure, AI helped me bolt a lot of this together because I have more ideas than time - you get what you get.

<!-- more -->

## Approach

I worked with Claude and built a small harness, around three "arms" of different tool-access configurations for the same agent on the same task. The "arms" were:

- **`shell`** - shell/exec tools plus coreutils, binutils, gdb, radare2. No MCP
  at all. This is the "person doing it manually" baseline.
- **`shell_mcp`** - shell tools *and* the Ghidra MCP server. The agent can use
  either, or both (more on that in a moment).
- **`mcp_only`** - Ghidra MCP server only, shell/exec disabled entirely. Forces
  the agent to live inside Ghidra's decompiler/tool surface with no fallback.

**Why MCP Only???** you might ask - and my answer intent is that it is the control. Logically, if we removed every tool from the agent **except** MCP, now the agent and the model have to do all of the hard work normal things could solve (math, XORs, etc.). If the harness is working correctly, we should consistently see that MCP only scores horribly worse than either `shell` or `shell_mcp`.

Two agent CLIs got run through all three arms: Claude Code (Sonnet 4.6) and Codex CLI (GPT-5.4) - sorry I'm behind on getting this out, keeping track of "the latest model" isn't part of this effort.

The tasks themselves are small C binaries I had Claude write and then I modified afterwards to minimize the possibility of a perfect training match (but they're all so simple it's likely you'd generate the same basic code even without an agent). Each was given exactly one deliberate bug or ctf-style "thing" to hunt down. Each binary the agent got was a stripped copy to mimic a more realistic item we'd see in actual reverse engineering tasks (symbols??? ... lol). Along with the binary, I had it create a brief (what to find, what to report, i.e. "the prompt") and a private grading rubric that never touches the agent's context, only the grader's. Everything was small enough I reviewed it by hand ... but you know, at scale, it would probably be more interesting.

7 tasks x 3 arms x 5 repeats x 2 agents = 210 trials and more typing on the keyboard than I would have liked.

### The tasks

Seven tasks went into the matrix, each a stripped, never-published-before
binary with one thing to find:

- **`task01_license`**: a keygen-style check, given a username and serial, figure out the algorithm the binary uses to derive the expected serial from the username, then forge a valid pair
- **`task02_overflow`**: an interactive console with an unbounded `strcpy` into a fixed stack buffer; crash it and explain why, point to the vulnerable function's address, and the offset to the saved return address
- **`task03_callgraph`**: takes a single command byte and does something different for each. One of the eight paths reaches a piece of notable behavior through indirection (not a straight read of the input), and finding it means actually tracing the call graph instead of pattern matching the disassembly.
- **`task04_xorblob`**: one "unlock" input causes different output; recover what that output actually is via static analysis alone, this is the task where we'd expect MCP only to struggle since there are no other "tools" to enable the math
- **`task05_record`**: another crack-me style, takes a hex-encoded fixed-size binary record and rejects most inputs; recover the exact field layout (offsets, sizes, valid ranges) and construct a hex string the binary accepts.
- **`task06_fmtstring`**: another interactive console, this time with a classic format-string bug, get it to leak memory or crash, and correctly classify what kind of bug it is.
- **`task07_vm`**: takes a hex string, interprets it as bytecode for a small custom instruction set, reverse the opcode table, then hand-craft a program that makes it print exactly `1337`.

## How the scoring actually works

Every task has a rubric of specific claims an answer either does or doesn't make, each worth 1-2 points, adding up to a task-specific max (6 points for these 7). `task02_overflow`'s, for example:

| item | pts | what it checks for |
|---|---|---|
| `trigger_command` | 1 | names the actual vulnerable command |
| `gate_condition` | 1 | notices the command is gated behind an unlock code |
| `vuln_function` | 1 | names the function doing the unchecked copy, plus its address |
| `vuln_primitive` | 1 | correctly calls it an unbounded `strcpy` into a fixed-size stack buffer |
| `offset_to_ret` | 2 | reports the byte offset from the buffer to the saved return address |

Because I am the fox guarding the hen house on this and wanted to let it run over the weekend ... grading itself is a second, separate LLM call — same model, fresh context, no tools — that receives only the rubric and the trial's final answer text and returns a JSON verdict per checklist item (met/not-met plus a short
note), which gets summed into a score. The grader never gets to see the transcript, so it
can't be swayed by *how* the agent got there, only by what the final answer actually claims. Unfortunately, we can still trip up (as happened multiple times when debugging this crap) - the answer text itself can incidentally give away which arm produced it (an answer that name-drops a
Ghidra decompile call and now the dumb grading agent decides to spawn a sub-agent to go verify the claim...). As I highly doubt anyone from Anthropic, OpenAI, NVIDIA or MCP Product XYZ is making any grand sweeping changes based on this data, it's fine as it is; however, it is at least called out that it's an area in some other harnesses I decided to specifically move to "static grading" (which has its own new set of stupid problems). E.g. "Here be dragons."

## Results

The full 210-trial matrix, blind-graded, mean rubric score by arm and agent (**higher is better**):

![Score by tool-access arm](/wp-content/uploads/2026/mcplacebo-score.png)

And the effort it took to get there mean wall-clock seconds per trial (**lower is better**):

![Effort by tool-access arm](/wp-content/uploads/2026/mcplacebo-effort.png)

| arm | Claude wall-clock | Claude tool calls | Codex wall-clock | Codex tool calls |
|---|---|---|---|---|
| `shell` | 86.9s | 12.3 | 57.3s | 12.9 |
| `shell_mcp` | 76.3s | 12.5 | 62.3s | 12.3 |
| `mcp_only` | 112.6s | 22.1 | 74.9s | 19.5 |

Fortunately - we see our control pop out clearly. It is consistently the lowest score for both agents. It also consumes the most calls (expected). From this, we can infer at least our approach to measuring is reasonable.

## Observations
Now that we have a little confidence in our approach, what else can we observe about what happened for a relatively small data set (Dear Anthropic/OpenAI/NVIDIA: if you give me more tokens for free, I'll gladly run this over *the big stuff* I have sitting around, not just these toys :-) )

### Observation: `shell_mcp` vs plain `shell` is genuinely mixed
Claude scores marginally lower with MCP bolted on (95.7% vs 97.6%). This is small enough at n=35/arm that it could just be grading noise or standard error; however, it is *cheaper* on every token/cost metric with MCP available (~15–20% less output tokens, cache reads, and wall time). This means that `shell_mcp` comes out as the better score-per-dollar arm for Claude.

Codex shows a similar cost shape with `shell_mcp` being its best-scoring arm. Sadly tokens between Claude / Codex aren't really equal, so it's hard to say which is the most token-expensive one, so sadly there isn't a single "MCP is cheaper" or "MCP is pricier" story here and it looks to be agent-specific (with a stupid reason).

### Observation: The `mcp_only` no-calculator knee-capping doesn't promise it'll hurt
`mcp_only` disables shell entirely, which means no scratch arithmetic either. On the XOR-blob task that should be a real sticking point. And yet Claude scores *highest* on that exact task in `mcp_only` (100% vs 96.7% in `shell`), doing the keystream math by hand. Codex shows the opposite pattern on the identical task. Same constraint, opposite outcome, depending on the agent - or in my opinion, likely the model.

### Observation Annoyance: Claude & Codex don't handle MCP loads in the same way

Codex eagerly lists every MCP tool at session start; Claude Code defers almost everything, including MCP-provided tools, behind an explicit discovery step, so it doesn't even see the MCP surface until it goes looking for it. I had to nudge Claude's prompt to run tool discovery first specifically to compensate for that. This echoes a similar challenge I faced when working with an older Claude at work last year. This means that any Claude-vs-Codex delta here is partly a statement about how each CLI surfaces MCP tools which likely impacts the numbers (an exercise left to the reader).

Additionally, when breaking that same data down per task makes the "it depends on the task and the agent" point more concrete than the rolled-up averages do:

![Per-task score, by arm and agent](/wp-content/uploads/2026/mcplacebo-per-task.png)

A few things jump out per-task that the averages smooth over: Claude's `mcp_only` line beats its own `shell`/`shell_mcp` lines only on `xorblob` (the by-hand-arithmetic task) and is flat-to-worse everywhere else. Part of me wonders if Claude pulled this out of some existing test I've not been able to find with quick searching OR if it's just so common that XOR-ing needs to happen that Sonnet has trained extensively on it in some weird way.

Codex's `mcp_only` line actually *beats* its `shell` line on `overflow` and `callgraph`, which the aggregate numbers don't show at all; and `task07_vm` is the one task where all three arms cluster together for both agents, tool access just doesn't move it. Clearly that's just "hard" because it requires more long-view style thinking to maintain a "model" of the binary and the VM in the model's context. I can't prove it, but I could easily see it getting confused on which data is the code that executes and which data is the vm code that executes, thus driving a lot of the thrash.

## Where this goes next

The 7-task set above is a simple comparison which says there might be something wrong with the vibes *depending* on what variable you're attempting to maximize. If you're overly cost constrained, and the scaling holds true, 15-20% savings on your budget might be worth standing up all of the other infrastructure necessary to get the MCP systems working, especially if you're looking at hundreds of binaries or massive binaries (looking at you {insert_redacted})... but if you're pressed for time, you might get roughly the same results without the MCP system (in this type of use case for these types of evaluations).

I think we can say it's clear that MCP does help in some cases; however, it's far from a definitive "MCP **ALWAYS GETS THE W**".

In the future, I'll put the full harness, task sources, and the interactive results breakdown (since Claude and Codex aren't on comparable cost/token scales) in the [repo](https://github.com/wyattearp/MCPlacebo-eval-pub) once I get it cleaned up.
