---
title: A Deleted File Can Still Be Alive
date: 2026-09-25 21:31:00 +/-0530
categories: [Infra]
tags: [til]     # TAG names should always be lowercase
math: true
---

# TIL: A Deleted File Can Still Be Alive

If a process has a file open, deleting it doesn't free the data — only
the directory *name* goes away. The data (inode) sticks around until
every open file descriptor referencing it is closed.

## Why

Linux separates **names** (directory entries) from **data** (inodes).
`rm`/`unlink()` removes the name and decrements the inode's link count.
The kernel only frees the inode's disk blocks when:
- link count == 0 (no name points to it), **and**
- open fd count == 0 (no process has it open).

## How I hit this

A KVM guest's qcow2 disk (`vda.qcow2`) was deleted from disk out from
under a **running** QEMU process. `virsh console` still worked — the
VM was fine, because QEMU's fd to the file was still open.

```bash
ls -l /proc/<qemu-pid>/fd | grep qcow2
lrwx------ 1 libvirt-qemu kvm 64 ... 14 -> /data/.../vda.qcow2 (deleted)
```

The `(deleted)` suffix is the kernel telling you: "this fd's target has
no name anymore, but the data is still alive."

## The recovery trick

Read the data back out through the still-open fd, before the process
ever closes it:

```bash
cp /proc/<pid>/fd/<N> /path/to/recovered-file
```

Once that process exits, the inode's link count *and* open-fd count
both hit zero — data is gone for good.

## Minimal repro

```bash
tail -f /tmp/testfile &                 # holds a read fd open
PID=$!
rm /tmp/testfile                        # name gone, data still alive
ls -l /proc/$PID/fd | grep deleted      # -> testfile (deleted)
cp /proc/$PID/fd/3 /tmp/recovered       # rescue it
kill $PID                               # now it's truly gone
```

## References
- `man 2 unlink` — https://man7.org/linux/man-pages/man2/unlink.2.html
- `man 5 proc` (`/proc/<pid>/fd`) — https://man7.org/linux/man-pages/man5/proc.5.html

