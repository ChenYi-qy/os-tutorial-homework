## Some Concepts:
1、BIOS -> Basic Input and Output System,电脑在启动的时候必须加载操作系统(可能是从硬盘、USB等)，
这个时候还没有文件系统，但我们有BIOS，一段会在电脑开启的时候从芯片加载进内存的软件程序，BIOS提供
自动检测和对电脑设备的最基本的控制(屏幕，键盘，硬件等)，BIOS在完成一些硬件的low-level test(例如
内存是否正常工作)后会启动存储设备的操作系统。由于BIOS没有文件系统的概念，它只能读取指定扇区的数据
，而最容易发现操作系统的地方肯定是第一个磁盘的第一个扇区(例如：Cylinder0,Head 0,Sector 0),但我们的
磁盘也可能没有操作系统，对BIOS来说，它必须具备检测启动扇区存储的数据是boot code还是data,因为这两个
都可以被解释为CPU指令。

如果启动扇区的最后两个字节为"magic number" 0xaa55的话，BIOS就会识别为boot code,并将boot code加载进
内存，CPU就开始指令the first boot sector it finds that ends with the magic number

2、CPU Emulator -> translate low-level display device instructions into pixel rendering on a 
desktop window.


## Goal: Create a file which the BIOS interprets as a bootable disk
1、将以下512个字节写进binary editor后者写一段简单的汇编语言
```
  ; Infinite loop (e9 fd ff)
loop:
    jmp loop 

; Fill with 510 zeros minus the size of the previous code
times 510-($-$$) db 0
; Magic number
dw 0xaa55 
  
```
2、nasm -f bin boot_sect_simple.asm -o boot_sect_simple.bin -> 编译
3、执行boot code -> qemu boot_sect_simple.bin(ubuntu下需要加上--nographic and/or --curses flags)  
