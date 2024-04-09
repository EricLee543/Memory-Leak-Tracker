# Memory-Leak-Tracker

This is a toy project for completing CS302 Operating System.

This program can record each memory allocation by using `instrumentation` (插桩) techniques when invoking functions such as malloc, calloc, and new in C/C++. It can also record each memory deallocation when invoking functions such as free and delete. Upon program exit, it outputs the addresses of unfreed/deleted memory to detect memory leaks.

## Feature

It is limited to only output memory leaks at the end of the program. This toy project also supports online searching for memory leak chunks which are unreferenced and not freed/deleted for a long time.

- At the beginning of the program, it queries `/proc/self/maps` to find the start and end positions of the stack memory.
- Each time a memory allocation/deallocation function is called, it prints the stack memory by using the stack range got from step 1.
- Analysis.cpp analyzes whether the allocated heap memory addresses appear in the stack memory. If they do not appear in the stack, it indicates a memory leak.

## How to run

```
cd ./c && ./run.sh
or
cd ./cpp && ./run.sh
```

## Warning

This project will change the default malloc/calloc/free/new/delete functions in C/C++ by using `LD_PRELOAD` technique. It may cause some problems when running other programs. Please use it with caution. You can unset the `LD_PRELOAD` environment variable to disable this feature.
