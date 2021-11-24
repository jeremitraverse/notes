# L1 cache vs Shared Memory
L1 cache is automaticly managed by CUDA and shared memory is managed by your code. Shared
memory is used to store data that should be shared between threads with predictable timing

When we use the share memory -> need to sync our thread with syncthreads()

# 1D Convolution
- Applying a mask on a matrix 
- Mask are usually small and have a odd number width

## How to deal with frontiere
- All elements that are out of bounderies = 0 (ghost cells)

## Possible optimization
- Usage of the constant memory instead of the global memory
  - Cuda copies the constant memory inside the L1 cache for faster read spead

# 2D Convolution
