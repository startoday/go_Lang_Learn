1. func sth(x,y int) // when x and y are both int, you only need to pass once
2. can do multiple returns 
3. Go Lang is call by Value. advantage: data encapsulation: it can restrict errors in local; disadvantage: copying time
  - to pass by reference: func foo(y * int)  
4. pass array 
- func foo(x * [3]int){}  => foo(&arr)
- usually pass slice instead, passing the slice copies the pointer !!!!
  ```
    func foo (sli []int) {
      sli[0] = sli[0] + 1
    }
    func main(){
      a := []int{1,2,3}
      foo(a)
      fmt.Print(a) // 2,2,3
    }
  ```
5. variables as functions
  ```
    var funcVar func(int) int
    func incFn(x int) int {
      return x + 1
    }
    func main() {
      funcVar = incFn  //no parathesis 
      fmt.Print(funcVar(1))  //2
    }
  ```
6. functions as arguments
  ```
    func applyVal(afunc func(int) int, val int) int {
      return afunc(val)
     }
    func incFn( x int) int {return x + 1 }
    func decFn( x int) int {return x - 1 } 
    func main() {
      fmt.Println(applyVal(incFn, 1))  //2
      fmt.Println(applyVal(decFn, 1))  //0
    }
  ```
7.anonymous functions
  ```
    func applyVal(afunc func(int) int, val int) int {
      return afunc(val)
     }
    func main() {
      fmt.Println(applyVal(func ( x int) int {return x + 1 }, 1))  //2, no name is needed for that function
    }
  ```   
8. functions as return values
  ```
    func MakeDistOrigin (o_x, o_y float64) func (float64, float64) float64{
      fn := func(x,y float64)float64{return math.Sqrt(math.Pow(x- o_x,2) + math.Pow(y- o_y,2))}
      return fn
    }
    func main(){
      Dist1 := MakeDistOrigin(1,1)
      Dist2 := MakeDistOrigin(0,0)
		  fmt.Println(Dist1(2,2)) //Sqrt(2)
      fmt.Println(Dist2(2,2)) //Sqrt(8)
    }
    
    func fA() func() int {
	    i := 0
	    return func() int {
		i++
		return i
	    }
    }
   func main() {
	   fB := fA()
	   fmt.Println(fB()) //1
	   fmt.Println(fB()) //2
   }
  ``` 
9. closure
- when functions are passes/returned, their environment comes with them! just like the example in 8

10.variable argument number
- use ... for functions to take variable number of arguments; treated as a slice inside function
  ```
    func getMax(vals ... int) int{
       maxV := -1
       for _, v := range vals{ if v > maxV  {maxV = v }}
       return maxV
    }
    func main(){
		  fmt.Println(getMax(1,2,5,623,7)) //623
      //you can also pass a slice
		  vslice :=[]int{1,2,5,2,3}
      fmt.Println(getMax(vslice...)) //5, remember to add ... after slice!
    }
  ```
11. deferred function calls 
- call can be deferred until the surrounding function completes
- typically used for cleanup activities
```
  func main(){
    defer fmt.Println("bye")
    fmt.Println("hi")
    //print hi   bye
  }
```
- arguments are evaluated immediately; but function is deferred 
```
  func main(){
    i := 1
    defer fmt.Println(i)
    i++
    fmt.Println("hi")
    //print hi  1
  }
```
        
