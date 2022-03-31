## Goal: Learn to how to code basic stuff(loops,functions) with the assembler

## Strings
Define strings like bytes, but terminate them with a null-byte(like C) to be ablle to determine
their end. 
-> mystring:
        db 'Hello Wolrd',0

## Calling Functions
At the CPU level a function is nothing more than a jump to the address of a
useful routine **then a jump back again** to the instruction immediately following
the first jump.


## Include Files  
Sometimes you will likely reuse your code in multiple programs. nasm will allow
you to include external files as follows:
```
%include "xxx.asm"
```

