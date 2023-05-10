# Wiki: Go Bootcamp: Master Golang with 1000+ Exercises and Projects

The complete bootcamp course

## Creating a new go project


	$ go mod init github.com/cariza/dnsproxy
	
	$ go mod tidy
	

## Getting started

Get repos with go get:

	$ go get -u -d github.com/inancgumus/learngo/...

This is all stored in the directory specified in your go path:

	$ echo $GOPATH
	$ ls $GOPATH
	$ ls $GOPATH/src
	$ ls $GOPATH/src/github.com

You will see a directory "inancgumus". 

Open in go:

	$ code $GOPATH/src/github.com/inancgumus/learngo

To create go projects:

- Understand $GOPATH to know where to put source code
- Create folders and files & your main.go file
- Code - add the code that you want to run

$GOPATH
Your workspace
All go code (yours or third party) will be in this folder

	$ go env GOPATH

The folders in the $GOPATH folder:

- src - go source files
    - folder structure for your go code: $GOPATH/src/github.com/user-or-org/project/program/main.go
	- all your executable files go in a directory under $GOPATH/src

To get started with your own project, either create your own folder in the $GOPATH/src folder, or if you have a github account, use the github folder:

	$ mkdir src/github.com/cariza
	$ mkdir src/github.com/cariza/learngo
	$ mkdir src/github.com/cariza/learngo/first


Your first program:

```
// should always provide a package name
package main

import "fmt"

// entry point to go programs
func main() {
    // fmt is a standard library
    fmt.Println("Hello Gopher!")
}
```

### Running and compiling

Running & Compiling:

	$ go build
	$ go run

go build
compiles your go program
Will create an actual executable file (eg "first")

	$ go build
	$ ./first

first being the folder that has your main.go file

    $ go run

Does not create an executable file

But does compile and run the go code 

Great for prototyping

file

Useful tool to check if a file is executable:

	$ file name-of-file
	$ file first
	> first: Mach-O 64-bit executable x86_64


Compile-Time & Runtime:

- Compiling - producing machine readable code for machines to read - requires to be executed in order to do what it was coded to do
- Compile-Time
- Runtime - When the compiled code is actually run - it starts to communicate with memory and cpu

Helper command:

	$ go run -x main.go

This shows how the linker combines the package files with your code.


Compiling go code for different environments:

Create an OS X executable:GOOS=darwin GOARCH=386 go build
Create a Windows executable:GOOS=windows GOARCH=386 go build
Create a Linux executable:GOOS=linux GOARCH=arm GOARM=7 go build

https://golang.org/doc/install/source#environment

### Useful Refs

Go Packages:

https://golang.org/pkg/

Tour:

https://tour.golang.org/


Format your go code:

    gofmt tool

Standalone go tour, you can download and run offline:

	$ go get golang.org/x/tour

Check your workspace's bin directory.

Learn more about the go playground:
https://blog.golang.org/playground

### Starting the tour notes

Starting the tour:
https://tour.golang.org/basics/1

17 parts:

Packages
- Note: The environment in which these programs are executed is deterministic, so each time you run the example program rand.Intn will return the same number. 

Imports
- good style to use "factored" import statement

eg
```
import (
	"fmt"
	"math"
)
```

Exported names
- When importing a package, you can refer only to its exported (capitalised) names. Any "unexported" names are not accessible from outside the package. 
    - eg math.Pi

