Heap Manager
============

A simple heap manager using segmented freelists and a first-fit selection protocol

## Structure ##
Each block has its own header and footer
#### Metadata Header ####
- Stores
 - Size: Byte size of block
 - Next: Pointer to next block
 - Prev: pointer to previous block

#### Footer ####
- Stores
 - Size: Byte size of block

#### Freelist Implementation ####
Uses an pointer array of size 10 grouping free blocks in buckets based on their corresponding sizes
- Example
  - 1: Holding 1-7    words
  - 2: Holding 8-15   words
  - 3: Holding 16-63  words
  - ...

##### Malloc && Free #####
Malloc implementation could use first-fit or best fit block selection based on initial selection. Then based on the found block size splits only when the leftover block would be a useful size.

Freeing coalesces, when possible, with both its previous and next blocks, then places the newly freed/merged block into its corresponding freelist.

##cd Test Case Results ##
Testing was done using both first-fit and best fit implementation (both with sorted lists and unsorted) and found first-fit produced the best results with the given methods.  
 - Test-Basic   : Heap Size: 1024         : Result: Passed
 - Test-Coalesce: Heap Size: 1024         : Result: Passed
 - Test-Stress1 : Heap Size: 1024         : Result: Passed
 - Test-Stress2 : Heap Size: 1024*1024*4  : Result: Passed
    - Loop count        : 50000
    - malloc successful : 41475
    - malloc failed     : 8525
    - execution time    : .100795 seconds
 - Test-Stress3 : Heap Size: 1024*1024*4  : Result: Passed
    - Loop count        : 50000
    - malloc successful : 41475
    - malloc failed     : 8525
    - execution time    : 1.446677 seconds
