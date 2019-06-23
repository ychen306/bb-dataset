This is a tool that automatically profiles the throughput of user-level x86-64 basic blocks.

Usage: `./a64-out.sh <REPS>`, where `REPS` is an integer.

The script reports the latency of running the code in `bb.bin` (unrolled `REPS` times),
where `bb.bin` contains the encoded binary (the raw binary, not binary in ELF or other formats)
of the code you want to profile;
The reported latency includes the overhead of measurement. 
To get the true throughput of a basic block we suggest you do the following
```
let a = 200
let b = 100
let latency_a = measure code unrolled a times
let latency_b = measure code unrolled b times
let throughput = (latency_a - latency_b) / (a - b)
```
We are releasing a wrapper script that does this automatically .

# Why you might want to use this tool

Q: Why yet another tool for throughput profiling (nanoBench, Agner Fog's script, etc)?  
A: Because sometimes you want to profile a piece of code with memory accesses,
and it's hard to do the setup (i.e. proper memory allocation + initialization of registers to avoid crashing).

Q: Does this always work (i.e. not crash)?  
A: No, but it works most of the time.
We have profiled 97% of basic blocks collected from raw binaries of various applications.
And 94% out of all basic blocks are profiled with stable timing and no cache misses.


Q: Does this work with basic blocks using RIP addressing?  
A: Not always, but most of the time.
