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
5. 
