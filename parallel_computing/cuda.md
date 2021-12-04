# CUDA

## SHARED MEMORY
Shared memory is inside the chip, so acces to this memory is faster and limited amount of
storage. Goal is to minimize the amount of read and writes to the global memory which is
slower since it's DRAM and located outside the chip.

## EXECUTING A KERNEL
A Kernel, in CUDA, is a function that's being run on the GPU. We run the kernel by calling
Kernel<<<grid_dim, block_dim>>>  
- Kernel : name of the function
- Block : the amount of block we want
- Threads : the amount of threads per block 
  - When using a dim3 to create the THREADS variable, i.e. (4, 5) : 
    - 4 :

