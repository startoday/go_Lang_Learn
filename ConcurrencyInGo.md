1. Power wall 
- If you get things runnning any faster, temperature will be high, and things will melt
- (dynamic) power equation: P = a*CFV^2   ; so people will think of decrease V to decrease power; but can't do too much due to 1. threshold 2. noise
- leakage power, when insulator getting thinner, (things are scale down) the leak of power is increasing 

2. concurrent execution
- concurrent execution is not necessarily the same as parallel execution(which things have to literally be executing at the same time)
- concurrent: start and end times overlap
- parallel will give faster time, since they are running at the same time=> must be executed on different hardware; concurrent tasks are "may be"
- mapping from tasks to hardware is not directly controlled by the programmer （not in go at least!)
- reason of using it: hiding latency!

3. Process
- things unique to process: memory - virtual address space, code, stack, heap...; registers-program counter, data regs, stack ptr

