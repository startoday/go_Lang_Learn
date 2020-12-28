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
  ```
    package main
    import "fmt"

    func prod( v1, v2 int, c chan int) { c <- v1 *v2}
    func main(){
      c := make(chan int)
      go prod(1, 2, c)
      go prod(3, 4, c)
      a := <- c
      b := <- c
      fmt.Println(a*b) //24
    }
  ```
9. blocking channels
- channel is default as unbuffered channel. which means it can NOT hold data in transit
- sending blokcings until data is received, eg A received 3, and it will blocked, hold until this data is received - receiving blocks until data is sent
- this means the channel is doing synchronization

10. buffered channel
- block is usually a bad thing, will reduce the concurrency
- default size is 0; but we can set the size in make. eg: c:= make(chan int, 3)
- sending only blocks if buffer is full
- receiving only blocks if buffer is empty
   ```
    package main
    import "fmt"

    func prod( v1, v2 int, c chan int) { c <- v1 *v2}
    func main(){
      c := make(chan int, 3)
      go prod(1, 2, c)
      go prod(3, 4, c)
      fmt.Println(<- c * <- c) //24
    }
   ```

11. iterating through a channle
   ```
    for i : = range c{ fmt.Println(i)}  // it will continue to read from channel c; one iteration each time a new value is received; infinite loop
    // iterates end when sender calls close(c)
   ```

12. receiving from multiple goroutines
- may have a choice of which data to use, first come first seved => use **select**
```
  select{
    case a = <- c1:
      fmt.Println(a)
     case b = <- c2:
      fmt.Println(b)
     case outchan <- c:
      fmt.Println("sent c")   // you can select both send and receive; which ever comes first will be picked
     default:
      fmt.Println("nope")   // use a default to avoid blocking
  }
```
- select with an Abort channel; there is a seperate abort channel; will receive data until an abort signal is received ( don't care which is sent)
```
  for{
    select{
      case a = <- c1:
        fmt.Println(a)
       case  <- abort:
        return
    }
  }
```
