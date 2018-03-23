# Backend programming for Non-Engineers

In this course,
we are going to write a little Go-based service.
No previous programming knowledge is needed.

This course takes about 15 minutes when speeding through it.
Please take time to understand what you are doing
and ask a lot of questions!


## Requirements

- a laptop with internet access


## Setting up Pairforce

If you have Go installed on your computer, skip this chapter and code away!
If not, don't worry, we will develop software on a cloud server from pairforce.io.
Pairforce is a platform that allows remote pair programming.
In this session, we use their cloud offering.

- go to [pairforce.io](https://pairforce.io)
- sign up (with email or Github account)
- click on "dashboard"
- click "start session"
- wait until the cloud server has started


## Intro to Go

Go is a modern language for building backend services.
It is optimized for engineering in the large -
large teams working over long periods of time on large code bases solving big problems.
More information at https://github.com/Originate/guide/tree/master/go.


## Step 1 - a hello world program

The first step in every programmer journey is a "hello world" program.
It is the simplest possible program.
All it does is print "hello world".

Go to the browser tab that shows the PairForce window.
The left side shows a file tree and an editor window to edit the content of files on the cloud server.
The right side shows a terminal for that cloud server.
This is a Linux system, so we are going to use Linux commands.

<a textrun="create-file">
Paste the code below into the text editor on the left:

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello world!")
}
```
Then click the "save" icon in the bottom of the editor, enter __hello.go__ as the file name,
and click the "save" button.

</a>

Let's look what this Go program does.

- `package main` tells Go that this is the main file in our program
- `import "fmt"` imports (loads) another package (code library) called `fmt`. This library allows Go programs to print text in the terminal it is running in
- `func main()` defines a function with the name `main`. This is how you tell Go which code to run. When starting a Go program, Go automatically runs the `main` function from the `main` package.
- inside the `main` function, we call the `Println` function from the `fmt` package with the arguments `"Hello world!"`.

<a textrun="run-console-command">
Let's see what this `Println` function does.
Run this command in the terminal to the right of the text editor window in the browser:

```
go run hello.go
```
</a>

It prints:
<a textrun="verify-run-console-command-output">

```
Hello world!
```
</a>


## Step 2 - a simple calculator

Programs can do more than just return text.
They can calculate things.
Let's build a little calculator in Go.
<a textrun="create-file">
Create a file __calc.go__ with the content:

```go
package main

import "fmt"

func main() {
	fmt.Println(1 + 1)
}
```
</a>

<a textrun="run-console-command">
Run it in the terminal:

```
go run calc.go
```
</a>

<a textrun="verify-run-console-command-output">
It prints the correct result:


```
2
```
</a>

Play with more complex formulas to get a feeling for how easy it.
The [math](https://golang.org/pkg/math) package of Go provides many mathematical functions.
Here is a slighly more complex example program:
<a textrun="verify-go-code-runs">

```go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println(math.Sqrt(10000000 / 42 * 13.4))
}
```
</a>



## Step 3 - a simple API server

Go was invented just a few years ago, in the internet age.
It has all the functionality needed to create network servers built in.

An API server is a web server that returns data in a machine-readable format.
In contrast, a web server returns data in a human-readable format.
First, we are going to create a simple API server.

<a textrun="create-file">

Create a file **api-server.go** with the content:

```go
package main

import (
	"fmt"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintf(w, "hello world!")
}

func main() {
	http.HandleFunc("/", handler)
	fmt.Println("API server online at http://localhost:8080")
	http.ListenAndServe(":8080", nil)
}
```
</a>

<a textrun="start-console-command">
Start the server by running:

```
go run api-server.go
```
</a>

<a textrun="wait-for-output">
You should see:

```
API server online at http://localhost:8080
```
</a>

Let's determine the address of the cloud server, so that we can look at the API.
Run this command in the terminal:

```
curl http://169.254.169.254/latest/meta-data/public-hostname/
```

It prints something that looks like:

```
ec2-52-53-223-49.us-west-1.compute.amazonaws.com
```

That's a website address under which your server is running.
Try it out by copy-and-pasting it into the URL field in a new browser tab.
**Append `:8080` to the end, without spaces.**
The address should look something like this (just with different numbers):

```
http://ec2-52-53-223-49.us-west-1.compute.amazonaws.com:8080
```

When you go to this address, you should see the text "hello world", which is exactly what our API returns.

<a textrun="stop-console-command">
When you are done, stop the server by hitting `Ctrl-C`.
</a>


## Step 4 - a web server

Right now our server is just a small API that returns a greeting.
Let's make it return a real web page.
Since we will do a lot of changes, and don't want to mess around in the server's source code each time,
we'll create a simple static file server.
For each request, it reads the file "index.html" and returns its content to the browser.
<a textrun="create-file">
Create a file __web-server.go__


```go
package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
	content, err := ioutil.ReadFile("index.html")
	if err != nil {
		log.Fatal(err)
	}
	fmt.Fprintf(w, "%s", content)
}

func main() {
	http.HandleFunc("/", handler)
	fmt.Println("server online at http://localhost:8080")
	http.ListenAndServe(":8080", nil)
}
```
</a>

Let's create another file by clicking on the `+` next to the tab of the editor that shows the filename.
<a textrun="create-file">
Paste this content:

```html
<html>
  <body>
    <h1>Hello World!</h1>
    It feels good to be online!
  </body>
</html>
```

Save the file and name it __index.html__.
</a>

<a textrun="start-console-command">
Start the server by running:

```
go run web-server.go
```
</a>

and make sure it starts up properly and says

<a textrun="wait-for-output">

```
server online at http://localhost:8080
```
</a>

You see a web page saying

```
Hello World!
```

You can modify the content of the file `index.html`
to make your webserver show different things.

<a textrun="create-file">
For example, update the content of the file __index.html__ to this one:

```html
<html>
  <head>
    <link rel="stylesheet"
          href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css">
  </head>
  <body>
    <div class="container">
      <div class="jumbotron">
        <h1 class="display-4">Hello, world!</h1>
        <p class="lead">
          Now this looks more like a real webpage!
        </p>
        <hr class="my-4">
        <p>
          We are using the famous Bootstrap theme originally developed at Twitter here.
        </p>
      </div>
    </div>
  </body>
</html>
```
</a>


<a textrun="stop-console-command">
When you are done, hit `Ctrl-C` to stop the server.
</a>

In the next session about front-end development,
we are going to populate this website with content and make it look polished.
