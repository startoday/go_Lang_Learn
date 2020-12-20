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



  
