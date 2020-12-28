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

4. Goroutines
- like a thread in Go
- Many Goroutines execute within a single OS thread

5. Go Runtime Scheduler
- like a little OS inside a single  OS thread
- programmer can determine how many logical processors that are going to be used

6. create a goroutine
- one goroutine is created automatically to execute the main()
- other goroutines are created using the **go** key word
  ```
    a = 1
    foo()   // main goroutine blocks on call to foo()
    a = 2
  ```
  with goroutine
  ```
    a = 1
    go foo()   // new goroutine blocks create foo(), main goroutine does not block
    a = 2
  ```
- if main finish first, then you may not able to see goroutine finish （early exit)

7. wait group
- add() increments the counter; done() decrements the counter; wait() blocks until counter == 0
  ```
  func foo(wg * sync.WaitGroup){
    fmt.Printf("New routine")
    wg.Done()
  }
  func main(){
    var wg sync.WaitGroup
    wg.Add(1)
    go foo(&wg)
    wg.Wait()
    fmt.Print("Main routine)
  }
  ```
  
8. channels
- communicatuiion through goroutines are using channels
- channels are typed
- use make() to create a channel =>  c := make(chan int)
- send data: c<-3   receive data from a channel x := <- c

  
