## Some Concepts:
* BIOS -> Basic Input and Output System, a collection of software routines that are initially loaded from chip into memory and initialised when the computer is switched on.
After BIOS completes some low-level tests of the hardware, it must boot the operating system stored on one of your devices(floopy disk, hard disk and so on), since BIOS has no 
notion of file system now, BIOS must simply load a file that represents your operating system. So the first step is to find the location of our operating system and the easiest place for
BIOS to find our OS is in the first sector if one of the disks(i.e. Cylinder0, Head0, Sector0), knon as **boot sector**. But sicne our disks may not contain an operating system, so it is 
important for ous BIOS to determine whether the boot sector of a particular disk is boot code that is intended for execution or simply data. Note that the CPU can not differentiate between code
and data: both can be intepreted as CPU instructions. Again, an unsophisticated way adopted here by BIOS, whereby **the last two bytes of an intended boot sector must be set to the magic number 0xaa55** 

* Assembler -> Translate assemble code to raw machine code. 


## Goal: Create a file which the BIOS interprets as a bootable disk
1. Writing following assemble code into your text editor.
```
  ; Infinite loop (e9 fd ff)
loop:
    jmp loop 

; Fill with 510 zeros minus the size of the previous code
times 510-($-$$) db 0
; Magic number
dw 0xaa55 
  
```
2. nasm -f bin boot_sect_simple.asm -o boot_sect_simple.bin -> insruct nasm to produce raw machine code from assemble code 
3. qemu-system-x86_64 boot_sect_simple.bin --nographic --curses -> execute boot code 

## Results:

![](https://user-images.githubusercontent.com/58657543/148485046-94c92174-97cb-4ceb-9549-331b6c42267f.png)
* Note: (You keep waiting cause our code is an Infinite loop)
