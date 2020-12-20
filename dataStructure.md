1. arrays
- fixed-length series of elements of a chosen type
- []    => var x [5]int = [5]{1,2,3,4,5}  //have to be the same length  ;  x := [...]{1, 2,3,4} // implies ... size as 4
- indices start at 0
- elements initialzied to zero value
- iterating:  for i, v range x {}   //similar as enumerate 

2. slices ( a "window" on an underlying array ) arr[1:3] => index 3 's stuff is not include 
- pointer indicates the start of the slice
- length is the number of eles in slice  len(sli)
- capacity is the max number of eles    cap(sli)
- sli := [] int{1,2,3}  // this doesn't have ... in [] , so compiler will think we want the slice, will create an array first, then it makes a slice point to the whole array

3. when you just want to have a slice ( the size is variable, don't want a fixed size, and you don't care about the underlying array)
can use make() to create it

    eg: sli = make([]int, 10)  //cap and len are both 10 in the example

    eg: sli = make([]int, 10, 15)  //cap 15 and len 10 

- append()   sli = make([]int, 0, 3)   sli = append(sli, 100);it will increase the array size if necessary; time penalty of course


4. map 

   eg: var idMap map[string][int]// [key type][val type]
       
       idMap = make(map[string][int])
       
   eg: idMap := map[string]int{"joe":123}
     
- access: idMap["joe"]
- add/update a pair:  idMap["joe"] = 456
- delete(idMap, "joe")
- id, p := idMap["joe"] // id is value, p is whether joe is in the map
- len(map)
- iterate for key,val := range idMap{ fmt.Println(key,val) }

5. structs

    ```
      type struct Person {
        name string
        addr string
        phone string
       }
      var p1 Person
      p1.name = "Kai"
     ```
      
 - initialize fileds to zero:  p1 := new(Person)
 - initialzie: p1 := Person(name: "j", addr:"x.st", phone:"123")

