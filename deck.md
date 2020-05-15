---
theme: uncover
class: invert
paginate: true
---
<style>
  section {
    font-family: "helvetica";
  } 
  
  img { width: 100%; }

  h1 strong { color: #FF7500 !important; }

  img[src*="#svg"] {
    width: 50%;
    height: auto;
  }
</style>

# **Rust One-Oh-One**

### ducks

May 15, 2020

---

## Preview

- Intro
- Installation
- Hello, World
- Common Programming Concepts (vars, types, functions, etc)
- Ownership
- Collections

---

## What is, Rust?

A static, strongly typed and compiled language focusing on performance and
safety, especially concerning concurrency and memory

---

## What is, Rust?

Started in 2006 by Graydon Hoare as a personal project. Sponsored by Mozilla
in 2009 and announced in 2010.

Rust 1.0 was released on **THIS DAY** in 2015.

---

## What is, Rust?

Fun fact: voted most loved programming language since 2016 in the SO Dev Suvery

---

## How to install Rust

Use `rustup` to install and manage Rust versions.

```
$ curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

---

## Rustup 

Update all branches:
`rustup update`

Update stable branch:
`rustup update stable`

Update rustup itself:
`rustup self update`

---

## Howdy, y'all *

```
fn main() {
    println!("Howdy, y'all");
}
```

---

## Ahoy, Cargo!

Cargo is Rust's build system and package manager. 

`cargo --version`

---

## Creating a new Cargo project *
<!-- up_dog example -->

```
cargo new up_dog && cd up_dog
```


Cargo will create 2 files and 1 directory.


`Cargo.toml` - cargo project config file
`src/main.rs` - src directory with our main rust file

---

## Cargo config

```
[package]
name = "up_dog"
version = "0.1.0"
authors = ["Up Dog <up@dog.com>"]
edition = "2018"

[dependencies]
```

---

## Building and running

`cargo build`

`cargo run`

`cargo run -- --verbose --dry-run` 

---

### Test, Docs, Benchmarks, Check

`cargo test`

`cargo doc`

`cargo bench`

`cargo check`

---

## Common Programming Concepts

- variables
- data types
- functions
- flow control
- comments

---

## Variables and mutability *
<!-- immutable-variables example -->

```
let pi = 3.14159;
```

By default, variables are immutable.
This is a Rust nudge towards safety and concurrency.

Rust uses conventional snake case for variable names as well as function names.

---

## Variables and mutability *
<!-- mutable-variables example -->

Declare a mutable var by using the `mut` keyword.

```
let mut count = 0;
```

---

## Constants

Cannot use `mut` with constants.
Define with `const` and the value type must be annotated.

`const MAX_HP: u32 = 100_000;`

---

## Data types

Because Rust is *statically typed*, it must know the types of all vars at
compile time. Often, the compiler can infer the type based on the value.

However, in more complex situations, such as converting types, you will need
to provide an annotation.

---

## Scalar types

A scalar type represents a single value. Rust has four primary scalar types:
integers, floating-point numbers, Booleans, and characters.

---

## Integers

An int is a number without a fraction. They can be `u` for unsigned or `i` for
signed. 

We saw `u32` earlier.

This is a positive number that takes up 32 bits of space.

---

| Length  | Signed | Unsigned |
| ------- |:------:| --------:|
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    |

---

## Floating-point numbers

Rust has two primitive types for floating-point numbers, which are numbers with
decimal points.

Those two types are `f32` and `f64` which contain 32 bits and 64 bits
respectively.

```
let version = 2.0;

let y: f32 = 3.0;
```

---

## Numeric Operations *

Rust supports the basic math operations you're used to: addition, subtraction,
multiplication, division, and remainder.

---

## Boolean

Two possible types: `true` or `false`.

```
let t = true;

let f: bool = false;
```

---

## Character Type

`char` is Rust's most primitive alphabetic type.
Note that `char` types are defined with single quotes instead of double quotes.

```
let z = 'z';

let poop = '💩';
```

---

## Character Type

Rust’s `char` type is four bytes in size and represents a Unicode Scalar Value,
which means it can represent a lot more than just ASCII. Accented letters;
Chinese, Japanese, and Korean characters; emoji; and zero-width spaces are all
valid char values in Rust.

---

## Compound Types

Compound types can group multiple values into a single type and Rust has two
of these types: tuples, and arrays.

---

## Tuples

Tuples are a general way to group any number of values with a variety of types.
Tuples have a fixed length and once declared, cannot grow or shrink.

```
let tup: (i32, f64, u8) = (350, 6.4, 1);

let (x, y, z) = tup;

let tree_fiddy = tup.0;
```

---

## Array

Unlike tuples, every element of an array must have the same type.
Rust arrays differ slightly because they have a fixed length.

```
let arr = [1, 2, 3, 4, 5];
```

---

## Array

Useful for when you want data allocated on the stack instead of the heap or
if you want to ensure you always have a fixed number of elements.

```
let months = [
    "January", "February", "March", 
    "April", "May", "June", "July",
    "August", "September", "October", 
    "November", "December"
];
```

---

## Array Access

Like other languages, you can access an array element by index.
Rust indices start at 0.

```
let arr = [1, 2, 3];
let first_el = arr[0];
```

---

## Functions

Functions are defined with `fn` and have a set of parens after the function
name. The curly brackets then tell the compiler where the function body
begins and ends. Order of functions does not matter.

---

## Function parameters

```
fn add(x: u32, y: u32) {
  println!("total: {}", x + y);
}
```

---

### Statements and Expressions

Function bodies are made up of a series of statements optionally ending in an
expression. Rust is an expression-based language so this distinction is
is important.

---

### Statements and Expressions

Statements are instructions that perform some action but do not return a value.
Expressions evaluate to a resulting value.

Creating a variable and assigning a value with `let` is a statement.

---

### Statements and Expressions

In fact, the whole example is a statement as function definitions are also
statements.
```
fn main() {
    let y = 6;
    println!("y: {}", y);
}
```

---

### Statements and Expressions *

This differs from other languages such as C or Ruby where assignment returns
the value. In those languages, you can write `x = y = 6` and have both `x` and
`y` have the value of 6; this is not the case with Rust.

---

### Statements and Expressions

Here, `x+1` will evaluate to and return 6. 

```
fn main() {
    let x = 5;

    x + 1
}
```

---

### Statements and Expressions *

Note the missing semicolon.

In Rust, expressions **DO NOT** include ending semicolons. A semicolon
turns it into a statement and it will not return a value.

---

### Return Values 

Functions can return values to the code that calls them. We do not name the
return values, but we do declare the type after an arrow (`->`).

In Rust, the return value is synonymous with the value of the final expression
in the function.

---

### Return Values

You can return early from a function by using `return` but most functions in
Rust return the last expression implicitly.

```
fn pi() -> f64 {
    3.14159
}
```

---

### Comments

``` 
// this is a comment
```

```
// a bit longer
// and a more complicated
// version of a comment
// I wish they had better mulitline support
```

---

### Comments

```
fn main() {
    let one = 1; // comment can go here
}

fn less_main() {
    // but this might be better to read 
    let two = 2;
}
```

---

### Documentation Comments

```
/// Adds one to the number given.
///
/// # Examples
///
/// ```
/// let arg = 5;
/// let answer = my_crate::add_one(arg);
///
/// assert_eq!(6, answer);
/// ```
pub fn add_one(x: i32) -> i32 {
    x + 1
}
```

---

### Documentation Comments
```
cargo doc

cargo doc --open
```
---

![Image](./images/docs.png)

---

### Documenting Contained Items

These doc comments are main used for documenting the lib or main module as a
whole.

```
//! # My Crate
//!
//! `my_crate` is a collection of utilities to make 
//!  performing certain calculations more convenient.

/// Adds one to the number given.
// --snip--
```

---

![Image](./images/docs2.png)

---

### Controlling Flow

- if, if else, else if, if in let
- loop, while, for

---

### If and Else

```
let number = 3;

if number < 5 {
  println!("condition was true");
} else {
  println!("condition was false");
}
```

---
If arm must evaluate to a `bool`

```
let number = 3;

if number {
  println!("number was three");
}
```

---

Must be explicit

```
let number = 3;

if number != 0 {
  println!("number was something other than zero");
}
```

---

### Else if

```
let number = 6;

if number % 4 == 0 {
  println!("number is divisible by 4");
} else if number % 3 == 0 {
  println!("number is divisible by 3");
} else if number % 2 == 0 {
  println!("number is divisible by 2");
} else {
  println!("number is not divisible by 4, 3, or 2");
}
```

---

### if in a let statement

Because `if` is an expression, we can use it on the right side of a let
statement.

```
let condition = true;
let number = if condition { 5 } else { 6 };

println!("The value of number is: {}", number);
```

---

The potential values for each arm of the `if` must be the same type.

```
let condition = true;

let number = if condition { 5 } else { "six" };

println!("The value of number is: {}", number);
```

---

### Loop (loop-a-doop-a-doop)

`loop` executes a block of code over and over and over again until you force it
to stop.

```
loop {
  println!("again!");
}
```

---

### Returning values from loops

Add value you want to return after a `break` expression.

```
let mut counter = 0;

let result = loop {
  counter += 1;

  if counter == 10 {
    break counter * 2;
  }
};

println!("The result is {}", result);
```

---

### Condtional loops with `whlie`

Continues to loop while a condition is true. Calls `break` when the condition
ceases to be true.

```
let mut number = 3;

while number != 0 {
  println!("{}!", number);

  number -= 1;
}

println!("LIFTOFF!!!");
```

---

### More concise control with `for`

```
let a = [10, 20, 30, 40, 50];
let mut index = 0;

while index < 5 {
  println!("the value is: {}", a[index]);

  index += 1;
}
```

Works, but error prone and slow

---

```
let a = [10, 20, 30, 40, 50];

for element in a.iter() {
  println!("the value is: {}", element);
}
```

---

```
for number in (1..4).rev() {
  println!("{}!", number);
}
println!("LIFTOFF!!!");
```

---

### Ownership

##### Rust's central and most unique feature.

Programs must manage how they use a computer's memory while running.
Some do this with garbage collection that looks for unused memory;
others for the programmer to explicity allocate and free the memory.

---

### Ownership

Rust took a new path: memory is managed through a system of ownership with a
set of rules that the compiler checks at compile time

---

### The Stack and the Heap

Both the stack and the heap are parts of memory that are available to your
program to use at runtime, but they are structured differently.

---

### The Stack

The stack stores values in the order it gets them and removes them in the
opposite order. This is called last in, first out (LIFO).

---

### The Stack

Think of a stack of plates. When you add a plate, you put them on top, and when
you need a plate, you take it from the top. You cannot add or take from the
middle or top.

---

### The Stack

Adding is called *pushing onto the stack*, and removing is called
*popping off the stack*

---

### The Stack

All data stored on the stack must have a known, fixed size.

Any data with an unknown size at compile time or a size that could change
must be stored on the heap instead.

---

### The Heap

The heap is less organized. When using the heap, you request a certain amount
of space. The OS finds a spot that is big enough, marks it as in use, and
returns a pointer, which is an address back to that spot.

---

### The Heap

This is more like a restaurant. When you arrive, you give the count of people
in your group, then the staff finds a table that has enough seats and then
takes you there. If you have another member joins, the staff knows where you
are located and direct them to you.

---

### The Stack and the Heap

Pushing to and popping off the stack is faster than allocating on the heap.
The OS never has to search for a place for the new data; it's always on top.

Allocating on the heap requires the OS to find a spot and perform bookkeeping
to keep track of the location. Accessing it requires following the pointer.

---

### Rules of Ownership

- Each value in Rust has a variable that’s called its owner.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

---

### Variable Scope

The variable `s` refers to a string literal, where the value of the string is
hardcoded into the text of our program. The variable is valid from the point at
which it’s declared until the end of the current scope.

```
{                      // s is not valid here, it’s not yet declared
  let s = "hello";     // s is valid from this point forward

  // do stuff with s
}                      // this scope is now over, 
                       // and s is no longer valid
```

---

### More complex example, a `String`

Until now, we've been seeing string literals, where a string value is hardcoded
into the program. These are convenient and fast, but not very flexible. One
big reason is they are immutable and not every string value will be known at 
compile time. For instance, any user input.

---

### More complex example, a `String`

For these situations, Rust has `string`. This type is allocated on the heap
and because of that can, it can store an amount of text unknown at compile time.

```
let s = String::from("hello");
```

---

This kind of string can be mutated:

```
let mut s = String::from("hello");

s.push_str(", world!"); // push_str() appends a literal to a String

println!("{}", s); // This will print `hello, world!`
```

---

### Memory and Allocation

To support a mutable and growable string, we must allocate memory on the heap.

- OS must request the memory
- We must return this memory to the OS when we're done

---

### Memory and Allocation

We do the first part by using `String::from`. The implemention of string will
request it for us.

---

However, the second point is different. 

With a GC, the GC keeps track and cleans up memory that isn't being used.
Without a GC, we must handle that responsibility and that can be a difficult
task. Too late and you waste memory, too early and your variable will invalid.

---

```
{
  let s = String::from("hello"); // s is valid from here

  // do stuff with s
}                                // this scope is now over, 
                                 // and s is no longer valid
```

---

There is a natural point at which we can return the memory our `String` needs to
the operating system: when `s` goes out of scope. When a variable goes out of
scope, Rust calls a special function for us. This function is called `drop`, and
it’s where the author of String can put the code to return the memory. Rust
calls drop automatically at the closing curly bracket.

---

This seems simple right now, but the behavior of code can be unexpected in
more complicated situations when we want to have multiple variables use the
data we’ve allocated on the heap. Let’s explore some of those situations now.

---

### Variable and Data Interaction: `move`

Multiple variables can interact with the same data in different ways in Rust.

```
let x = 5;
let y = x;
```

---

We can probably guess what this is doing: “bind the value `5` to `x`; then make
a copy of the value in `x` and bind it to `y`.” We now have two variables, `x`
and `y`, and both equal `5`. This is indeed what is happening, because integers
are simple values with a known, fixed size, and these two `5` values are pushed
onto the stack.

---

But let's look at `String`:

```
let s1 = String::from("hello");
let s2 = s1;
```

---

![Image](./images/ownership-1.svg#svg)

---

The length is how much memory, in bytes, the contents of the `String` is
currently using. The capacity is the total amount of memory, in bytes, that the
`String` has received from the operating system.

---

```
let s2 = s1;
```

When we assign `s1` to `s2`, the String data is copied, meaning we copy the
pointer, the length, and the capacity that are on the stack. We do not copy the
data on the heap that the pointer refers to.

---

![Image](./images/ownership-2.svg#svg)

---

![Image](./images/ownership-3.svg#svg)

---

Earlier, we said that when a variable goes out of scope, Rust automatically
calls the `drop` function and cleans up the heap memory for that variable.

---

This is a problem: when `s2` and `s1` go out of scope, they will both try to free
the same memory. This is known as a double free error and is one of the memory
safety bugs we mentioned previously. Freeing memory twice can lead to memory
corruption, which can potentially lead to security vulnerabilities.

<!-- ownership example -->

---

Copying the pointer, length, and capacity without the actual data might sound
like a shallow copy from other languages, but because Rust invalidated the first
variable, it's known as a *move*.

---

![Image](./images/ownership-4.svg#svg)

---

Rust never automatically creates "deep" copies with data. Any automatic copying
Rust does can safely be assumed to be shallow and therefore inexpensive.

---
Can explicitly deeply copy with `clone`.
```
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```

---

### Copy trait

```
let x = 5;
let y = x;

println!("x = {}, y = {}", x, y);
```

---

Rust has a special annotation called the `Copy` trait that we can place on types
like integers that are stored on the stack.

---

If a type has the `Copy` trait, an older variable is still usable after
assignment. Rust won’t let us annotate a type with the `Copy` trait if the type,
or any of its parts, has implemented the `Drop` trait. If the type needs
something special to happen when the value goes out of scope and we add the
`Copy` annotation to that type, we’ll get a compile-time error.

---

### Types that are `Copy`


- All the integer types, such as u32.
- The Boolean type, bool, with values true and false.
- All the floating point types, such as f64.
- The character type, char.
- Tuples, if they only contain types that are also Copy. 
  For example, (i32, i32) is Copy, but (i32, String) is not.

---

### Ownership and functions

```
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);     // s's value moves into the function...
                            // ... and so is no longer valid here

    let x = 5;              // x comes into scope

    makes_copy(x);      // x would move into the function,
                        // but i32 is Copy, so it’s okay to still
                        // use x afterward

}
```

---

### Ownership and Return values

```
let s1 = gives_ownership(); // gives_ownership moves its return
                            // value into s1

