## Some concepts:

* **TTY**: tty is acommand in Unix and Unix-like operating systems to print the file name of the terminal
and connected to standard input. 

* **Interrupts**: A mechanism that allow the CPU temporaily to halt what it is doing and run some other
higher-priority instructions before returning to the original task. An interrupt could be raised either by a software instruction(e.g. int 0x10) or
by some hardware devices that requires high-priority action(e.g. to read some incoming data from a network device) 

* **Interrupt Service Routines(ISRs)**: A table initally set up by BIOS at the start of memory. An ISR is simply a sequence of machine instructions, much like
our boot sector code, that deal with sepcific interrupt. And each interrupt is represented by a unique number that is an index to the ISRs, for example: interrupt 0x10 
causes the screen-related ISR to be invoked and interrupt 0x13: the disk-related I/O ISR.

* **CPU register**: Just as we use variables in high level languages, it is useful if we can store data temporarily during a particular routine. All x86 CPUs have four general purpose
**registers,ax,bx,cx,and dx.** for that purpose. Examples:
```assembly mov ax  1234; store the decimal number 1234 in ax
    mov al  0x56; ax -> 0x1256
    mov ah  0x34; ax -> 0x3456
```
* **16-bit real mode**: Means the CPU's instructions can work with a maximum of 16-bits at once 


## Goal: Make our previously silent boot sector print some text
1. write our hello program
```assembly 
mov ah, 0x0e ; tty mode
mov al, 'H'
int 0x10
mov al, 'e'
int 0x10
mov al, 'l'
int 0x10
int 0x10 ; 'l' is still on al, remember?
mov al, 'o'
int 0x10

jmp $ ; jump to current address = infinite loop

; padding and magic number
times 510 - ($-$$) db 0
dw 0xaa55

``` 
2. `nasm -f bin boot_sect_hello.asm -o boot_sect_hello.bin`
3. `qemu-system-x86_64 boot_sect_hello.bin --nographic --curses` 




## Reuslts:
  ![image](https://user-images.githubusercontent.com/58657543/160834636-7e7db0cd-25bd-4564-bcfe-f2cbb8a8393d.png)





