## The origin of stack 
The stack is really just a simple solution to the following inconvenience: the CPU has a limited number of **registers** for the temporary storage our routine's local varibales, but we often
need more temporary storage than will fit into these registers; now, we can obviously make use of our main memory, but specifiying specific memory address when reading and writing is inconvenient
, especially since we do not care exactly where the data is to be stored, only that we can retrieve it easily enough. The stack is also useful for argument passing to realise function calls.

## How to implement a stack
The CPU offers two instructions **push** and **pop** that allow us, repectively, to store a value and retrieve a value from the top the stack, and so without worrying exactly where they are stored.
The stack is implemented by two special CPU registers, **bp** and **sp**, which matain the addresses of the stack base and stack top respectively. Since the stack expands as we push data onto it, we 
usually set the stack's base far away from important regions of memory(e.g. such as BIOS code or our code) so there is no danger of overwriting if the stack grows too large. One confusing thing 
about the stack is that it actually grows **downwards** from the base pointer, so when we issue a push, the value actually gets stored below -- and not above -- the address of bp, and sp is decremented
by the value's size.

## Goals
Compile and execute `boot_sect_stack.asm` and see whether the output conform to your expectation.

