## Some Concepts:
* Cylinder-head-sector(CHS): an early method of giving addreses to each physical block of data on a hard disk drive. A cylinder is comprised of tracks decribed by all the heads(on separate plattters) at a single seek position. Each cylinder is equidistant from the center of the disk.
A track is divided into segments of **sectors**, which is the basic unit of storage.

* Cylinder: the cylinder describes the head's discrete distance from the outer edge of the platter and is so named since, when several platters are stacked up, you can visualise that all of the heads select a cylinder through all of the platters

* Head: the head describes which track (i.e. which speciac platter surface within the cylinder) we are interested in.

* Sector: the circular track is divided into sectors, usually of capacity 512 bytes, which can be referenced with a sector index.

* Carry Bit: an extra bit present on each register which stores when an operation has overflowed its current capacity.
```
mov ax, 0xFFFF
add ax, 1 ; ax = 0x0000 and carry = 1
```

## Goal: boot our os by reading from the disk
Note:
1.  boot secor -> sector1 of cylinder0 of head0 of hdd0; Any bytes after 512 correspond to sector2 of cylinder0 of head0 of hdd0
2. al -> the number of sectors actually read
3. jc -> jumps only if the carry flag was set
 

  

