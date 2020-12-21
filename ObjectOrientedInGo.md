1. Go Lang doesn't have class type. It can define a class to have a receiver type

  ```
    type MyInt int
    func (mi MyInt) Double() int {return int(mi * 2)}
    func main(){
      m := MyInt(3)
      fmt.Print(m.Double()) // 6
    }
  ```
2. 
