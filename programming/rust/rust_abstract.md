---
tags: rust
---
# Overview

Rust is a low level programming capable of ignoring the memory allocation problems. It does this by using the ownership and borrowing system. The trade-off is that the programmer must be extremely aware of how values are pointed to, particularly values that are stored on the process's heap.

## Content

There are two main literature that teaches you Rust, and one exercise based teaching tool. The two books are both created by the Rust foundation, one of them is the **Rust Book** and the other one is **Rust by Examples**. They have similar content, with **Rust Book** being more content based, and **Rust by Example** being much more example based (more code examples, and less text). The example based teaching tool is called **Rustlings** and it provides an environment with many incorrect code in which the user will debug.

I personally recommend starting up with **Rustlings** and then reading the other two citation as you go when you are learning **Rust**.

## Table of Content

- Rust Book
	- [6. Enums](rust_book/ch06_00_enums.md)
	- [10. Modules](rust_book/ch10_00_modules.md)
- Rust by Example
	- [19.2 Vectors](rust_by_example/ch19_02_vectors.md)
- Resources
	- [`String`](rust_string.md)

## Citation

- [Rust Book](https://doc.rust-lang.org/book/)
- [Rust by Example](https://doc.rust-lang.org/rust-by-example/)
- [Rustlings](https://github.com/rust-lang/rustlings)