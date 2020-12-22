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

5. Polymorphism
- identical at a high level of abstraction
- different at a low level of abstraction
- Go Lang doesn't have inheritance

6.Type satisfies an interface if type defines all methods specified in the interface (same method signature)
- no need to state it explicity
  ```
    type Shape2D interface {
      Area() float64
      Perimeter() float64
    }
    type Triangle {...}
    func (t Triangle) Area() float64 {...}
    func (t Triangle) Perimeter() float64 {...}
  ```

7. Interface type and Interface value

  ```
  type Speaker interface {Speak()}
  type Dog struct {name string}
  func (d Dog) Speak(0 {fmt.Println(d.name)}
  func main(){
    var s1 Speaker
    var d1 Dog{"Brain"}
    s1 = d1  // dynamic type is dog and dynamic value is d1
    s1.Speak()
  }
  ```
  - nil dynamic value is valid; can still call the method; better to check the dynamic value in the dynamic type method
  - nil interface value = interface with nil dynamic type => can't call the method => throw error
    
8. when to use interface
- need a function which takes multiple types of parameter
  
  FitInYard()  Shape need to have Area() and Perimeter() 
  ```
    func FitInYard(s Shape2D) bool {
      if (s.Area() > 100 && s.Perimeter() >100 ){return True} 
      return False
    }
  ```
9. Empty Inteface
- empty interface specifies no methods
- all types satisfy the empty interface
- use it to have a function accept any type as a parameter
  ```
  func PrintMe(val interface{}) {fmt.Println(val)}
  ```
10. Interface concealing type differences

11. Type Assertion
-  rec, ok :=s.(Rectangle)  if ok {DrawRect(rec)} //s Shape2D
```
  func DrawShape(s Shape2D) bool {
    switch := sh :=s.(type) {
    case Rectangle "
      DrawRect(sh)
    case Triangle:
      DrawTri(sh)
    }
  }
```
12. Error handling
- correct operation : error == nil
  ```
  f, err := os.open("xx.text")
  if err != nil {
    fmt.Println(err)
    return
  }
  ```
  
   
