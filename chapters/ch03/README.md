# Chapter 03 - Hello To The Web World


## Goal

Create a simple web server that responds "Hello World"


## Let's Start

Refer to the template in chapter 01 for the code and fill in and can compare with the completed code at the end.

### Package Name
There's a special package name that indicates this is the entry point to a runnable program vs a library. It's called `main`. Let's use that.

### Imports
Out of the box, Go has a rich set of libraries. For a web server, just import the `"net/http"` package.
Similarly to chapter 02, we will need to write text out, so we will need `"fmt"`.

### Code

#### Functions
##### SayHello()
Let's re-use the `SayHello()` from chapter 02.

```go
func SayHello() string {
	return "Hello World"
}
```

#### Route Handler
We want the server to respond "Hello World" when a user hits the index route "/".
If you look up the docs for "net/http", you would see there's a `HandleFunc(pattern string, handler func(ResponseWriter, *Request))` function. We can make the `pattern` equal to `"/"`. However, `SayHello() string` does not meet the function type needed for the second parameter. We need to write a second function that meets that prototype.

```go
func rootHandler(w http.ResponseWriter, req *http.Request) {
	fmt.Fprintln(w, SayHello())	
}
```

`http.ResponseWriter` is a writer that will write to a given http response. We use `Fprintln` to use that writer and write our "Hello World" to it, which is the response.

#### main()
Let's have main setup the server.

```go
func main() {
	http.HandleFunc("/", rootHandler)
	http.ListenAndServe(":8080", nil)
}
```

### Execution

`$ go run ch03.go`

### Full Code
```go
package main

func SayHello() string {
	return "Hello World"
}

func rootHandler(w http.ResponseWriter, req *http.Request) {
	fmt.Fprintln(w, SayHello())	
}

func main() {
	http.HandleFunc("/", rootHandler)
	http.ListenAndServe(":8080", nil)
}

```
