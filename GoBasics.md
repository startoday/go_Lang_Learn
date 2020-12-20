1. Why Go?
- code runs fast 
- Garbage collection (it has! usually for language as fast as go, They DON'T!)
- simpler objects (simpler OOD)

2. Compiled code vs inteperated code
- Compiled code is fast
- Interpreters makes coding easier (mange memory automatically(interpreter handles that; compiled language, you need to de-locate those memories) ; infer variable types)

Go is a compile language but has some good things of inteperate language, for example, garbage collection

3. go tools
- go build: compiles the porgram, create the executable files
- go doc: print docs for a package
- go fmt: formats source code files! (spotless!!!)
- go get: download packages and install them 
- go list: list all installed packages
- go run: compiles .go files and runs the executable
- go test: run tests using files ending in _test.go

4. variables
- names must start with a letter, can be numbers, letters and underscores; case sensitive, can't use keywords
- variable must have a name and a type (declaration) eg: var x,y int
- type declaration: defining an alias for a type; eg: type Celsius float64   ; type IDnum int
- initialization : 
  
  var x = 100  ;
  
  var x int = 100; 

  var x int
  
  x = 100
  
- uninitialized vars have a zero val:  var x int // x = 0 ; var x string // x = ""
- short var declaration:  x := 100   ":=" operator   => can only do this inside a function

5. pointer:
    - & operator returns the address of a var/function 
    - “ * ”   operator returns data at an address(dereferencing)
    - eg: 
    ```
          var x int = 1 
          var y int 
          var ip * int // ip is an int pointer
          ip = &x // ip now points to x
          y = * ip  // y is now 1
    ```
    - new() return a pointer to the var that created
    ```
          ptr := new(int)
          *ptr = 3  // set the value as 3
    ```

6. variable scope
- blocks: {} / universe block -all Go source  / Package block - all source in a package/ File block -all source in a file

7. int8, int16, int32,uint8,uint16...你可以specify size 但也可以交给compiler解决by just use int！

8. binary operations need operands of the same type
  ```
   var x int32 = 1
   var y int16 = 1
   x = y // will fail!! compiler consider them as two different types

   // needs to do type conversion
   x= int32(y) //will work
   ```
9. floats
- float32 :  ~ 6 digits of percision
- float64 :  ~ 15 digits of percision
- complex numbers represented as two floats: real and imaginary => eg : var z complex128 = complex(2,3) => 2+3i
 
10. code points - unicode characters

Rune - a code points in Go

String is read only in Go, with double quotes; each byte is a rune

ToUpper(r rune)
ToUpper(s)

11. const: Expression whose value is known at compile time

const x = 1.3

12. iota: similar as enum (want consts different from each other)
- Each constant is assigned to a unique integer
- starts at 1 an increments

- eg:
  ```
    type Grades int
    const (
      A Grades = iota
      B   //no need to specify iota again!!
      C
      D
      F
    )
  ```
 
13. control flow
- eg : for <init>; <cond>;<update> { <stmts> }   ; i = 0 for i < 10 { fmt.Printf("hi")  i++}
- switch ( a multiway if statements) => no "break" needed for each case!!! no cascading!!!
  
  
14. scan
- Scan reads user input
- Takes a pointer as an argument
- Typed data is written to pointer

15. RFCs (requests for comments| remote function calls)
- protocals such as HTTP, URI, you can just import pacakges to use 

16. JSON
- turn some other object into Json called JSON marshalling
   
   barr, err :=json.Marshal(p1) //p1 is a Person struct; barr is a []byte
   
   err := json.Unmarshal(barr, &p2) // var p2 Person 
   
   
17. Files
- ioutil packag: readfile will read the whole things, so it is not good to read a large file
- os package: os.open() os.close() 
