## Some concepts and questions

* Why we need to read from the disk?
Answer: We know that BIOS loaded our boot code form the first sector of the disk, but that is **all** it loaded; what if our operating system code is larger than 512 bytes? So that operating systems usually don't fit into a single sector. so one of the first things they must do is
bootstrap the rest of the code from the disk into memory and then begin executing that code. And BIOS provides routines that allow us to manipulate data on the drivers.

* The origin of segmentation:
When the CPU runs in its intial 16-bit real mode, the maximum size of the registers is 16 bits, which means the highest address we can reference in an instuction is 0xffff, which amounts by today's standards to a measily 64KB. But a day-to-day operating systems would never sit comfortably
in such a tight box, so it is important to understand the solutionb, of segmentation, to this problem.

* Segmentation: To get around this limit, the CPU designers added a few more special registers, **cs,ds,ss and es**. called **segment** registers. We can imagine main memory as being divided into **segments** that are indexed by segmemt regiters. 