Functions
- arguments: type comes after the variable name
    - eg func add(x int, y int) int {
- arguments can be shortened: 
    - x int, y int 
    - to 
    - x, y int
- Also note: you defined the input and the output variables and their types
- eg func split(sum int) (x, y int) {

Multiple results
- a, b := swap("hello", "world")
- see full example below

Named return values
- return values may be named (best practice - for readability)
- if not named then called a "naked" return

Variables
- var
- type is last
- eg: var c, python, java bool

Variables with initializers
- var i, j int = 1, 2
- note if an initializer is present the type can be left out

Short variable declarations:
- instead of using var:
    - k := 3
- for inside functions, doesn't work outside of functions

Zero values
- 0 for numeric types,
- false for the boolean type, and
- "" (the empty string) for strings.

Type conversions
- var i int = 42
- var f float64 = float64(i)

Type inference
- k := 3

Constants
- const Pi = 3.14
- cannot be declared using the := syntax

Numeric constants
- high-precision values
```
const (
	// Create a huge number by shifting a 1 bit left 100 places.
	// In other words, the binary number that is 1 followed by 100 zeroes.
	Big = 1 << 100
	// Shift it right again 99 places, so we end up with 1<<1, or 2.
	Small = Big >> 99
)
```




Example for Multiple results

```
package main

import "fmt"

func swap(x, y string) (string, string) {
	return y, x
}

func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}
```

Format cheatsheet:

https://yourbasic.org/golang/fmt-printf-reference-cheat-sheet/

Default formats and type

    * Value: []int64{0, 1}

| Format	| Verb	| Description | 
| :-------- | :---- | :---------- |
| [0 1]	    | %v	| Default format |
| []int64{0, 1}	| %#v	| Go-syntax format |
| []int64	| %T	| The type of the value |


Syntax:

fmt.Printf(<format identifier / verbs>, <replacer value/s..,.,.,.,.,>}

Escape Sequences 
	
    eg \n


Packages

- You can give your packages any name, but in order to make it executable you need the package main 
- Only one package clause per file
- Multiple files can belong to the same package (package main in each file)
- A package contains a lot of go files that are in the same directory
- Only one file in a package can have the main function

Commands:

	$ go run .

or this:

	$ go run *.go

or this:

	$ go run main.go hey.go bye.go

### Executable packages vs Library packages

Executable packages
- use the package main naming
- have a main function
- created for running
- can't import
- name should be package main
- has to have a function called main

Library Packages
- not executable, can only be imported into executable packages
- created for reusability
-  importable
- libraries can be imported in other library packages or executable packages
- can have any name
- does not have to have a function called main

### Scopes

Normal variables scopes

Lingo:
- Visibility
- Declarations

File scoped 
- import

Package scoped
- functions can be shared across a package (provided the files belong to the same package)
- you cannot have multiple functions with the same names in the same package (this includes package scoped variables)

Block Scoped
- inside a function / code block

Importing 
- imports are available on the file scope (not package scope)

Renaming imports:
- import newname "package"


Statements:
- statements control the execution flow
- control statements like if
- ; semicolons allow you to put multiple statements in the same line
- Go adds semicolons between statements behind the scenes

Expressions
- computes one or multiple values
- expressions should be use with or within a statement
- eg: fmt.Println("Hello!" + "!")

Comments
- //
- /* ... */

Generate documentation from the libraries:

eg Println

	$ go doc -src fmt Println


Examples for reference:

https://github.com/inancgumus/learngo/blob/master/04-statements-expressions-comments/exercises/01-shy-semicolons/solution/main.go

https://github.com/inancgumus/learngo/blob/master/04-statements-expressions-comments/exercises/02-naked-expression/solution/main.go

https://github.com/inancgumus/learngo/blob/master/04-statements-expressions-comments/exercises/03-operators-combine/solution/main.go

https://github.com/inancgumus/learngo/blob/master/04-statements-expressions-comments/exercises/04-print-go-version/solution/main.go

https://github.com/inancgumus/learngo/blob/master/04-statements-expressions-comments/exercises/05-comment-out/solution/main.go

https://github.com/inancgumus/learngo/blob/master/04-statements-expressions-comments/exercises/06-use-godoc/solution/solution.md


### Create your own package

An example:
	https://github.com/inancgumus/learngo/tree/master/first/printer

First library package:

Create a folder:

	$ mkdir printer

Add a *.go file:

	$ touch printer.go

Code:

// It's a good practice to name your package the same as your folder

    package printer

Note:

You cannot run this package. It is not an executable package, but rather a library package.

Install the package:

	$ go install
	$ ls $GOPATH/pkg/darwin_amd64/

You will see your new library package installed there

Exporting:
Allow a package to make it's functionalities available to other packages

Step 1:

to export a name, make the first letter uppercase

Example source code:
https://golang.org/src/errors/errors.go
- see the uppercases
    - New
    - Error

Creating executables:

Create a cmd folder (inside your package folder):

	$ mkdir cmd

Add a main.go file:

	$ touch cmd/main.go

Add code:

package main

import "github.com/..../printer"

func main() {
	printer.Hello()
}

Your printer code:

package printer

import "fmt"

func Hello() {
	fmt.Println("Hello)
}


---------

## Part 2

----------


### Go Data Types

Go is a statically typed language. 

Basic Data Types

- int
- float64 - has a fractional part - non exact numbers (negative and positive)
- bool
- string


### Declarations

Naming internal variables - should always start with a lowercase letter or underscore

Naming exported variables - should start with a capital letter

Cant use ! in variable names

Order of statements matter, you must declare your variable before using it

Zero values - every go type has a zero value (like a default uninitialized value).

	booleans - false
 	numerics - 0
	strings - ""
	pointers - nill

Note:

Unused variable errors only happen for block scoped variables.

Blank Identifier _

Allows you to create a variable that is blank

You can declare multi line variables:

```
var (
	speed 	int
	heat 	float64
	off 		bool
	brand 	string
)
```

Or parallel declaration:

var speed, velocity int


Note:
In go, the variables are case sensitive, myvariable and MyVariable are different variables.


Type inference:
- go can figure out a variables type by the initiliased value
- eg var safe = true or safe := true (bool type)

Short declaration:
Using :=
	save := true

2 declarations:
- Declaration vs Short Declaration 

Why can't you use short declaration with package scope:
- you can only use the full var declaration for package scope
- why - because on the package level all statements need to start with a keyword (eg var - the short declaration does not start with a keyword)

Declaring multiple value with short declaration style:

	safe, speed := true, 50

Redeclaration:

Short declaration can also be used to reassign values to an existing variable, only if it's part of an initialized statement:

	name := "Nikola"
	name, age := "Marie", 33

When to use normal declaration vs short declaration:
- normal declaration:
    - var variable = value
	- or if you dont know value:
	- var variable type
    - When you don't know the initial value of the variable - easier to read. 
    - When you need a packaged scope variable.
    - When you want to group variables together for readability

- short declaration
    - if you know the initial value of a variable
    - to keep code concise
    - for redeclaration
	
Shadowing
- When variables of the same names end up in nested scopes
- https://rpeshkov.net/blog/golang-variable-shadowing/

Detect shadowing

- Variable shadowing can be detected by vet command from Go. 

Call it this way:

    go tool vet --shadow file.go

When you run this command, you’ll see shadowing issues in the file you’ve provided.

Example:

    main.go:14: declaration of "err" shadows declaration at main.go:13

### Assignment 

Operators
- =, -, +,

Note: in go you can assign your own operators


Multiple assignment:

...
import ( "fmt"; "time")
...

	speed, now = 100, time.Now()
	fmt.Println(speed, now)


Swapping variables:

using multiple assignment

	speed, prevSpeed = prevSpeed, speed


Example: path seperator
- using path library

    func Split(path string) (dir, file string)

syntax:
- func FuncName(args types) (responses types)

```
import ( "fmt"; "path" )

func main() {
	var dir, file string
	dir, file := path.Split("css/main.css")
	fmt.Println("file:", file)
}
```

or rather, for conciseness you can write:

```
func main() {
	_, file := path.Split("css/main.css")
	fmt.Println("file:", file)
}
```

Type Conversion

	type(value)

- changes the type of a given value into this type
- does not change the original value, just outputs the converted value

Example: 

This will error:

	speed := 100
	force := 2.5
	speed = speed * force

solution:

	speed = speed * int(force)

In this case though the conversion dropped the 0.5 amount, and we don't gt an accurate value
- called: destructive operation

better solution:

	speed = int( float64(speed) * force) )

another example of type converstion:

	string([]byte{104, 105})
	> hi
	// numbers convert to letters when converted

### Terminal args

Input from terminal:

use "os" package
- os speaks to the operating system
- os will help us get the user input


Intro to slices:

	var Args []string
	this stores a slice of strings

A slice can store multiple values
- each value in a slice is an unnamed variable
- you can use index expressions
    - Args[0]    Args[1]    Args[2]
	- Args[0] stores a path to the running program

Testing Args:

```
import (
	"fmt"
	"os"
)

func main() {
	fmt.Printf("%#v\n", os.Args);
}
```

	$ go run main.go

	$ go build -o greeter

	$ go run main.go
	// it will now output the executable path as ./greeter
	

len

	$ len(os.Args)

Pass arguments to the command by just adding them to the command:

	$ go run main.go one two three

func main() {
    fmt.Println("%#v\n", os.Args)
    fmt.Println(os.Args[0])
    fmt.Println(len(os.Args))
    fmt.Println(os.Args[1])
    fmt.Println(os.Args[2])
    fmt.Println(os.Args[3])
}

### Printf

fmt.Printf()

Allows you to format text

	text := "test text"
	fmt.Printf("%q\n", text)
	fmt.Printf("%s\n", text)

You can use multiple vers with printf (%q being the verb)

%v any value, not type specific
%d an integer
%T the type of the variable 
%s string
%t for bool
%f for float - you can add precision
	- %.2f - for 2 decimal points

multi verbs:

	fmt.Printf("total: %d success: %d / %d \n", total, ok, failed)

escape sequences:

	\n

Argument indexing

	using printf to reference passed values:

	fmt.Printf("%v is %v away. Think! %[2]v kms \n",
		planet, distance)


Copy lines:

    command + shift + d


Note on numbers:

go does type conversion so when you do something like this:

	var ratio float64 = 3 / 2
	go is actually doing this under the hood:
	ratio = float64(int(3) / int(2))
	and returns "1"
	to get an accurate number one of the values needs to be a float
	var ratio float64 = float64(3) / 2
	returns 1.5
	or
	var ratio float64 = 3.0 / 2
	returns 1.5



Operator precedence:

	parentheses
	multiplication operators (*, /)
	addition ( + , - )
	https://golang.org/ref/spec#Operator_precedence

incdec statement

	n++
	n--

note: incdec is a statement not an operator:

	you cant do this: 5 + n++

You can use:

	+=
	-=
	*=
	/=

package

	strconv
	for converting strings to other types

eg

	feet, _ := strconv.ParseFloat(arg, 64)
		docs: ParseFloat func(s string, bitSize int) (float64, error)
	meters := feet * 0.3048
	fmt.Printf("%g feet is %g meters. /n", feet, meters)

Celsius to farenheit conversion:

	20c * 1.8 + 32 = 68f

Reminder:

float values are innacurate 
    dont compare float values for equality

using a float and a int in an expression, the value is converted to float

    value = 2 + 3.0


String literals

string literal "hi there"

raw string literal 'hi there'

raw string literals can also be multi lined

```
'hi
there'
```

Reasons so use raw string literals:
- using multi line strings
- don't have to escape quotes of backslashes
	
String Concatenation:

	name, last := "carl", "sagan"
	name += " edward"

	"hello" + ", " + "how" + " " + "are you" + "?"

when combining strings and integers you can't just use +

	eg + strconv.Itoa(sum)

Note: use strconv.Itoa to convert ints to strings for concatenating

	(itoa but caps i -> I - not L)

Another useful function: 

    strconv.FormatBool

len

	len(stringvalue)

returns how many bytes in a string, not how many characters (for non english characters it will return different results. Non english characters need more bytes

Length of characters

use:

    import "unicode/utf8"
    func main() {
        utf8.RuneCountInString(name)
    }

Strings library:

https://golang.org/pkg/strings/#ToUpper

	strings.Repeat
	strings.ToUpper

Libraries worth noting:

	strconv
	strings
	unicode/utf8


Why have typed systems?

- goal: prevent bugs as early as possible

Predeclared Types

	Built in types in the programming language
	Core feature in the language

Signed types

	positive and negative values = -1 or 1
	eg int

int32 - also called "rune"

Unsigned types:

	uint
	only positive numbers (not negative)

Some examples of predeclared types:

	bool
	string
	int
	int8
	int16
	int32 - also called rune
	int64
	uint
	uint8 - also called byte
	uint16
	uint32
	uint64
	float32
	float64
	complex64
	complet128


Defined types (also called named type)

- you can create a defined type from an existing type called an underlying type
- you can also give the defined type it's own methods (or no methods at all)

eg

	type Duration int64

Note: A defined type is not the same type as it's underlying type, it is considered a new different type
- but you can convert a value
    - eg
		type Duration int64
		var ms int64 = 1000
		var ns Duration
		ns = Duration(ms)
	- BUT also note they have to have the same underlying type (eg int64(


Why do we need Defined Types?
- being able to attach methods
- methods can only be declared at the package scope
- methods are just like functions

	eg
	func(d Duration) Hours() float64
	h, _ := time.ParseDuration("4h30m")
	h.Hours()


Defining a new type:

```
type gram float64
type ounce float64

func main() {
	var g gram = 1000
	var o ounce
	o = ounce(g) * 0.035274
	
	fomt.Printf("%g grams is %.2.f", o, g);
}
```

Note there is no type heirarchy in go:

	type Duration int64
	type MyDuration Duration

MyDuration still has an underlying type of int64 same as Duration

Note: Types created in packages are also different types, even if they share the same name as in the main function. 

	salt = Gram(weights.Gram(100))

Creating a local type from a package type:

	type myGram weights.Gram

Aliased Types

	byte = uint8
	they are the same

	type byte = uint8

	rune = int32
	type rune = int32


### Constants

	all basic literals are unnamed constants
	eg: 1, 3.14, "hello" true false etc

Declare a named constant

	const meters int = 100
	(in go constants dont need to be caps)

Constants can also help catch some errors at runtime before compiled (earlier detection)


Rules

    Learn the rules like a pro so you can break them like an artist

- you cant initialise a constant with a function (the only exception is the len function)
- variables belong to runtime (can't be used to assign to constants)


Declaring multiple constants

	const min, max int = 1, 1000
	(left should match right)

	const (
		min int = 1
		max int = 1
	)

Export constants

You can also export constants

Just make them start with a Capital letter like with variables

	const Meters int = 100


### Typeless constants
	
	const min = 1 + 1
	const pi = 3.14 * min
	// Normally this would error, but because they're untyped constants this works.

When the constant is assigned a literal without explicitly being given a type to be, it remains typeless. Constants just get assigned the literal value

untyped constants are like chameleons, can be used where needed (int float64 rune etc)


### Default types

Every basic literal has a default type, if no type provided then it goes to the literal's default type

Type conversion

	Go only converts when the type is needed
	Typeless variables will for example remain typeless, and get converted as needed
	i := 5 + 3.5
	i becomes a float64 but is still typeless
	But, you still need to use compatible types with each other
	This will error: f := true + "string"
	bool and string even as typeless are incompatible

Why define types and not stay typeless?
- declare methods (caan only declare methods on a defined type)
- type safety

Go does implicit conversion of types:

These const inherit types because its needed by the way we declared them:

![Variable types](./images/1.%20Nanosecond%20Duration.jpg)

math.Round

	rounding float values
	math.Round(3.333)

iota

iota is a number generator for constants, a built-on constant generator

	const (
		monday = iota
		tuesday
		wednesday
		thursday
		friday
		saturday
		sunday
	)

Note: iota is used with constants

Blank identifier _

Using blank identifiers with variables

EST -5
MST -7
PST -8 

notice that this sequence has a gap in it (no -6)
the blank identifier indicates skipping that value

	const (
		EST = -(5 + iota)
		_
		MST
		PST
	)

Recap for iota:

	iota is a constant generator
	blank identifier can help skip


### Naming conventions

idiomatic

often use letters rather than full variable names (unlike python)

Some common abbreviations and names used in Go

```
var s string
var i int
var num int
var msg string
var v string
var val string
var fv string // flag value
var err error
var args []string
var seen bool
var parsed bool
var buf []byte
var off int //offset
var op int // operation
var opRead int
var l int
var n int
var m int
var c int
var a int // array
var r rune
var sep string // seperator
var src int
var dst int
var b byte
var b []byte
var buf []byte
var w io.Writer
var r io.Reader
var pos int
```

Tips:

- Use the first few letters of the word
- Use fewer letters in smaller scopes
- Use the complete words for larger scopes
- Use mixedCaps
- Use all capitals for common acronyms eg API
- Dont stutter eg player.PlayerScore, rather player.score
- Dont use _ no underscores (it's a no no)

Operators:

Comparison & Ordering operators & Logical operators

Ordering operators:

	> 
	<

Logical Operators:

	&&
	||
	!

Comparison Operators

Compare 2 values

	>, <, ==, != 

Same as other programming languages

You can compare strings as well, because strings are actually numbers

	"abc" > "cde"

Comparison operators always create a bool value

	fast := speed >= 80

Comparison and assignment

a tip: 

    you can't compare what you can't assign

- eg dont compare a string with an int
- var speed int
- speed == "100" 
- because you wouldn't be able to: speed = "100" you'd get a type error
- but you can compare them by converting the to the same types
- inval == int(floatval) 

Logical operators

	can only work with bool values or bool expressions
	AND - &&
	OR - ||
	NOT -  !
		- !(...)

Go short circuits and doesnt check both values if the first one is false it's irrelevant what the second one is 

### If

If statements:

	if (score > 3) {
		...
	}

	BUT you cn also write like this:

	if score > 3 {
		...
	}

In go if statements only work with bools. Bool expression or bool value.

Note the above ^ only bool statements- condition expression

Else:

	if score > 3 && valid {
		...
	} else if score == x {
		...
	} else {
		...
	}

Convert string to int:

	strconv.Atoi(os.Args[1])

Convert int to string:

	strconv.Itoa(os.Args[1])

Some example code:

    package main

    import (
        "fmt"
        "os"
    )

    func validArgs() bool {
        if len(os.Args) < 3 {
            return false
        }
        return true
    }

    func main() {

        user, pass, ouser, opass := "jack", "1888", "inanc", "1879"

        const (
            usage   = "Usage: [username] [password]"
            access  = "Access granted to \"%q\""
            invalid = "Invalid password for \"%q\""
            denied  = "Access denied for \"%q\""
        )

        if !validArgs() {
            fmt.Printf(usage)
            return
        }

        u, p := os.Args[1], os.Args[2]

        if u != user && u != ouser {
            fmt.Printf("Access denied for \"%s\" \n", u)
        } else if u == user && p == pass {
            fmt.Printf("Access granted to \"%s\" \n", u)
        } else if u == ouser && p == opass {
            fmt.Printf("Access granted to \"%s\" \n", u)
        } else {
            fmt.Printf("Invalid password for \"%s\" \n", u)
        }
    }



Error Handling

    nil

no value

nil is the zero value for pointer-based types

go doesnt have throw catch

error value
- more readable and less bugs that normally occur with throw catch statements


strconv.Itoa -> never fails
- int to ascii

strconv.Atoi -> can fail 
- ascii to int
- func Atoi(s string) (int, error)

Example

    func main() {

        n, err := strconv.Atoi(os.Args[1])
        
        fmt.Println("Converted number :", n)
        fmt.Println("Returned error value:", err)
    }

Run:

    go run main.go 42
    go run main.go string

Add error statement:

    n, err := strconv.Atoi(age)
    if err != nil {
        fmt.Println("ERROR:", err)
        return
    }
    fmt.Printf("SUCCESS: Converted %q to %d \n", age, n)

Simple statements 

for multi if

Short if statement (using simple statements):

	n, err := strconv.Atoi("42")

	if err == nil {
		fmt.Println("There was no error
	}

Can also be written as:

	if n, err := strvonc.Atoi("42"); err == nil {
		fmt.Println("There was no error, n is", n)
	}

(A bit ike javascript's for loop, but with an if statement)


Example of using short if statements with if else 

- also notice the scope of variables stay within the main if statement:

```
if a := os.Args; len(a) != 2 {
    fmt.Printf("Give me a number")
} else if n, err := strconv.Atoi(a[1]); err != nil {
    fmt.Printf("An error occured, %q", err)
} else {
    fmt.Printf("%s * 2 %d\n", a[1], n*2)
}
```

Shadowing
- common problem in go
```
var int n

if ...

} else if  n, err := strvonv.Atoi(os.Args[1]); err != nil {
... n becomes shadow
```

n in the if statement is shadowing the main scope's n variable
- this happens also with the the use of := which can create a new value or assign to an existing value


To fix use = instead of := 

	var (
		n int
		err error
	)

	if...	

	} else if n, err = strvonv.Atoi(os.Args[1]); err != nil {
	...

Now you won't get the shadowing that you got before when using the := 

To tell xcode to help detect shadowing:

![Commad Palette](./images/2.%20ction%20View%20Go%20Debug%20Terminal%20Window.jpg)

![Settings](./images/3.%20Preferences%20Open%20Settings%20(JSON).jpg)

![More settings](./images/4.%20ser%20Settings.jpg)

```
"go.lintOnSave": "package",
"go.vetOnSave": "package",
"go.vetFlags": [
	"-all",
	"-shadow"
]
```

Summary:

![Simple statement](./images/5.%20simple%20statement.jpg)

![Scopes](./images/6.%20scopes.jpg)

![Shadowing gotcha](./images/7.%20shadowing%20gotcha.jpg)

### Switch

2 Types of switch:
	Expression switch
	Type Switch

Switch condition will be compared for each case condition
- types need to match
- type of switch condition needs to match type of case

condition expression (eg switch xxxx)
- the switch condition determines the type of the case conditions

Example

	var city := "Paris"
	switch city {
		case "Paris":
			fmt.Println("France)
	}

Break statements:

Note: you dont need break statements - go adds them automatically
- break not needed

Case clause
- has the case condition
- has it's own scope


Default clause:

	var city := "Paris"
	switch city {
		case "Paris":
			fmt.Println("France)
		default:
			fmt.Println("Where?")
	}
There can only be 1 default clause


Multiple values in case clause:
- similar to logical or ||
```
	var city := "Paris"
	switch city {
		case "Paris", "Lyon":
			fmt.Println("France)
		default:
			fmt.Println("Where?")
	}
```

Switch with bool expressions:

	i := 10

	switch {
		case i > 0:
			fmt.Println("positive")
		case i < 0:
			fmt.Printl("negative")
		default:
			fmt.Println("zero")
	}


Fallthrough statement

fallthrough statements should be the last statement in a case block (if you want to use them)


	i := 142

	switch {
		case i > 100:
			fmt.Println("big positive number")
			fallthrough
		case i > 0:
			fmt.Printl("positive number")
			fallthrough
		default:
			fmt.Println("number")
	}

Go is different to other languages, instead of having break statements, it has fallthrough statements, you have to explicitly tell it to have fallthrough behaviour rather than it existing by default.

Short switch statement:

	i := 10

	switch {
		case i > 0:
			fmt.Println("positive")
		case i < 0:
			fmt.Printl("negative")
		default:
			fmt.Println("zero")
	}

Can be rewrittern as:

	switch i := 10; true {
		case i > 0:
			fmt.Println("positive")
		case i < 0:
			fmt.Printl("negative")
		default:
			fmt.Println("zero")
	}

This can be shortened even more (remove true but keep ; semicoloon)

	switch i := 10; {
		case i > 0:
			fmt.Println("positive")
		case i < 0:
			fmt.Printl("negative")
		default:
			fmt.Println("zero")
	}

### time

time package

using the Hour function/method on time package

	func (t Time) Hour() int

Can then be used with time.Now() to get the Time type

	t := time.Now()
	t.Hour()

	Or:

	h := time.Now().Hour()

Switch shortened example:

    switch h := time.Now().Hour(); {
    case h < 12:
        fmt.Println("Morning")
    case h < 18:
        fmt.Println("Afternoon")
    default:
        fmt.Println("Evening")
    }

### If vs Switch

    switch m := os.Args[1]; m {
    case "January", "February", "March":
        fmt.Println("Summer")
    case "April", "May", "June":
        fmt.Printf("Autumn")
    case "July", "August", "September":
        fmt.Println("Winter")
    case "October", "November", "December":
        fmt.Println("Spring")
    default:
        fmt.Printf("Please provide a valid month")
    }



## Loops

In go there is only 1 loop, the for loop

![Loop syntax](./images/8.%20init%20statement.jpg)

For

	for i := 1; i <= 1000; i++ {
		sum += i
	}

syntax:

	for (init statement) (condition) (post statement / action) {
		...
	}

Break statement:

You can restructure the for loop in a few ways:

    for i += 1; i < 1000; i++ {

    }

// For loop with a preinitialised value

    var i := 1000

    for ; i < 1000; i++ {

    }

// For loop with a single statement

    var i := 1000

    for ; i < 1000; {
        i++
    }

// Infinite loop: - use break

    var i := 1000

    for {
        i++
    }

eg:

    for {
        if i > 5 {
            break
        }
        sum += i
        i++
    }

Continue statement

	continue

Breaks loop but not whole loop, just the current loop step

Use breakpoints in vscode
- behind the scenes the debugger uses a program called delve 


Example with continue and break:

    var i = 0

    for {
        if i > 5 {
            break
        }
        if i%2 == 0 {
            i++
            continue
        }
        fmt.Printf("%d \n", i)
        i++
    }

Nested Loops

Example:

    var (
        to  = 5
        err error
    )

    if len(os.Args) < 2 {
        fmt.Printf("Using default \"%d\"\n", to)
    } else if to, err = strconv.Atoi(os.Args[1]); err != nil {
        fmt.Println("Invalid arg %s", err)
        return
    }

    // ss := "%5s"
    sd := "%5d"

    // headers
    for i := 0; i < to+1; i++ {
        fmt.Printf(sd, i)
    }
    fmt.Println()

    for i := 0 + 1; i < to+1; i++ {
        fmt.Printf(sd, i)
        for in := 1; in < to+1; in++ {
            fmt.Printf(sd, in*i)
        }
        fmt.Println()
    }


This is a pretty nice example to also read through:

Maths table exercise:

https://github.com/inancgumus/learngo/blob/master/13-loops/exercises/07-multiplication-table-exercises/02-math-tables/solution/main.go


Remember: os.Args is just a slice of strings

var Args []string

Eg: string string string

Becomes:

| string 	| string 	| string |
| :--- | :--- | :--- |
| Args[0]	| Args[1]	| Args[2] |


	for i:= 1; i < len(os.Args); i++ {
		fmt.Printf("%q\n", os.Args[i])
	}

Using Field to split words:

Fields func(s string) [] string

    words := strings.Fields("one two three four")

    for j := 0; j < len(words); j++ {
        fmt.Printf("#%-2d: %q\n", j+1, words[j])
    }

SPACING TIPS

fmt.Printf spacing tips:

Space on the left of string/digit:

	fmt.Printf("#%2d: %q\n", j+1, words[j])

Space on the right of string/digit:

	fmt.Printf("#%-2d: %q\n", j+1, words[j])

Range:

Using a for range
- similar to python
- can be used to loop over slices, strings, maps, channels etc

```
	for i, v := range os.Args {
		if i == 0 {
			continue
		}
		fmt.Printf("%q\n", v)
	}
```

An even better approach:

```
for _, v := range os.Args[1:] {
    fmt.Printf("%q\n", v)
}
```

You can affect index of a slice in a range:

	Note: range os.Args[1:]


REFACTOR TIPS:

Convert/Refactor a for loop: 

	for j := 0; j < len(words); j++ {
		fmt.Printf("#%-2d: %q\n", j+1, words[j])
	}

Refactor to for range:

	for i, v := range words {
		fmt.Printf("#%-2d: %q\n", i+1, words[v])
	}


Another example:

	 words := strings.Fields("one two three four")

	 for j := 0; j < len(words); j++ {
	 	fmt.Printf("#%-2d: %q\n", j+1, words[j])
	 }

	 for i, v := range words {
	 	fmt.Printf("#%-2d: %q\n", i+1, v)
	 }

You can also just use for just the indexes:

	for i := range words {
		fmt.Println(i)
	}

You don't need to use: for i, _ := range ...

Another example with os.Args:

	for _, v := range os.Args[1:] {
		fmt.Printf("%s \n", v)
	}

Summary for loops:

![for loop](./images/9.%20for.jpg)

![for with break](./images/10.%20break.jpg)

![for with continue](./images/11.%20continue.jpg)

![nested for loops](./images/12.%20nested%20loops.jpg)

![for with range](./images/13.%20for%20range.jpg)

### Randomization

Package rand

Random numbers are generated by a source

Random types
- float
- int
- etc

```
	guess := 10
	func Intn (n int) int 
		rand.Intn(guess + 1)
```

### Seed 

Seed updates when you pass it a new number

	rand.Seed(num)

Seed it with time - it's constantly changing - unix time

    func (t Time) Unix() int

    func (t Time) UnixNano() int64

Example with Seed:

	rand.Seed(time.Now().UnixNano())
	
	quess := 10

	for n := 0; n != guess; {
		n = rand.Intn(guess + 1)
		fmt.Printf("%d ", n)
	}

Note:

strings.Fields

Break a string up into a list

	const corpus = "I am a list of words"
	words := strings.Fields(corpus)

Remember range:

You can use range to loop over a list of words	

	for _, q:= range words {

	}

Break

break - use break to exit a loop

Labeling

Labeled for loops to break a specific loop:
	
    const sentence = "a brown fox jumped over the cat again and again"

Break with label:

```
queries:
    for _, s := range os.Args[1:] {
        for i2, w := range strings.Fields(sentence) {
            if w == s {
                fmt.Printf("#%-3d %s \n", i2, w)
                break queries
            }
        }
    }
```

Continue with label:

```
query:
    for _, k := range keywords {
        for i, w := range words {
            if k == w {
                fmt.Printf("#%-3d %s \n", i, w)
                continue query
            }
        }
    }
}
```

Another example:

![labeling examples](./images/14.%20queries.jpg)

![label example](./images/15.%20range%20query%20%7B.jpg)

Using GoTo:

Jumping from almost anywhere inside a function
- not only for loops 

Loop with Goto:

Using an if:

```
loop: 
	if i < 3 {
		i++
		goto loop
	}
```

Note: Goto can be very dangerous, so be wary of using it, but it can be used to simplify code - but only as a last resort



## Composite values

Composite value 
- can store multiple values

![Composite Types](./images/16.%20PART%20IV.jpg)

Types

- Arrays
- Slices

Note: arrays, length is part of it's type. Slices length is not part of it's type. 

[...] elipses for an array still results in a length, which still becomes part of it's type

### Arrays

    nums := [...]int{54, 143, ..., 1000}

    var sum int

Can then be used in a for .. range... loop

Efficiency:
- CPU Cache-Lines,
- Fast Access
- 1-o-1 representation of memory

Arrays & memory usage:
- go stores array items in consecutive memory cells
- each item in an array is 1 byte
    - but you can specify multiple bytes, they will then just be consecutive in multiples

Array syntax:

	var ages [2]byte
	- this indicates an array with length 2 - of type byte

You can't have an array with length negative:
- there's no negative lengths - nonsensical
- invalid: var ages [-2]byte

Default values in the array is the default of the type:
- byte - 0
- string - ""
- etc

Examples of syntax:

	var ages [2]int

	ages[0] = 6
	ages[1] -= 3

fmt.Printf with %q:

	fmt.Printf("book: %q\n", books)

fmt.Printf with %#v to print with array's type:

	fmt.Printf("book: %#v\n", books)

You can declare arrays like this as well:

	var books [4]string

	OR

	yearly := 4
	var books [yearly]string

Note, go does not allow you to access arbitrary memory locations by default 
	(there is a work around but a more advanced topic/concept)



Gotchas

for range gotchas with arrays
- when you range over an array , the array gets copied
- all elements in the array get copied (this can add strain on a system storing large cvolumes of data? maybe?)
- A gotcha as well, is if you want to update any of the array elements in the range, append or prepend mvalues etc - you can't do it with the range value/item you have to still edit the original array with an index.



Array length gotcha:
- Array's type is consisting of its length and its element type together.
- Eg var luminosity [100]float32
- Type = [100]float32
- element type of the array would still be float32

Memory storage of arrays:

- var nums [5]int64
- Stores in 8 bytes (int64 means 8 bytes per array item)


Benefits of using arrays:
- for .. range... loop
- but remember range creates a copy of the array, you can't edit array with range values


Array literal (is also a composite literal)

Array initialization:

How to initialize the array and assign values

    var books [4]string
    books[0]

Rather:

Use Array Literal

    var books = [4]string{
        "book1",
        "book2",
        "book3"
    }

or 

    books := [4]string {
        "book1",
        "book2",
        "book3"
    } 

(^ this is the array literal)

or in same line

    [4]string{"book1","book2"}

or

    var (
        blue = [3]int{6, 9, 3}
        red = [3]int{6, 9, 3}
    )

Composite Literal used to create composite values

#### Elipses operator

Elipses operator

[...]string{"book1","book2"}
- the array will figure out it's own length, based on values passed and assigned, in this case 2.




Example:

```
func main() {

    if len(os.Args) < 2 {
        fmt.Println("Please provide a name")
        return
    }

    name := os.Args[1]

    mood := [...]string{
        "Happy",
        "Sad",
        "Angry",
        "Jealous",
        "Hungry",
        "Cold",
        "Hot",
        "Guilty",
        "Excited",
        "Joyous",
    }

    rand.Seed(time.Now().UnixNano())
    n := rand.Intn(len(mood))

    fmt.Printf("%s is %s \n", name, mood[n])

}
```

Comparing arrays:

Arrays can only be compared is they are the same type. 
Remember: An array's type includes it's length

Eg

	[3]int{6, 9, 3} and be compare with [3]int{1, 2, 3}

But you can't compare:

	[3]int{6, 9, 3} with [2]int{6, 9} 

because one is type [3]int and the other [2]int - different types

![](./images/17.%20Arrays%20are%20not%20comparable%20when%20their%20types%20are%20different.jpg)

Assigned arrays are copied into a new array:

	blue := [3]int{6, 3, 9}
	red := blue

red in the above example is a new copy of the array
- new memory space allocated for new array

You can also only assign arrays to each other if they are of the same types

	blue := [3]int{6, 9, 3}
	red = [2]int

You cannot now:

    red = blue

They are different types

### Multi dimensional arrays

Array literal for multi dimensional arrays 

	[2][3]int {
		[3]int{5,6,1}
		[2]int{9,8,4}
	}

OR you can also write:

	[2][3]int {
		{5,6,1}
		{9,8,4}
	}
	
Go infers the types from the multi deminsional declaration at the start [2][3]int - it knows it's [3]int

Contains an outer and inner array
- basically saying it contains 2 arrays or 3 int type

Multi dimensional arrays you can only store arrays of the same types

An example of ranging through multi dimensional arrays:

	students := [...][3]int {
		{5, 6, 1},
		{9, 6, 4},
	}

	var sum float64

	for _, grades := range students {
		for _, grade := range grades {
			sum += grade
		}
	}

	const N = float64(len(students) * len(students[0])) 

	average := sum/N

	fmt.Printf("Avg Grade: %g\n", sum/N)

### Arrays with keys 

Arrays with Keyed Elements
- describing indexes manually 
- also one of the features of slices

```
	rates := [3]float {
		0: 0.5,
		1: 2.5,
		2: 1,5,
	}
```

OR

	rates := [3]float {
		2: 1,5,
	}

0, 0, 1,5

OR

	rates := [3]float {
		5: 0.5,
		2.5,
		0: 1,5,
	}

Becomes

	1,5, 0, 0, 0, 0.5, 2,5

Note: Go puts unkeyed indexes at the end of the array

Keyed indexes can also be assigned using constants:

Remember this iota trick? Auto increments creates values 

	const (
		ETH = iota
		WAN
	)

	rates := [...]float64{
		ETH: 5.5,
		WAN: 120.5,
	}

	// Start constants at a different index

	const (
		ETH = 9 - iota  	// 9nth
		WAN			// 8th
	)

Unnamed types

Unnamed <> named

Unnamed and Named Types Arrays are comparable IF their underlying types are identical

	bookcase{6, 9, 3} == [3]int{9,9, 3}
	- both have the underlying types of [3]int

BUT

	bookcase {6, 9, 3} != cabinet {6, 9, 3}

They're both named types - and they can't be the same
	
BUT you can convert them, because they have the same underlying types:

	bookcase {6, 9, 3} == bookcase(cabinet{6, 9, 3})

### Custom array types

Creating types:

	type bookcase [5]int

Or

	type (
		bookcase [5]int
		cabinet [5]int
	)
	
	blue := bookcase{6, 9, 3, 2, 1}
	red := cabinet{6, 9, 3, 2, 1}

You can compare variables with identical types - but once you name them as a new type, they have a s=cascading type layer - so the underlying type changes because you've added a new type ontop of the type hierarchy

This is an important layer of knowledge to have to understand the go type system.

Recap arrays

![](./images/18.%20a%20Array%20is%20a%20collection%20of%20elements.jpg)

![](./images/19.%20can%20access%20array%20elements%20using%20index%20expressions.jpg)

![](./images/20.%20How%20many%20elements.jpg)

![](./images/21.%20This%20is%20the%20type%20of%20the%20array.jpg)

![](./images/22.%20Array%20Literals.jpg)

![](./images/23.%20Ellipsis....jpg)

![](./images/24.%20Keyed%20Elements.jpg)

![](./images/25.%20Multi-Dimensional%20Arrays.jpg)

![](./images/26.%20Copied%20array%20and%20the%20Original%20array%20are%20not%20connected.jpg)

![](./images/27.%20Different%20types%20of%20arrays%20are%20neither%20comparable%20nor%20assignable.jpg)

![](./images/28.%20An%20unnamed%20composite%20type's%20underlying%20type%20is%20itself!.jpg)

![](./images/29.%20Unnamed%20and%20Named%20typed%20values%20are%20comparable.jpg)


Digital clock example program

```
// Copyright © 2018 Inanc Gumus
// Learn Go Programming Course
// License: https://creativecommons.org/licenses/by-nc-sa/4.0/
//
// For more tutorials  : https://learngoprogramming.com
// In-person training  : https://www.linkedin.com/in/inancgumus/
// Follow me on twitter: https://twitter.com/inancgumus

package main

import (
	"fmt"
	"time"

	"github.com/inancgumus/screen"
)

func main() {
	// for keeping things easy to read and type-safe
	type placeholder [5]string

	// put the digits (placeholders) into variables
	// using the placeholder array type above
	zero := placeholder{
		"███",
		"█ █",
		"█ █",
		"█ █",
		"███",
	}

	one := placeholder{
		"██ ",
		" █ ",
		" █ ",
		" █ ",
		"███",
	}

	two := placeholder{
		"███",
		"  █",
		"███",
		"█  ",
		"███",
	}

	three := placeholder{
		"███",
		"  █",
		"███",
		"  █",
		"███",
	}

	four := placeholder{
		"█ █",
		"█ █",
		"███",
		"  █",
		"  █",
	}

	five := placeholder{
		"███",
		"█  ",
		"███",
		"  █",
		"███",
	}

	six := placeholder{
		"███",
		"█  ",
		"███",
		"█ █",
		"███",
	}

	seven := placeholder{
		"███",
		"  █",
		"  █",
		"  █",
		"  █",
	}

	eight := placeholder{
		"███",
		"█ █",
		"███",
		"█ █",
		"███",
	}

	nine := placeholder{
		"███",
		"█ █",
		"███",
		"  █",
		"███",
	}

	colon := placeholder{
		"   ",
		" ░ ",
		"   ",
		" ░ ",
		"   ",
	}

	// This array's type is "like": [10][5]string
	//
	// However:
	// + "placeholder" is not equal to [5]string in type-wise.
	// + Because: "placeholder" is a defined type, which is different
	//   from [5]string type.
	// + [5]string is an unnamed type.
	// + placeholder is a named type.
	// + The underlying type of [5]string and placeholder is the same:
	//     [5]string
	digits := [...]placeholder{
		zero, one, two, three, four, five, six, seven, eight, nine,
	}

	// For Go Playground, do not use this.
	screen.Clear()

	// Go Playground will not run an infinite loop.
	// Loop for example 1000 times instead, like this:
	//   for i := 0; i < 1000; i++ { ... }
	for {
		// For Go Playground, use this instead:
		// fmt.Print("\f")
		screen.MoveTopLeft()

		// get the current hour, minute and second
		now := time.Now()
		hour, min, sec := now.Hour(), now.Minute(), now.Second()

		// extract the digits: 17 becomes, 1 and 7 respectively
		clock := [...]placeholder{
			digits[hour/10], digits[hour%10],
			colon,
			digits[min/10], digits[min%10],
			colon,
			digits[sec/10], digits[sec%10],
		}

		// Explanation: clock[0]
		// + Each element of clock has the same length.
		// + So: Getting the length of only one element is OK.
		// + This could be: "zero" or "one" and so on... Instead of: digits[0]
		//
		// The range clause below is ~equal to the following code:
		//   line := 0; line < len(clock[0]); line++
		for line := range clock[0] {
			// Print a line for each placeholder in clock
			for index, digit := range clock {
				// Colon blink on every two seconds.
				// + On each sec divisible by two, prints an empty line
				// + Otherwise: prints the current pixel
				next := clock[index][line]
				if digit == colon && sec%2 == 0 {
					next = "   "
				}
				// Print the next line and,
				// give it enough space for the next placeholder
				fmt.Print(next, "  ")
			}

			// After each line of a placeholder, print a newline
			fmt.Println()
		}

		// pause for 1 second
		time.Sleep(time.Second)
	}
}
```

Array notes:

- cannot declare the length of an array with a variable
- if you have this use case - rather look at using slices (no fixed length to be concerned with)

### Slices

Composite types

- Slices - dynamic arrays

### Slices & Internals

Updating package prettyslice

	go get -u github.com/inancgumus/prettyslice

Differences between slice & array

Array is a fixed element type

With slices - it's like an array but you can add (or remove) elements in runtime

Why can't you do this with an array?

- the length is part of it's type
- when you declare a type in go you can't change it again in runtime
- an array's length belongs in compile time, cannot be changed in run time

Why can you alter slice lengths

- length is not part of it's type
- no fixed length at compile-time
- can grow and shrink in runtime

A slice variable []type

- var nums []int
- it's length belongs to runtime

Uninitialized slice value is nil

- nil value means it hasn't been initialized

Slice

- var nums []int
- the length is not part of it's type
- no matter the length of the slice it will be of the underlying type eg []int 

Array
- var nums [2]int
- the length is part of it's type

Comparing slices:
- you can't compare slices
- a slice value can only be compared to a nil value

How would you compare slices?
- idiomatic way is to use a loop

Loop for comparison:

	var ok string
	for i, game := range games {
		if game != newGames[i] {
			ok = "not "
			break
		}
	}
	fmt.Printf("games and newGames are %equal\n\n", ok)

(note you can use slices in a range clause even if they are nil)

You can range over a slice just like an array

You can also assign a slice to a slice (provided they have the same element type):

	games := []string{"one", "two"}
	newGames := []string{"three", "four"}
	newGames = games

	You can also set to nil:

	games = nil


Notes on nil and empty:

games = nil -> not initialized

games = []string{} -> just empty

	var ok string
	for i, game := range games {
		if game != newGames[i] {
			ok = "not "
			break
		}
	}
	
	if games == nil {
		ok = "not "
	}

	 fmt.Printf("games and newGames are %equal\n\n", ok)

An improved comparison is len

	if len(games) != len(newGames) {
		ok = "not "
	}

Rookie mistake alert: Don't check if a slice is empty or not by comparing it with a nil value - rather use len. If len is 0 then it's either nil or empty.

### Append

You can append to slices

eg

	newslice = append(existingslice, newelement)

In Go slices tend to be preferred over arrays:

Example code:

	rand.Seed(time.Now().UnixNano())

	max, _ := strconv.Atoi(os.Args[1])

	var uniques []int

	loop:
		for len(uniques) < max {
			n := rand.Intn(max) + 1
			fmt.Print(n, " ")
			
			for _, u := range uniques {
				if u == n {
					continue loop
				}
			}
			uniques = append(uniques, n)
		}
		fmt.Println("\n\nuniques: ", uniques)

Sort

	sort.Ints(slice)

Convert an array to a slice:

slice expression: [:]

	nums := [5]int{5, 4, 3, 2, 1}
	sort.Ints(nums[:])

Append
- built in function 

Returns a new slice element with the newly appended element at the end of the list

	newslice = append(slice, newElement)

Append Multiple:

	append(slice, el1, el2, el3, nthel etc)

Append slices:

	nums := []int{1, 2, 3}
	tens := []int{12, 13}
	nums = append(nums, tens...)

Using ellipses operator ...

### Slicing arrays or slices

Slicing
	- arrays or slices can be sliced
	- strings - byte slice

Syntax for slicing:

	newSlice := sliceable[startposition:endposition]

Example

	msg := []byte{'h','e','l','l','o'}

	msg[0:1] 
	> h

Caution: You cannot slice a sliceable variables beyond it's length

Tip:

Using append with slicing:

	append(msg[:4], '!')
	> hell!

BUT CAUTION:
	this affects the original slice
	The original slice now becomes this new value


[x:] - from x to end
[:x] - from start to x



### Backing Array

A slice does not store elements in memory, instead an array is created in the background that stores the elements. This is called a backing array. The backing array handles the elements being stored in memory.

A slice does not create a new backing array, just a instance of the array elements

	ages := []int{35, 15, 25}

	ages[:1]
	ages[1:3]

These all refer to the same backing array (not new arrays)

![](./images/30.%20BACKING%20ARRAY.jpg)

This shared approach makes slicing fast and cheap.

When you manually create an array, and then slice it - it becomes the backing array of the new slice.

A non-empty slice literal always creates a new backing array.

Remember append (you can create a new slice):

	grades := []float64{40, 10, 20, 50, 60, 70}
	var newGrade []float64
	newGrades = append(newGrades, grades...)

Another way to create a new backing array:

	newGrades := append([]float64(nil), grades...)

Backing arrays gotchas:

Sorting a backing array affects all the slices that reference that array

	sort.... affects the backing array

Note on why it's efficient:

A slice's backing array is contiguous in memory. So, accessing an element of a slice is very fast. Go can look at a specific memory location to find an element's value very fast.

Backing array notes:

When a slice is created by slicing an array, that array becomes the backing array of that slice.

Creating new backing arrays:

A slice literal always creates a new backing array.

	slice1 := []int{1, 2, 3}
	slice2 := []int{1, 2, 3}

Slice headers:

Slice = SliceHeader, it's a tiny data structure that describe its backing array

![](./images/31.%20SLICE%20HEADER.jpg)

This slice has a pointer field starting at the 35:

![](./images/32.%20SLICE%20HEADER%202.jpg)

![](./images/33.%20SLICE%20HEADER%203.jpg)

![](./images/34.%20NIL%20SLICE.jpg)

More info on how slices are created:

![](./images/35.%20Source%20file%20srcruntimeslice.jpg)

Notice it's the header info, with just a pointer to the array

## Memory Addresses

Memory Address:

Getting the memory address of a value:

	&data

The ampersand & shows the memory address of a value that is next to it

### Backing array address vs header address

Note: backing array address and header address are different values.

A slice header is just a tiny data structure with three numeric fields.

	Pointer, length and capacity

The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice.

The length and capacity of a slice s can be obtained using the expressions len(s) and cap(s).

Functions and arrays

When you pass an array value to a function, it creates a new array (like a local array) within the function. Different backing arrays for each. Changing an array inside a function won't mutate the original array.

```
type collection [4]string

func main() {
	data := collection["slices", "are", "awesome", "period"]
	change(data)
	s.Show("main's data", data)
}

func change(data collection) {
	// data becomes a local scoped value to this function
	// this data array and the data array in the main are different
	data[2] = "briliant"
	s.Show("change's data", data)
}
```

### Memory size of code 

Working out the memory size of go code:

What is the total memory usage of this code?

    var array [1000]int64
     
    array2 := array
    slice := array2[:]

`array` is 1000 x int64 (8 bytes) = 8000 bytes. Assigning an array copies all its elements, so `array2` adds additional 8000 bytes. A slice doesn't store anything on its own. Here, it's being created from array2, so it doesn't allocate a backing array as well. A slice header's size is 24 bytes. So in total: This program allocates 16024 bytes

    int64 is 8 bytes
    1000 element - 8 * 1000
    copying an array to another array = 8000 * 2
    Slice header = 24 bytes

    16000 + 24 = 16024

Capacity of a slice

cap function returns the capacity of a slice
	
	ages := []int{35, 15, 25}
	ages = ages[0:0]
	ages[0:cap(ages)]

You cannot extend a slice beyond it's capacity

You cannot extend a slice back

- once you've sliced values you can't try reaccess other values

Length of the array:

The length describes the length of a slice but a capacity describes the length of the backing array beginning from the first element of the slice

The append function is pretty efficient in how it works. Don't try to optimize it - it already is optimized.

What are the length and capacity of the words slice?

    // The words slice has 1023 elements.
    //
    // Tip: The keyed slice works like the same as a keyed array.
    // If you don't remember how it works, please check out the keyed elements in the arrays section.
    //
    words := []string{1022: ""}
    words = append(words, "boom!")

That's right! The length and capacity of the words slice was 1023. Appending one more element doubles the capacity. It's because the capacity was less than 1024. If the capacity was 1024 and greater, the append will grow the backing array roughly around 25%. Please take a look at the differences here: https://play.golang.org/p/cIogCPr7QGP

    // The words slice has 1024 elements.
    //
    // Tip: The keyed slice works like the same as a keyed array.
    // If you don't remember how it works, please check out the keyed elements in the arrays section.
    //
    words := []string{1023: ""}
    words = append(words, "boom!")

After the capacity of 1024, the append function grows at a slower rate, about 25%. Please take a look at this to understand it better: 

Length & Capacity:

	len(slice)
	cap(slice)

Full slice expressions

	newDlice := slice[START:STOP:CAP]

	stop position CANT be greater that cap position

Limit the slice size with cap

One use case for this is if you overwrite the cap - and then append you will create a new backing array (instead of overwriting the both slices)

![](./images/36.%20func%20main().jpg)
￼
If the cap hadn't been updated, then index 3 and 4 of the original slice would just have been overwrittern. 
Editing the cap helped create a new backing array and then the original values were not overwritten

Make

Pre allocate a backing array

	make([]int, 3)
	the second value (3) becomes the length and capacity of the backing array

Why use make? You can precreate backing arrays for slices - help with performance? memory allocation?

	make([]int, 3, 5)

An interesting example:

Set capacity: make

Create a backing array with a larger capaciity with make:

![](./images/37.%20s.PrintBacking.jpg)

The only problem is, append adds elements after the length of the slice.

The trick is to create a slice with 0 length and capacity you want:

![](./images/38.%20func%20main()%202.jpg)

Notice: 

	upTasts := make([]string, 0, len(tasks))

### Copy

![](./images/39.%20It%20returns%20the%20number%20of%20copied%20elements.jpg)

A big note here, copy will only copy over a max of the length of the starting array it's copying to. You can't create a longer slice with copy - so you will loose overlapping copied elements if the starting slice is shorted than the copied slice.

To grow a slice you can use append. 

You can also use append to copy over elements (instead of copy) - but you dont get the same features that you get with copy:

	data = append(data[:0], []float64{10, 5, 15, 0, 20}...)

Another trick with copy is to use make before copy:

	saved := make([]float64, len(data)]
	copy(saved, data)

vs

	saved := append([]float64(nil), data...)

They do the same

### Multi dimensional slices

	spendings := [][]int {
		{200, 100},
		{500},
		{50, 25, 75}
	}

	for i, daily := range spendings {
		var total int

		for _, spending := range daily {
			total += spending
		}
		fmt.Printf("Day %d: %d\n, i+1, total)
	}

Lets say you want to make sure your array always has a length of 5 for mon - fri:

	spendings := make([][]int, 0, 5)
	spendings = append(spendings, []int{200,100})
	spendings = append(spendings, []int{25, 10, 45, 60})
	spendings = append(spendings, []int{5, 15, 35})
	spendings = append(spendings, []int{95, 10}, []int{50, 25})

Note: elipses not used - you're appending the whole slice not slice elements


A better way to do this:

![](./images/40.%20content.jpg)

![](./images/41.%20for%20i%2C%20line.jpg)

Creating a fetch function to retrieve data from a "file":

[todo ... add code]

Question 1:

What are the length and capacity of the 'part' slice?

1. lyric := []string{"show", "me", "my", "silver", "lining"}
2. part  := lyric[1:3:5]


General Formula: 

	`[low:high:max]` => `length = high - max` 
	
and 

`capacity = max - low`. `lyric[1:3]` is `["me" "my"]`. `lyric[1:3:5]` is `["me" "my" "silver" "lining"]`. 

So, `[1:3]` is the returned slice, length: 2. `[1:3:5]` limits the capacity to four because after the 1st element there are only four more elements.

Copy notes:

A note on how copy works:
- it seems you tell it where to copy from, if you just pass a slice it copies from the start, if you pass it a slice with a specified start, it starts at the end:
- eg

    cutpoints := []int{8, 10, 5}

    for n, i := 0, 0; n < len(lyric); i++ {
        n += copy(fix[n+i:], lyric[n:n+cutpoints[i]])
        fix[n+i] = "\n"
    }


More examples:

    slice := []string{"one", "two", "three", "four"}
    extra := []string{"five", "six", "seven", "eight"}
    new := make([]string, 10, 10)
    copy(new, slice)
    copy(new[len(slice):], extra)
    fmt.Printf("%s \n", new)

## Files

Working with Files:

Reading files:

ioutil.ReadDir
- []os.FileInfo
- .Name()
- .Size()

Example func main:

    args := os.Args[1:]

    if len(args) == 0 {
        fmt.Println("Error: provide args")
        return
    }

    files, err := ioutil.ReadDir(args[0])

    if err != nil {
        fmt.Println(err)
        return
    }

    for _, file := range files {
        if file.Size() == 0 {
            fmt.Printf("%s \n", file.Name())
        }
    }

Writing files:

ioutil.WriteFile
- uses bytes slice
- strings can be converted to bytes slices with ...

Note: A string is actually a byte slice underneath
- stringvalue... -> the ... expands it to the bytes

File permissions:

permissions-calculator.org

Example

    var names []byte

    for _, file := range files {
        if file.Size() == 0 {
            fmt.Printf("%s \n", file.Name())
            names = append(names, file.Name()...)
            names = append(names, '\n')
        }
    }

    err = ioutil.WriteFile("test.txt", names, 0644)
    if err != nil {
        fmt.Println(err)
        return
    }

ioutil
- ioutil.ReadDir
- ioutil.WriteFile


Adding longer backing array:

	var total int

	for _, f := range files {
		if file.Size() == 0 {
			total += len(file.Name()) + 1
		}
	}

	names := make([]byte, 0, total)

Checking the performance:

	$ time go run main.go > /dev/null

More about Strings:

- Bytes, Runes and String
- Unicode Code Points
- Character Sets
- Printing and Converting
- Indexing and Slicing Strings
- String Internals

STRINGS are byte slices []byte
- they are interchangeable with each other

You can represent a character with a run eliteral
- numbers and rune literals are the same thing?
- unicode code point - a number that can represent a character

![](./images/42.%20Rune%20Literals.jpg)

Rune literals are numeric code points
- they are numbers
- eg 65 = code point for "A"
- eg 90 is the code point for "Z"

UTF-8 encoded representation of characters:

- % -12x   string(n)
- the extra space will print bute with extra spaces
- string(n) encodes the given code point to a utf-8 encoded string value automatically


A byte would store a character that can fix into a single byte (0 - 255)

But many characters once UTF-8 encoded need multiple bytes
- for multi byte storage you use runes.
- eg emojis would use rune - multi byte characters


How bytes, runes and strings work together:

- A string value is a read-only byte slice
= A string is an immutable byte slice - you cannot change any of it's values
- but you can duplicate the string with a new byte slice with a new backing array

```
	str := "Yugen"

	// str[0] = "N" - errs
	// str[1] = "O" - errs

	bytes := []byte(str)

	str = string(bytes)

	fmt.Printf("%s\n", str)
```

Lengths

	len(str)

len - counts the number of bytes in a string - not runes

	utf8.RuneCount(...)  /  utf8.RunecountInString(str)

utf8.RuneCount - will return the number of runes


Printing a byte slice as hexadecimal numbers:

	% x

this will also show you the bytes
Remember: len counts the bytes, not the words/runes, so runes will appear as more because they are more bytes

Count runes as well:

	utf8.RuneCountInString()


If you range through a string with runes, you'll notice the indexes skip in certain elements:
- this is because of the multiple bytes to store the rune values

```
	for i, r := range str {
		fmt.Printf("str[2%d] = % -12x = %q\n|, i, string(r), r)
	}
```

Eg

￼![](./images/43.%20str%5B%200%5D%20%3D%2059.jpg)

This makes it tricky when you want to retrieve a rune from a string slice - 
- str[1] will only return part of the rune
- str[1:3] would get you the whole rune and not just partial 
- with slicing you are returning 1 byte at a time


Rune in a UTF-8 encided string can have a different number of bytes because UTF-8 is a variable byte-length encoding

Especially in scripting languages you can index UTF-8 strings easily. However, Go doesn't allow you to do so by default because of efficiency reasons.

Go never hides the cost of doing something.

Another solution to make sure you convert the string's byte slice containing the runes from the byte slice to a rune slice:

	runes := []runes(str)

In this case you can index for the entire rune, and not a byte at a time

Why use byte slices over rune slices?
- memory - rune slices is int32 - it stores 4 bytes per index
- with a byte slice it literally just stores the bytes you need, no extra bytes stored

UTF-8 encoding
- a string could be encoded in any encoding scheme - not just UTF-8
- only string literals are UTf-8 encoded
- string variables can be used for more than UTF-8 though, eg sound, images etc.


Rune Decoding

For Loops

What you might do:

	for i := i < len(text); i++ {
		fmt.Printf("%c", text[i])
	}

	This will print each byte - runes are multiple bytes - meaning this will print out partial part of the rune and not the full rune

	r, runeSize := utf8.DecodeRune(text)
	or
	r, runeSize := utf8.DecodeRuneInString(text)

For loop with runes:

	for i := 0; i < len(text); {
		r, size := utf8.DecodeRuneInString(text[i:])
		fmt.Printf("%c", r)
		i += size
	}
	
For range loops:

	for _, r := range text {
		fmt.Printf("%c", r)
	}
	
This will return the bytes not the strings in each loop

Converting a slice to a string is a costly application

utf8 package:

	word := []byte("öykü)
	_, size := utf8.DecodeRune(word)

Uppercase the first rune:

	copy(word[:size], bytes.ToUpper(word[:size]))
	fmt.Printf("%s = % [1]x\n", word)


It's sometimes easier to use the utf8 helper methods than a for range loop

Why are string literals immutable?

String Header

    func main() {

    }

    type StringHeader struct {
        pointer uintptr
        length int
    }

    func dump (s string) {
        ptr := *(*StringHeader)(unsafe.Pointer(&s))
        fmt.Printf("%q: %+v\n", s, ptr)
    }

Convert a string to a bytes slice:
- bytes := []byte(str)


Different formats:
- Rune
- Decimal
- Hexidecimal

```
	const word = "console"

	for _, w := range word {
	    fmt.Printf("%c\n", w)
	    fmt.Printf("\tdecimal: %[1]d\n", w)
	    fmt.Printf("\thex    : 0x%[1]x\n", w)
	    fmt.Printf("\tbinary : 0b%08[1]b\n", w)
	}

	// print the word manually using runes
	fmt.Printf("with runes       : %s\n",
	    string([]byte{'c', 'o', 'n', 's', 'o', 'l', 'e'}))
	
	// print the word manually using decimals
	fmt.Printf("with decimals    : %s\n",
	    string([]byte{99, 111, 110, 115, 111, 108, 101}))

	// print the word manually using hexadecimals
	fmt.Printf("with hexadecimals: %s\n",
	    string([]byte{0x63, 0x6f, 0x6e, 0x73, 0x6f, 0x6c, 0x65}))
```

Pro Tip:
- Don't convert types if you can avoid it. 
- If you're working with a byte - keep working with a byte - a string keep working with a string.
- Bytes are more efficient - so if you can work with them it's preferable


Conversion Cheetsheat for Go:

Tip: avoid converting - try stay with the type if you're using that type

Strings & Ints:

Convert string to Int:

	strconv.Atoi(...)


Convert int to string:

	strconv.Itoa(...)

Bytes & Strings:

Convert a string to a byte slice:

	[]byte(str) 

Convert a byte slice to a string:

	string(byteslice)

Runes and strings:

Convert a string to a rune:

	 utf8.DecodeRuneInString(char)

Check if a rune is a space (new line etc)

	unicode.IsSpace(r);

Take a look at the unicode packages

	$ go doc unicode 



Maps and Internals

Indexable Key-Value Pairs

Maps use an O(1) Algorithm

- maps spend a constant amount of time looking for a key

Example declaration:

	var dict map[string]string

Index:

For arrays of slices the index is an integer key

With maps you can use any comparable type for a key

Notes on comparable types: https://flaviocopes.com/golang-comparing-values/

Example:

    var dict map[string]string

    key := "good"
    value := dict[key]
    fmt.Printf("%q means %#v\n", key, value)
    fmt.Printf("# of Keys: %d\n", len(dict))

Note:

Key and Value types don't need to match. 

	eg map[string][]float64

Key types of a map need to be comparable (==)
- slice, map and functions are not comparable so not valid key types for maps


Populate a map

You can read from an uninitialised map. You cannot write. 

You need to initialise a map in order to write to it.

Use:

	:=

Eg, using a map literal:

	dict  := map[string]string{}

Now you can assign to it:

	dict  := map[string]string{}
	dict["up"] = "upword"
	dict["down"] = "downword"

Remember:

Composite literals create, initialize, and return composite values

You can also create with values:

Eg:

	dict := map[string]string{
		"good": "xxx",
		"great": "xxx",
		"perfect": "xxx",
	}

All keys need to remain the same specified type

All values need to remain the same specified type

How to detect whether a key exists or not in a map:

    value, ok = mapValue[key]

ok is true if the key exists, false if it doesnt 

Example with if:

	if value, ok := dict[query]; !ok {
		fmt.Printf("%q now found\n", query)
		return
	}

Note:

for maps the keys and value are stored unordered, if you loop over a map, don't depend on the order

Maps are designed for fast lookups, not for fast traversal

Slices are better for fast looping/traversal

Maps internals (+cloning)

Maps have headers
- tracks 

When you create a map go creates a map header behind the scenes, and a map variable (value) is a pointer to a map header value in memory

Map vs slice

Map values are like slice values they do not store any elements on their own

They are pointers to some internal structures

Difference

A slice value is a slice header
- it stores the slice header directly in itself
- there is a pointer field in the slice header that points to a backing array 
- a slice value indirectly points to a backing array

A map value 
- a map value does not contain the map header in itself
- a map value is only a pointer - a memory address of a map header
- the map header then contains a pointer to the real data

slice value = header -> points to backing array

map value = pointer -> points to map header -> map header points to map data


map header tracks everything about a map value

Map value itself is not a structure, unlike a slice which is.

Map headers are a lot more complex than slice headers.
- map data have a lot of moving parts behind the scenes
- when you assign maps to a new value or pass them to functions, you only pass the pointer and the pointer points to the map header (you dont pass the whole header)

Make

How do you create 2 map values from a single map. Make lets you do this. Similar to how it was used with slices.

eg

	newmap := make(map[string]string)

you can also add length

	newmap := make(map[string]string, len(oldmap))


Remember you can use range to loop through maps:

eg

	for k, v := range oldmap {
		newmap[v] = k
	}


delete

Delete values from a map:

	delete(mapvalue, "key")

How do you destroy a whole map value? 

Remember doing something like this:

	mapvalue = nil

this will only overwrite the pointer value of the value, not the underlying map itself

    mapclear() 

To delete a whole map you need to do it by a loop:

	for k := range mapvalue {
		delete(dict, k)
	}

Go converts this loop to a single operation called mapclear()

### Structs 

Structs allow us to represent concepts

Kind of like classes in OOP

It's like a blueprint (maybe more like inheritance) 

Structs group related data in a single type

Field name and types are fixed at compile-time - no new field names or types can be changed or added at runtime

Field values belong to runtime, so values can be changed during runtime 

![](./images/44.%20SLICE%20%26%20MAP.jpg)

Declaring a struct with a struct literal:

	type VideoGame struct {
		Title 		string
		Genre 		string
		Published 	bool
	}

Rule: field names should be unique

Creating a struct value:

Note a struct value is a composite literal

	pacman := VideoGame {
		Title: 		"Pac-Man",
		Genre:		"Arcade Game",
		Published: 	true,
	}


Zero values:

Every uninitialised struct field gets a zero-value depending on its type. 


struct values:

Struct values go together with its fields. Struct values act as a single value


An example of code that could be improved with a struct:


	var (
		name, lastname string
		age int

		name2, lastname2 string
		age2 int
	)

	name, lastname, age = "Pable", "Picasso", 91
	name2, lastname, age2 = "Sigmund", "Freud", 83

vs

	var picasso struct {
		name, lastname string
		age int
	}

	var freud struct {
		name, surname string
		age int
	}

	fmt.Printf("\nPicasso: %+v\n", picasso)
	fmt.Printf("\nFreud: %+v\n", freud)

vs

	type person struct {
		name, lastname string
		age int
	}

	var picasso person
	var freud person

	fmt.Printf("\nPicasso: %+v\n", picasso)
	fmt.Printf("\nFreud: %+v\n", freud)

Setting values:


	type person struct {
		name, lastname string
		age int
	}

	var picasso person
	var freud person

	picasso.name = "Pablo"
	picasso.lastname = "Picasso"
	picasso.age = 91

	freud.name = "Sigmund"
	freud.lastname = "Freud"
	freud.ago = 83

	fmt.Printf("\nPicasso: %+v\n", picasso)
	fmt.Printf("\nFreud: %+v\n", freud)

Retrieving individual fields:

	fmt.Printf("\field: %+v\n", picasso.name)
	fmt.Printf("\field: %+v\n", picasso.lastname)
	fmt.Printf("\field: %+v\n", picasso.age)
	
Changing + modifiers to # modifiers (plus to sharp) 

	fmt.Printf("\nPicasso: %#v\n", picasso)
	-> prints the struct type (eg main.person)

You can also dynamically create with values:

eg
	picasso := person{
		name: "Pablo",
		lastname: "Picasso",
		age: 91
	}

You dont have to provide the field names:

	picasso := person{
		"Pablo",
		"Picasso",
		91
	}

Go will match the order of the values to the order of the fields

Order only matters with you don't use fields names. If you use fields names the fields and values can be in any order.

Best practice: use field names

Comparison & Assignment

Structs are base values - no backing array like with slices

Structs are comparable. You can compare structs of the same type.

Refactoring form this:

	type song struct {
		title, artist string
	}

	func main() {
		song1 := song{title: "title1", artist: "artist"}
		song2 := song{title: "title2", artist: "artist"]
	}

To:

	type song struct {
		title, artist string
	}

	type playlist struct {
		genre string
		songs []song
	}

	func main() {
		rock := playlist{genre: "indie rock", songs: []song{
			song{title: "song1", artist: "artist1"},
			song{title: "song2", artist: "artist2"},
		}}
	}

Slice literal []song{}

or

	type song struct {
		title, artist string
	}

	type playlist struct {
		genre string
		songs []song
	}

	func main() {
		songs := []song{
			song{title: "song1", artist: "artist1"},
			song{title: "song2", artist: "artist2"},
		}

		rock := playlist{genre: "indie rock", songs: songs}
	}

A Gotcha:

You can only compare a struct provided all fields are comparable

Slices are not comparable

You cannot compare struct values if they contain fields with incomparable types like a slice, map or function value.

In this case you need to compare manually with a range loop.

Inheritance / Embedding

Go doesn't have inheritance, but it has composition. This is referred to as Embedding in go.

Go prefers composition over inheritance. 

Reference (more info): https://turnoff.us/geek/inheritance-versus-composition/

An example:

	type text struct {
		title string
		words int
	}

	type book struct {
		text text
		isbn string
	}

	moby := book{
		text: text{title: "moby dick", words: 234242},
		isbn: "23242"
	}

...moby.text.title

Or using anonymous fields:

	type text struct {
		title string
		words int
	}

	type book struct {
		text
		isbn string
	}

	moby := book{
		text: text{title: "moby dick", words: 234242},
		isbn: "23242"
	}

moby.title...

Note you still have to use the explicit fields in the struct literal. No magic there.

![](./images/45.%20ANONYMOUS%20FIELDS.jpg)

Log Parser
- Initially setup in Section 11
- Then revisited and improved with structs in section 12: 
    - vid 164

Log Parser notes:

When using maps, you can't change the map directly, you can only change an addressable value (this will be covered more in the pointers section).

You need to create a copy of the map and assign it to the field:

	r := result{
		domain: domain,
		visits: visits + p.sum[domain].visits,
	}

	p.sum[domain] = r

or even better, more concisely:

	p.sum[domain] = result{
		domain: domain,
		visits: visits + p.sum[domain].visits,
	}

Encoding values in JSON

Exported fields (making struct fields caps):

	type user struct {
		name 		string
		password 	string
		permissions
	}

vs exported:

	type user struct {
		Name 		string
		Password 	string
		Permissions
	}

This is accessible by other packages

Using the json package:

	out, err := json.Marshal(users)
	if err != nil {
		fmt.Println(err)
		return
	}

pretty print version:

	out, err := json.MarshalIndent(users, "", "\t")

syntax:

	out, err := json.MarshalIndent(users, <prefix>, <indent>)


Note: the json wont display anonymous fields. Fields need to be named.

You can do further configuration of the displayed json data with field tags. See below:

Advanced:

structs can have field tags (like additional instructions)

![](./images/46.%20FIELD%20TAGS.jpg)

Field tags are metadata about the field. Mostly used for controlling the encoding/decoding behaviour. 

Field tags are string literals. They have a key value structure, the value is comma separated options.

![](./images/47.%20FIELD%20TAGS%202.jpg)

More info on field tags:
https://www.youtube.com/watch?v=_SCRvMunkdA



Decoding json

    json.Marshall() encodes json
    json.Unmarshall() decodes json

Note: you can't pass unmarshall a variable directly, you need to pass it a pointer (&....)

eg

	var users []user

	err := json.Unmarshal(input, &users)

Note the &users

Address operator

The & is called the address operator. It gives the value address of the variable. 

Notes on structs:

Field names and types are part of a struct's type.

eg

	struct {
		title, genre 	string
		rating		float64
		released 	bool
	}

is type:

	struct{ title string, genre string, rating float64, released bool}

Note:

Types with different names cannot be compared. However, you can convert one of them to the other because they have the same set of fields. movie{} == movie(performance{}) is ok, or vice versa.

 eg

	type movie			struct { item }
	type performance 	struct { item }

Homework:
- do exercises 167

Functions:

Reusable code blocks

Pointers stores memory addresses

    func name(param1 type1, param2 type2, ...) (returnTypeA, returnTypeB, ...){
        .... code
        return value1, value2... // should match return values declared
        // or just a plain return no values
    }

    func sum(a int, b int) {} == func sum(a, b int) {}

Declaring package variables is a bad practice (like a global value in the package)

![](./images/48.%20thre.com.jpg)

Go constructor pattern

This is called the constructor pattern.
Now, the parser knows how to create itself.
Go does not have init functions, but this is a work around.

eg

	func newParser() parser {
		return parser(sum: make(map[string]result))
	}

Naked Return

Returns the named result values automatically

![](./images/49.%20NAKED%20RETURN.jpg)
￼
^ go does this behind the scenes without the vars parts (the var does not need to be declared) - look into this a bit more 

Pass by value

In Go, every value is copied when assigned to a variable or passed to a function
- however there is a gotcha with map values
Map values are the memory address of a mad header
- so maps passed to a function will point to the header and in turn to the value in memory anyway 
BUT within the map is has values, like slices, and the slices will copy as new values 
so same map, but different slice
- so one solution is to return slice values from functions

Pointers

What is a pointer?

A pointer stores the memory address of a value

In the examples P and V will be used
- P -> Pointer Variable
- V -> Variable

& -> finds the address
* -> finds the value
* -> *Type denotes a pointer type


The get the memory address of a variable you us &variable

eg
	var counter byte = 100
	P := &counter

Note P is a pointer variable and stores a memory address. The pointer variable has a pointer type, *byte 

To get the value of a pointer variable you use the indirection operator - *
eg
	*P
	V := *P

V is now the actual variable, so it's type is now byte and value 100

Pointer types

Pointers have types too

![](./images/50.%20var%20counter%20byte%20%3D%20100.jpg)

- *type
- eg *byte

Indirection operator

![](./images/51.%20INDIRECTION%20OPERATOR.jpg)

Note if you change the V value you don't change the counter

![](./images/52.%20INDIRECTION%20OPERATOR%202.jpg)

A pointer value will always point to the latest value of the value it points to

![](./images/53.%20ALWAYS%20FRESH.jpg)

Note, the counter variable, when updated can update the value that it is pointing to:

![](./images/54.%20SPOOKY%20ACTION%20AT%20A%20DISTANCE.jpg)

![](./images/55.%20SUMMARY.jpg)

![](./images/56.%20SUMMARY%202.jpg)

Using pointers with functions

A func can change a value belonging to another func (or scope) indirectly through a pointer.

Pointers are variables too, and are stored in memory.

Go automatically manages the memory around handling counters.

Pointers & Composites

Slices

Slices already contain pointers. 

Slice header bears a pointer to its backing array, so you don't need to use a pointer to a slice to modify its elements.

Passing slices to functions is uncommon. In turn Using slices with pointers is uncommon. 

Maps

A map value is already a pointer. So you also don't need to use pointers with maps.

Structs

Structs work well with pointers

Methods and interfaces

![](./images/57.%20DATA%20%2B%20BEHAVIOR.jpg)

Attaching methods to a type

Value Receiver

Attach the printBook() method to the book type.

    func (b book) printBook() {
        fmt.Printf("...", b.title, b.price)
    }

(b book) -> input parameter / receiver

![](./images/58.%20VALUE%20RECEIVER.jpg)

![](./images/59.%20DATA%20%2B%20BEHAVIOR%202.jpg)


Pointer Receivers

A method is a function that automatically receives a variable

eg

	var (
		mobydick = book{title: "moby dick", price: 10
	)

	mobydick.print()

Method expressions

You can also call a method directly form a type

Method Expressions allow you to call a method through a type

eg

	var (
		mobydick = book{title: "moby dick", price: 10
	)

	book.print()

Go automatically behind the scenes passes through the type as the first argument of a method.

![](./images/60.%20Manually%20passes%20mobydick%20to%20print.jpg)


Method vs Function

A method belongs to a type
A function belongs to a package

![](./images/61.%20POINTER%20RECEIVER.jpg)

Eg

	type game struct {
		title string
		price float64
	}

	func (g *game) print() {
		fmt.Printf("%-15s: $%.2f\n", g.title, g.price)
	}

	func (g *game) discount(ratio float64) {
		g.price += (1 - ratio)
	}

...

	var (
		minecraft := game{title: "minecraft", price: 20
	)

	minecraft.discount(.5)

Using pointers helps go know that you want the calling type instance to be affected

Note 

You did not need to call the discount method with & 

eg

	(&minecraft).discount(.5)

Go does this behind the scenes. It knows if there is a pointer to make it a pointer value.

When a method has a pointer receiver Go can take its address automatically.

Large structs

A method with a value receiver copies the received value - more memory is used

Each time a method is called it copies a new copy of the value

eg

	func main() {

		type huge struct {
			games { 100000000 } game
		}

		var h huge

		for i := 0; i < 10; i++ {
			h.addr()
		}
	
	}

	func (h huge) addr() {
		fmt.Printf("%p\n", &h)
	}

This will copy the huge struct each time

vs updating to a pointer

	func (h *huge) addr() {
		fmt.Printf("%p\n", &h)
	}

Now the program runs and uses a lot less memory and runs faster.

Attachable types

Methods can be attached to almost any type, not just structs.

![](./images/62.%20ATTACHABLE%20TYPES.jpg)

You can keep extending your application with more methods and types.

eg

	func main() {
		var (
			minecraft = game { title: "minecraft", price: 10 }
			tetris = game{ title: "testris", price: 20 }
		)	

		var items = []*game
		items = append(items, &minecraft, &tetris)

		my := list(items)
		my.print()
	}

	type list []*game

	func (l list) print() {
		for _, it := range l {
			it.print()
		}
	}

Interfaces

Interface decouples types from each other

Interface is a protocol - a contract. It's an abstract type.

Abstract type vs concrete type

All non-interface types are concrete types
- int, array, slice, func, string, struct, map, float64, chan etc


Eg

	type printer interface {
		print()
	}

It's an abstract type, only describes (a protocol / contract) no implementation

Convention "-er" suffix
- eg printer

The interface only describes the expected behaviour (methods)

eg interface code:

	type printer interface {
		print()
	}

	type list []printer

	func (l list) print() {
		if len(l) == 0 {
			fmt.Println("Sorry, We're waiting for delivery. "
			return
		}

		for _, it := range l {
			fmt.Printf("(%-10T) --> ", it)
			it.print()
		}
	}

Go does not have the "implements" keyword. It is already implied.

A type satisfies an interface automatically when it has all  the methods of the interface without explicitly specifying it.

"The bigger the interface the weaker the abstraction" - Rob Pike

Keep interfaces small - eg single methods

Dynamic value

Extract the dynamic value from the interface value

Declare a variable as the interface type:

eg interface calle printer

	var p printer

Now assign a value to it, eg a struct

	p = mobydick
	p = rubik
	p = &minecraft
	p = &tetris

You can assign any value to the interface as long as it follows the interface, eg has the declared method/s eg print()

	p.print()

Note, you can't call any other methods besides the interface mthods

eg if the struct has other methods normally, even though you assigned the struct to the interface and the struct has many more methods, you can only call the methods that the interface has declared in itself 

![](./images/63.%20You%20can%20no%20longer%20access%20all%20the%20methods.jpg)

![](./images/64.%20DYNAMIC%20VALUE.jpg)

Just a note, the print() is also considered a dynamic value because you can change it during runtime, just as long as it satisfies the interface

![](./images/65.%20DYNAMIC%20VALUE%202.jpg)

An interface has 2 parts
- Dynamic value 
- Dynamic type


How do you extract the original values of the object/class? You use a type assertion. 

eg

	p.(*game)

![](./images/66.%20EXTRACTION.jpg)

![](./images/67.%20The%20interface%20value.jpg)

Doesn't have to be a pointer type, it needs to match the original type

	eg p.(book)

You can still add multiple methods to the interface, you just don't have to add the method into it's definition

Some examples of how you can handle different types 

![](./images/68.%20func%20(1%20list)%20discount%20(ratio%20float64)%20%7B.jpg)

You can also rewrite more compact:

![](./images/69.%20func%20(l%20list)%20discount%20(ratio%20float64)%20%7B.jpg)

Notice the multi "it" variables names, duplicating names is quite common in go. 

There are 2 use cases for a type assertion

1. you can use it to extract the dynamic value from an interface value
2. you can check whether an interface value provides the methods that you want or not

Empty interfaces

eg 

	type empty interface {
	
	}

or

	interface {}

or

	var e interface{}


You can assign values to interfaces in runtime. But the interface still has a type. 

To extract the value you need to extract it using a type assertion.

eg

	var any interface{}

	any = 3

	any = any.(int) * 2

	fmt.Println(any)


The variable `any` stores an int value
However you cannot directly use it as an int value.
You need to extract it using a type assertion: any.(int)

Eg with slice:

	nums := []int{1, 2, 3}

	var any interface {}
	any = nums

	_ = len(any.([]int))

You can use an empty interface when you want a value of multiple types:

eg

	type book struct {
		title 		string
		price 		money
		published 	interface{}
	}

To summarise:

Go allows you to write type safe code, but the empty interface can cross that line. But use it sparingly, it can result in hard to understand and brittle code.



Type switch

When you have a lot of conditions to check you can also use a type switch:

eg

	switch e := v.(type) {

	}

Detect and extract the dynamic value from an interface value

(v should be an interface value)

![](./images/70.%20TYPE%20SWITCH.jpg)

Examples of .(type) usage in a switch:

	switch v.(type) {
		case int:
			fmt.Print("int	-> ")
		case string:
			fmt.Print("string	->")
		default:
			fmt.Print("nil	->")

	}

or

	var t int

	switch v := v.(type) {
		case int:
			t = v
		case string:
			t, _ = strconv.Atoi(v)
		default:
			return "unknown"
	}

	// Mon Jan 15:04:05 -0700 MST 2006
	const layout = "2006, Jan"

	u := time.Unix(in64(t), 0)
	return u.Format(layout)

Promoted Methods

Using struct embedding 
(rewatch the struct embedding lecture)

Reminder of struct inheritance:

![](./images/71.%20INHERITANCE.jpg)

Go doesnt use inheritance though, it uses composition, and in go composition is called embedding:

There with inheritance it was a new object, with composition is is not a new type, is contains the same type.

![](./images/72.%20EMBEDDING.jpg)

https://turnoff.us/geek/inheritance-versus-composition/

Code example:

	type text struct {
		title string
		words int
	}

	type book struct {
		text text
		isbn string
	}

	moby := {
		text: text{title: "moby dick", words: 23423),
		isbn: "12312"
	}

anonymous field (dont need to say text twcie):

	type book struct {
		text
		isbn string
	}

by using the anonymous field you can type less code

eg

	moby.text.words == moby.words

Back to promoted methods:

EG a product type

![](./images/73.%20package%20main.jpg)

![](./images/74.%20type%20book%20struct.jpg)

update the book's print t pointer

![](./images/74.%20type%20book%20struct.jpg)

![](./images/75.%20product.jpg)

![](./images/76.%20LearnGoProgramming.com%20%20%40inancgumus.jpg)

![](./images/77.%20LearnGoProgramming.com%20%20%40inancgumus%202.jpg)

![](./images/78.%20LearnGoProgramming.com.jpg)

![](./images/79.%20package%20main%203.jpg)

Fix errors

![](./images/79.%20errors%20package%20main.jpg)

![](./images/80.%20PROMOTED%20METHODS.jpg)