let s2 = String::from("hello"); // s2 comes into scope

let s3 = takes_and_gives_back(s2);  

// s2 is moved into
// takes_and_gives_back, which also
// moves its return value into s3

// Here, s3 goes out of scope and is dropped. 
// s2 goes out of scope but was moved,
// so nothing happens. s1 goes out of scope and is dropped.
```

---

```
fn gives_ownership() -> String {  // gives_ownership will move its
                                  // return value into the function
                                  // that calls it

    // some_string comes into scope
    let some_string = String::from("hello"); 

    some_string                   // some_string is returned and
                                  // moves out to the calling
                                  // function
}
```

---

```
// takes_and_gives_back will take a String and return one
fn takes_and_gives_back(a_string: String) -> String { 
  // a_string comes into scope

    a_string  
    // a_string is returned and moves out to the calling function
}
```

---

Taking and returning ownership can be tedious.

```
fn main() {
    let s1 = String::from("hello");

    let (s2, len) = calculate_length(s1);

    println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}
```

---

### References

```
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

---

![Image](./images/references-1.svg#svg)

---

```
let s1 = String::from("hello");

let len = calculate_length(&s1);
```

```
// s is a reference to a String
fn calculate_length(s: &String) -> usize { 
    s.len()
} // Here, s goes out of scope. 
  // But because it does not have ownership of what
  // it refers to, nothing happens.
```

---

The scope for references is the same as any variable, but we do not drop
what the reference points to when it goes out of scope because we do not own
that value.

When passing parameters as references, we don't need to return because we never
own it.

---

In Rust, using references as function parameters is called *borrowing*.

You **WILL** "fight the borrow checker", especially in the beginning.

---

```
fn main() {
    let s = String::from("hello");

    change(&s);
}

fn change(some_string: &String) {
    some_string.push_str(", world");
}
```

<!-- mutatable references example -->

---

### Mutable references

```
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

---

Mutable references have one big restriction: you can have only one mutable
reference to a particular piece of data in a particular scope. This code will
fail:

```
let mut s = String::from("hello");

let r1 = &mut s;
let r2 = &mut s;

println!("{}, {}", r1, r2);
```

<!-- multiple mut references example -->

---

The benefit of having this restriction is that Rust can prevent data races at
compile time. A data race is similar to a race condition and happens when these
three behaviors occur:

- Two or more pointers access the same data at the same time.
- At least one of the pointers is being used to write to the data.
- There’s no mechanism being used to synchronize access to the data.

---

Data races cause undefined behavior and can be difficult to diagnose and fix
when you’re trying to track them down at runtime; Rust prevents this problem
from happening because it won’t even compile code with data races!

---

```
let mut s = String::from("hello");

let r1 = &s; // no problem
let r2 = &s; // no problem
let r3 = &mut s; // BIG PROBLEM

println!("{}, {}, and {}", r1, r2, r3);
```
<!-- mutable-and-immutable-references example -->

---

### Dangling References

In languages with pointers, it’s easy to erroneously create a dangling pointer,
a pointer that references a location in memory that may have been given to
someone else, by freeing some memory while preserving a pointer to that memory.

---

n Rust, by contrast, the compiler guarantees that references will never be
dangling references: if you have a reference to some data, the compiler will
ensure that the data will not go out of scope before the reference to the data
does.

---

```
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String {
    let s = String::from("hello");

    &s
}
```

<!-- dangling reference example -->

---

```
fn dangle() -> &String { // dangle returns a reference to a String

    let s = String::from("hello"); // s is a new String

    &s // we return a reference to the String, s
} // Here, s goes out of scope, and is dropped. Its memory goes away.
  // Danger!
```

---

```
fn no_dangle() -> String {
    let s = String::from("hello");

    s
}
```

---

### Slice type

Another data type that does not have ownership is the slice. Slices let you
reference a contiguous sequence of elements in a collection rather than the
whole collection.

Write a function that takes a string and returns the first word it finds in
that string. If the function doesn’t find a space in the string, the whole
string must be one word, so the entire string should be returned.

```
fn first_word(s: &String) -> ?
```

---

### String slices

A string slice is a reference to part of a `String`, and it looks like this:

```
let s = String::from("hello world");

let hello = &s[0..5];
let world = &s[6..11];
```

---

Similar to taking a reference to the whole `String` but with the extra `[0..5]`
bit. Rather than a reference to the entire `String`, it’s a reference to a
portion of the `String`.

---

We can create slices using a range within brackets by specifying
`[starting_index..ending_index]`, where `starting_index` is the first position
in the slice and `ending_index` is one more than the last position in the
slice.  Internally, the slice data structure stores the starting position and
the length of the slice, which corresponds to `ending_index` minus
`starting_index`. So in the case of `let world = &s[6..11];`, `world` would be
a slice that contains a pointer to the 7th byte (counting from 1) of `s` with a
length value of 5.

---

![Image](./images/string-slices-1.svg#svg)

---

With Rust’s .. range syntax, if you want to start at the first index (zero),
you can drop the value before the two periods. In other words, these are equal:

```
let s = String::from("hello");

let slice = &s[0..2];
let slice = &s[..2];
```

---

By the same token, if your slice includes the last byte of the String, you can
drop the trailing number. That means these are equal:

```
let s = String::from("hello");

let len = s.len();

let slice = &s[3..len];
let slice = &s[3..];
```

---

You can also drop both values to take a slice of the entire string. So these
are equal:

```
let s = String::from("hello");

let len = s.len();

let slice = &s[0..len];
let slice = &s[..];
```

---

```
fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}
```

---

### String Literals are Slices

Recall that we talked about string literals being stored inside the binary. Now
that we know about slices, we can properly understand string literals:

---

```
let s = "Hello, world!";
```

The type of `s` here is `&str`: it’s a slice pointing to that specific point of
the binary. This is also why string literals are immutable; `&str` is an
immutable reference.

---

### String slices as Parameters

Knowing that you can take slices of literals and `String` values leads us to one
more improvement on `first_word`, and that’s its signature:

```
fn first_word(s: &String) -> &str {
```

---

A more experienced Rustacean would write the signature shown below 
instead because it allows us to use the same function on both `&String` values
and `&str` values.

```
fn first_word(s: &str) -> &str {
```

---

If we have a string slice, we can pass that directly. If we have a `String`, we
can pass a slice of the entire `String`. Defining a function to take a string
slice instead of a reference to a `String` makes our code more general and useful
without losing any functionality.

---

String slices are special to strings but there are other types of slices.

```

let a = [1, 2, 3, 4, 5];

let slice = &a[1..3];
```

---

You will use this kind of slice for all sorts of other collections

---

### Collections

- vectors
- strings
- hash maps

---

### Vectors

A vector is of the type `Vec<T>`. 

Allow you to store more than one value in a single data structure that puts all
the values next to each other in memory.

A growable array basically.

They are useful when you have a list of items, such as the lines of text in a
file or a list of players for a game.

---

Note that we added a type annotation here. Because we aren’t inserting any
values into this vector, Rust doesn’t know what kind of elements we intend to
store. This is an important point. Vectors are implemented using generics.

```
let v: Vec<i32> = Vec::new();
```

---

For now, know that the `Vec<T>` type provided by the standard library can hold
any type, and when a specific vector holds a specific type, the type is
specified within angle brackets.

---

In more realistic code, Rust can often infer the type of value you want to
store once you insert values, so you rarely need to do this type annotation.
It’s more common to create a `Vec<T>` that has initial values, and Rust provides
the `vec!` macro for convenience. The macro will create a new vector that holds
the values you give it.

---

```
let v = vec![1, 2, 3];
```

---

### Updating a Vector

```
let mut v = Vec::new();

v.push(5);
v.push(6);
v.push(7);
v.push(8);
```

---

### Accessing a Vector

```
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];
println!("The third element is {}", third);

match v.get(2) {
  Some(third) => println!("The third element is {}", third),
    None => println!("There is no third element."),
}

```

---

### Iterating

```
let v = vec![100, 32, 57];

for i in &v {
  println!("{}", i);
}
```

---

```
let mut v = vec![100, 32, 57];

for i in &mut v {
  *i += 50;
}

```

---

### Strings

The `String` type, which is provided by Rust’s standard library rather than coded
into the core language, is a growable, mutable, owned, UTF-8 encoded string
type.

```
let mut s = String::new();
```

---

```
let data = "initial contents";

let s = data.to_string();

// the method also works on a literal directly:
let s = "initial contents".to_string();
```

Available on any type that implements the `Display` trait

---

```
let s = String::from("initial contents");
```

---

```
let mut s = String::from("foo");
s.push_str("bar");
```

---

### Concatenation

```
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2; // note s1 has been moved here and can no longer be used
```

---

### Things to explore on your own

- structs
- hash maps
- enums and pattern matching
- generics and lifetimes
- tests

---

### Resources

- https://doc.rust-lang.org/book/title-page.html
- 
