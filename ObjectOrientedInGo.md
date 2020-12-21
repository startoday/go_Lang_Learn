1. Go Lang doesn't have class type. 
- It can define a class to have a **receiver type**
- the receiver type and function has to be in the same package
  ```
    type MyInt int
    func (mi MyInt) Double() int {return int(mi * 2)}
    func main(){
      m := MyInt(3)
      fmt.Print(m.Double()) // 6
    }
  ```
-  m is passed by value
2. controlling access
  ```
  package data
  var x int = 1
  func PrintX() {fmt.Println(x)} //can see x value from this function but no access to x
  ``` 
- controlling access to structs
  ```
  package data
  type Point struct{
    x float64
    y float64 
  }
  func ( p * Point) InitMe(xn, yn float64) {   // pass by reference!! reason is at 3
    p.x = xn   // dereferencing is automatic with . opertaor
    p.y = yn
  }
  package main 
  func  main (){
    var p data.Point
    p.InitMe(3,4)   //also here you don't need to reference it (*p)   when calling the method
  }
  ``` 
3. the receiver type is passed by reference, so,it won't change the receiver type
- when receiver is large, lots of copying is required
- when use pointer to pass by reference, no need to Deference! 

4. Better to be consistent, when you using pointer-receiver or  non-pointer-receiver!
