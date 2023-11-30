## Getting started

### Rust Web framework: actix-web

### Cargo

```
cargo new [project_name]
cargo run
```

## Manual Memory Management

### Main concept

1. Stack
2. Heap
3. Pointers
4. Smart Pointers

### Stack

- It's a special region of the process memory that stores variables created by each function
- For every function call a new stack frame is allocated on top of the current one.
- The size of every variable on the stack has to be known at compile time
- When a function exists it's stack frame is released

```
FUNCTION main {
	INTEGER a = 2
	CALL stack_only(a)
}

FUNCTION stack_only(INTEGER b) {
	INTEGER c = 3
}

```

- The size of stack frame depends on the machine. (size limit)
- Stack overflow exception

```
FUNCTION infinite {
	CALL infinite
}

```

### Heap

- It's a region of the process memory that is NOT automatically managed.
- It has no size restrictions.
- It's accessible by any function, anywhere in the program.
- Heap allocations are expensive and we should avoid them when possible.

```
FUNCTION main {
	INTEGER a = 2
	CALL stack_only(a)
}

FUNCTION stack_only(INTEGER b) {
	INTEGER c = 3
	CALL stack_and_heap
}

FUNCTION stack_and_heap {
	INTEGER d = 5
	POINTER e = ALLOCATE INTEGER 7
	DEALLOCATE e
}

```

![[Pasted image 20220331024138.png]]

### Smart Pointer

- It's a wrapper around a raw pointer providing additional capabilities.
- When stack frame is released, the memory is disallocated.
- The type of smart pointer is BOX
- My opinion: No need DEALLOCATE

```
FUNCTION main {
	INTEGER a = 2
	CALL stack_only(a)
}

FUNCTION stack_only(INTEGER b) {
	INTEGER c = 3
	CALL stack_and_heap
}

FUNCTION stack_and_heap {
	INTEGER d = 5
	POINTER e = SMART_POINTER(7)
}

```

### Explore the Memory Layout in GDB

- My Opinion: Debug Tool to see memory layout

```
gdb project_name
> list # source code
> b func_name # breakpoint
> r # go to breakpoint
> bt 2
> info locals

```

## Building a Command Line Application

### Introduction

- Functions
- Basic Data Types
- Standard Library
- Memory Ownership

### Basic Data Types

1. Booleans
2. Characters
3. Integers
4. Floats
   ![[Pasted image 20220401032257.png]]

### Functions

```
main : special function
fn main() {
	println!("Hello, world!");

	calculate_weight_on_mars(100.0);
}

fn calculate_weight_on_mars(weight: f32) -> f32 {
	return 50.0;
	// 50.0
}

```

### Macros

```
fn main() {
	println!("Weight on Mars : {}kg", calculate_weight_on_mars(100.0));
}

fn calculate_weight_on_mars(weight: f32) -> f32 {
	(weight / 9.81) * 3.711
}

```

### Mutability

```
fn main() {
	let mars_weight = calculate_weight_on_mars(100.0);
	mars_weight = mars_weight * 1000.0; // ERROR because it's immutable variable
	println!("Weight on Mars : {}kg", mars_weight);
}

fn calculate_weight_on_mars(weight: f32) -> f32 {
	(weight / 9.81) * 3.711
}

```

### The standard library

```
use std::io;

fn main() {
	let mut input = String::new();
	io::stdin().read_line(&mut input);
	let mars_weight = calculate_weight_on_mars(100.0);
	mars_weight = mars_weight * 1000.0; // ERROR because it's immutable variable
	println!("Weight on Mars : {}kg", mars_weight);
}

fn calculate_weight_on_mars(weight: f32) -> f32 {
	(weight / 9.81) * 3.711
}

```

### Ownership

```
use std::io;

fn main() {
	let mut input = String::new();
	let mut s = input;
	io::stdin().read_line(&mut input);
	let mars_weight = calculate_weight_on_mars(100.0);
	mars_weight = mars_weight * 1000.0; // ERROR because it's immutable variable
	println!("Weight on Mars : {}kg", mars_weight);
}

fn calculate_weight_on_mars(weight: f32) -> f32 {
	(weight / 9.81) * 3.711
}

```

- Each value in Rust is owned by a variable
- When the owner goes out of scope, the value will be deallocated
- There can only be ONE owner at a time.

### References and Borrowing

```
use std:io

fn main() {
	let mut input = String:new();

	io::stdin().read_line(&mut input).unwrap();

	borrow_string(&input);
	own_string(input);
}

fn borrow_string(s: &String) {
	println!("{}", s);
}

fn own_string(s: String) {
	println!("{}", s);
}

```

### Complete code

```
use std::io

fn main() {
	let mut input = String::new();
	io::stdin().read_line(&mut input).upwrap();
	let weight: f32 = input.trim().parse().unwrap();
	let mars_weight = calculate_weight_on_mars(weight);
	println!("Weight on Mars: {}kg", mars_weight);
}

fn calculate_weight_on_mars(weight: f32) -> f32 {
	(weight / 9.81) * 3.711;
}

```

### Struct

```
fn main() {
	let server = Server::new("127.0.0.1:8080");
	server.run();
}

struct Server {
	addr: String,
}

impl Server {
	fn new(addr: String) -> Self {
		Self {
			addr: addr
		}
	}

	fn run(self) {

	}
}
```
