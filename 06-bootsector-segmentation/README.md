## Some concepts and questions

*  **Why we need to read from the disk**: We know that BIOS loaded our boot code form the first sector of the disk, but that is **all** it loaded; what if our operating system code is larger than 512 bytes? So that operating systems usually don't fit into a single sector. so one of the first things they must do is
bootstrap the rest of the code from the disk into memory and then begin executing that code. And BIOS provides routines that allow us to manipulate data on the drivers.

* **The origin of segmentation**:
When the CPU runs in its intial 16-bit real mode, the maximum size of the registers is 16 bits, which means the highest address we can reference in an instuction is 0xffff, which amounts by today's standards to a measily 64KB. But a day-to-day operating systems would never sit comfortably
in such a tight box, so it is important to understand the solutionb, of segmentation, to this problem.

* **Segmentation**: To get around this limit, the CPU designers added a few more special registers, **cs,ds,ss and es**. called **segment** registers. We can imagine main memory as being divided into **segments** that are indexed by segmemt regiters. 
when we specify a 16-bit address, the CPU automatically calculates the absolute address as the appropriate segment's start address offseted by our specified address. By **appropriate segment**, I mean that, unless explicitly told otherwise, the CPU will
offset our address from the segment register appropriate for the context of our instruction.

* **Segment Register**:
1. *Data Segment*: ds -> used to modify the actual location of the data
2. *Stack Segment*: ss -> used to modify the actual location of the stack's base pointer,bp
3. *Code Segment*: cs -> used to modify the actual location of the code
4. *Extra Segment*: es -> used to be general purpose  register

* **How to calculate the absolute address**: The CPU multiplies the value in the segment register by 16 and then adds your offset address; and because we are working with hexadecimal, when we 
 multiplies a number by 16, we simply shift a digit to the left. So if we set ds to 0x4d and then issue the statement `mov ax, [0x20]`, the value stored in ax will actually be loaded from 
"16 * 0x4d0 + 0x20".

## Conclusion
Segment-based addressing allows us to reach futehr into memory, up a litle over 1MB(0xff*16+0xff).


