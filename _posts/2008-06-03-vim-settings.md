---
id: 211
title: Vim Settings
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=211
permalink: /2008/06/03/vim-settings/
categories:
  - Rants
  - Technology
tags:
  - programming
  - vim
---
This really isn&#8217;t for anyone else other than myself. I&#8217;m sick and tired of having to look up all the vim commands to put in my .vimrc file every time I build/logon to a new system. Maybe you&#8217;ll get some joy out of the comments. [Here it is][1]:

<div class="codesnip-container" >
  &#8221; enable syntax highlighting because it&#8217;s pretty and useful and it should be on by effing default!!!<br /> syntax on</p> 
  
  <p>
    &#8221; show the current cursor position in the bottom right cause i can&#8217;t count lines for crap<br /> set ruler
  </p>
  
  <p>
    &#8221; show incomplete command in the lower right corner for when i forget insane vim commands<br /> set showcmd
  </p>
  
  <p>
    &#8221; allow backspace to work and not annoy the ever living crap out of me<br /> set backspace=1
  </p>
  
  <p>
    &#8221; jump to matching [({ thingys. sometimes i like this, sometimes i don&#8217;t<br /> set showmatch
  </p>
  
  <p>
    &#8221; show search matches as you type because i&#8217;m generally looking for mis-speeellings<br /> set incsearch
  </p>
  
  <p>
    &#8221; make the mouse enabled at all times because i like being able to paste crap in<br /> set mouse=a
  </p>
  
  <p>
    &#8221; makes Vim use the indent of the previous line for a newly created line otherwise i can&#8217;t read my own code<br /> set autoindent
  </p>
  
  <p>
    &#8221; i don&#8217;t know what this is, but if it makes my code smarter, i want to use it<br /> set smartindent
  </p>
  
  <p>
    &#8221; highlight search results so you can actually find what you&#8217;re looking for<br /> set hlsearch
  </p>
  
  <p>
    &#8221; lots of fun stuff for specific files<br /> filetype plugin indent on
  </p>
  
  <p>
    &#8221; allow the EOL to be backspaced over cause i like getting the previous line too<br /> set backspace=2
  </p>
</div>

 [1]: http://hackerforhire.org/vimrc