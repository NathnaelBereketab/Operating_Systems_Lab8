# Lab 8: Memory Management Simulation

## Overview
Implementation of three memory allocation policies (First Fit, Best Fit, Worst Fit) with support for memory deallocation and coalescing.

## Compilation
```bash
cd MMU
make mmu
```

## Usage
```bash
./mmu <input_file> -{F|B|W}
```

### Examples
```bash
./mmu input0.txt -F    # First Fit
./mmu input0.txt -B    # Best Fit
./mmu input0.txt -W    # Worst Fit
```

## Input Format
```
<INITIAL_PARTITION_SIZE>
<PID> <BLOCKSIZE>          # Allocate memory
-<PID> 0                   # Deallocate memory
-99999 0                   # Coalesce free blocks
```

## Implementation Details

### Functions Implemented
- `list_is_in_by_pid()` - Check if PID exists in list
- `list_add_ascending_by_address()` - Insert blocks sorted by address
- `list_add_ascending_by_blocksize()` - Insert blocks sorted by size (ascending)
- `list_coalese_nodes()` - Merge physically adjacent blocks
- `allocate_memory()` - Allocate memory using specified policy
- `deallocate_memory()` - Free memory from process

## Files
- `list.c` - Linked list implementation
- `list.h` - List header file
- `mmu.c` - Memory management unit implementation
- `util.c` - Utility functions
- `util.h` - Utility header
- `Makefile` - Build configuration

## Test Results

### First Fit (-F)
- Allocates from first available block (FIFO)
- PID 8 allocated at: `39950-41183`
- Final coalesced blocks: `0-1049`, `5050-11049`, `39950-99999`

### Best Fit (-B)
- Allocates from smallest suitable block
- PID 8 allocated at: `1050-2283` (smaller block chosen)
- Final coalesced blocks: `0-2283`, `6284-11049`, `39950-99999`

### Worst Fit (-W)
- Allocates from largest available block
- PID 8 allocated at: `39950-41183` (largest block chosen)
- Final coalesced blocks: `0-11049`, `39950-41183`, `45184-99999`

## Author
Nathnael Bereketab
