---
layout: post
title: "xfs_repair Failures"
description: "Hours of a life lost in recovering 60TB of data"
category: 
tags: [technology,xfs,xfs_repair]
---

# The Issue
We have a **really** old SAN that we've been trying to migrate off of for months and just been unable to get any downtime time to do it ... but fun fact, if you don't make time for downtime, downtime will make time for you ... at the most inopportune time. Such is the case with our SAN that experience a failure due to a phased power outage. Upon returning the parts of the building back to normal, the ESXi / V-Sphere could no longer see the SAN and the SAN no longer wanted to mount the partitions and export them because of xfs errors (more on that at a later time).

Normally, I wouldn't write something up about this, but ServerFault isn't letting me post the answer and [I refuse to be this guy][1]:

![wisdom_of_the_ancients]({{"/wp-content/uploads/2022/wisdom_of_the_ancients.png" | absolute_url}})

After running through numerous [stack][2] [exchange][3] issues and not finding the answer, I landed back in recovery mode ... wondering what to do because I couldn't get the system to mount and it **needed to mount** to replay the corrupted log.

In recovery mode, a mount produced the following:

```
mount -t xfs -o ro, norecovery /dev/mapper/... /data
mount: structure needs cleaning
# checking for a /data in a mount command produced nothing :-(
```

Attempting to run an `xfs_repair` resulted in a failures and lead me to this [Serverfault stack exchange answer][2]; however, this procedure did not work as anticipated other errors seemed to indicate that updated versions of the `xfs_*` tools would correct the issue (they did not) by using various recuse ISOs (they produced the same output).

The actual issue was able to be identified by checking the `dmesg` output on the system:
```
Jan  7 14:47:35 san-storage kernel: XFS (dm-0): Mounting Filesystem
Jan  7 14:47:35 san-storage kernel: XFS (dm-0): Starting recovery (logdev: internal)
Jan  7 14:47:35 san-storage kernel: ffff88204d50a000: 45 46 49 20 50 41 52 54 00 00 01 00 5c 00 00 00  EFI PART....\...
Jan  7 14:47:35 san-storage kernel: XFS (dm-0): Internal error xfs_alloc_read_agf at line 2146 of file fs/xfs/xfs_alloc.c.  Caller 0xffffffffa024bc19
Jan  7 14:47:35 san-storage kernel: 
Jan  7 14:47:35 san-storage kernel: Pid: 1701, comm: mount Not tainted 2.6.32-431.el6.x86_64 #1
Jan  7 14:47:35 san-storage kernel: Call Trace:
Jan  7 14:47:35 san-storage kernel: [<ffffffffa0276e5f>] ? xfs_error_report+0x3f/0x50 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa024bc19>] ? xfs_alloc_read_agf+0x39/0xd0 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa0276ece>] ? xfs_corruption_error+0x5e/0x90 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa024bb40>] ? xfs_read_agf+0x100/0x1a0 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa024bc19>] ? xfs_alloc_read_agf+0x39/0xd0 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa029bf57>] ? kmem_zone_alloc+0x77/0xf0 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa024bc19>] ? xfs_alloc_read_agf+0x39/0xd0 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa024bcca>] ? xfs_alloc_pagf_init+0x1a/0x40 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa0291350>] ? xfs_initialize_perag_data+0xa0/0x120 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa0291e18>] ? xfs_mountfs+0x558/0x6a0 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa02a995c>] ? xfs_fs_fill_super+0x25c/0x310 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffff8118c38e>] ? get_sb_bdev+0x18e/0x1d0
Jan  7 14:47:35 san-storage kernel: [<ffffffffa02a9700>] ? xfs_fs_fill_super+0x0/0x310 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffffa02a77d8>] ? xfs_fs_get_sb+0x18/0x20 [xfs]
Jan  7 14:47:35 san-storage kernel: [<ffffffff8118b7fb>] ? vfs_kern_mount+0x7b/0x1b0
Jan  7 14:47:35 san-storage kernel: [<ffffffff8118b9a2>] ? do_kern_mount+0x52/0x130
Jan  7 14:47:35 san-storage kernel: [<ffffffff811ac94b>] ? do_mount+0x2fb/0x930
Jan  7 14:47:35 san-storage kernel: [<ffffffff81140d64>] ? strndup_user+0x64/0xc0
Jan  7 14:47:35 san-storage kernel: [<ffffffff811ad010>] ? sys_mount+0x90/0xe0
Jan  7 14:47:35 san-storage kernel: [<ffffffff8100b072>] ? system_call_fastpath+0x16/0x1b
Jan  7 14:47:35 san-storage kernel: XFS (dm-0): Corruption detected. Unmount and run xfs_repair
```

Checking a `mount` command would actually show that nothing mounted successfully; however, the kernel still believed that it occurred, even on a reboot into a recovery (no idea why - it shouldn't!). Running an `unmount -f /data/ /dev/mapper/...` resulted in successfully enabling the `xfs_repair /dev/mapper/...` to execute without the need for the `-L` flag and allowed for restoration of the data.

Depending on your system, a combination of several of the answers steps would result in restoring the system to functionality. The final procedure identified was:

## Gain Access To Partitions
 1. **Assumption - you are rebooted into recovery mode or the system is "unmounted"**
 2. Identify and make nodes for LVM: `vgscan -v --mknodes` 
 3. Activate LVM nodes: `vgchange -a y`

## Unable to Mount
 1. Attempt to mount the partition using `mount`, this will likely fail
 2. Attempt to repair the parition using `xfs_repair`, this will likely fail
 3. Verify that `dmesg` indicates that you need to umount the partition
 4. Unmount the partition using an `umount -f /path/to/mnt/point /dev/mapper/...` (**note the included the path to the device**)
 5. Verify that the partition does not show as mounted in a `mount`
 6. Run an `xfs_repair -n /dev/mapper/...` - this should succeed
 7. Optional - inspect each item with an `xfs_db` by checking each inode to understand what would happen if it was corrected
 8. Run an `xfs_repair /dev/mapper/...`
 9. Mount the partition using a `mount /path/to/mnt/point` and inspect for data loss
 10. **BACKUP UP YOUR DATA**
 

## Clean Mount
 1. Attempt to mount the partition using `mount`
 2. Run a `mount` and verify the partition shows as mounted to replay the log
 3. Run a `unmount /path/to/mnt/point`
 4. Run an `xfs_repair -n /dev/mapper/...`
 5. Optional - inspect each item with an `xfs_db` by checking each inode to understand what would happen if it was corrected
 6. Run an `xfs_repair /dev/mapper/...`
 7. **BACKUP YOUR DATA**


  [1]: https://xkcd.com/979/
  [2]: https://serverfault.com/a/834853
  [3]: https://superuser.com/a/430719/311569