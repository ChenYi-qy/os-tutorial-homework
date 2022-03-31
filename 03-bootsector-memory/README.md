## Some Concepts
* Memory Offsets: Our boot sector is somewhere in memory(the start of our boot-sector code, is at some address in memory, while the addresses in boot sector is relative the start of boot-sector address
rather than the start of memory. So we need to figure out its absolute address, which is 0x7c00(start of boot-sector) + label-memory offset. While it is inconventient to always to have to account for
this lable-memory offset in our code, so many assemblers will correct label references during assemblege if you include the following instruction at the top of your code, telling it exactly where
you expect the code to loaded in memory:
```
[org 0x7c00]
```

## Goals
1. Try to comilple and execute "boot_sect_memory.asm" and "boot_sect_memory_org" by yourself to understand memory offset.
2. Learn how the computer memory is origanized(page 14 of [this doc](http://www.cs.bham.ac.uk/~exr/lectures/opsys/10_11/lectures/os-dev.pdf)).

