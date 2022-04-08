## Some Concepts:
* 32-bit protected mode: 

* Video Graphics Array(VGA): A video display controller, the video memory of the VGA is mapped to the PC's memory via a window. The VGA memory starts address **0xb8000** and it has a text mode which is useful to avoid manipulating direct pieels.
The formula for accessing a specific character on the 80x25 grid is:
``` 
0xb8000 + 2 * (row * 80 + col)
``` 

* Global Descripter Table(GDT): A complex data structure in memory, Used to define momory segments and their protected-mode attributes. Once we have defined the GDT, we can use
a special instruction to load it into the CPU. And we do not use the old method in 16-bit real mode to translate logical address to physical address, instead we use a segment register to index a particular  **segment descripter** in the GDT. 


* Why entering 32-bit protected mode?
1. Make fuller use of the CPU
2. To better understand how developments of CPU architectures can benefit modern operating system(memory protection in hardware)

* The main differences in 32-bit protected mode:
1. Registers are extended to 32 bits, with their **full**  capacity being accessed by prefixing an **e** to the register name: 
``` 
mov ebx, 0x274fe8fe 
```
2. There are two aditional general purpose registers: **fs**, and **gs**
3. 32-bit memory offsets are available, so an offset can reference a whopping 4GB of memory
4. The CPU supports a more sophisticated means of memory segmentation, which offers two big advantages:
    * Code in one segment can be prohibited from executing code in more privilidged segment, so you can protect your kernel code form user applications.
    * The CPU can implement **virtual memory** for user processes, such that **pages**(i.e. fixed size of chunks) of a process's memory can be swapped transparently between **the disk and memory** on an as-needed basis.
This ensure main memory is used efficiently, in that code or data that is rarely executed needn't hog valuable memory

