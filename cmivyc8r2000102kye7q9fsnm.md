---
title: "📝 Article 6: Building My First Real Rust Function — first_word() — and What It Taught Me About Slices"
seoTitle: "Rust Function Insights: first_word() and Slices"
seoDescription: "Enhance Rust skills by learning `first_word()`, slices, references, UTF-8 complexities, and safe borrowing"
datePublished: Sun Dec 07 2025 16:43:41 GMT+0000 (Coordinated Universal Time)
cuid: cmivyc8r2000102kye7q9fsnm
slug: article-6-building-my-first-real-rust-function-firstword-and-what-it-taught-me-about-slices
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1765125794568/82568d89-ff47-40ae-8bcb-85fc73e1c4c7.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1765125808897/3c3a49c7-ad32-4f64-9f50-df22d426df39.png
tags: rust

---

Out of all the exercises I’ve done in Rust so far, the `first_word()` function was the most eye-opening.

It seems simple:

> “Given a string, return everything before the first space.”

But while building it, I learned four major Rust concepts at once:

* `&str` slices
    
* borrowed references
    
* UTF-8 and why indexing isn’t trivial
    
* returning references safely
    

Let me walk you through the journey.

---

# ⭐ The Goal

```rust
let s = "hello world";
let w = first_word(s);  

println!("{}", w); // "hello"
```

We want to scan the string and return the part up to the first space — without taking ownership, without allocating new memory, and without cloning.

Rust makes this possible *because* of slices.

---

# 🔍 Step 1: What is a Slice?

A slice (`&str`) is a **view into part of a string**.

Example:

```rust
let s = String::from("hello world");
let slice = &s[0..5];
println!("{}", slice); // "hello"
```

Important facts:

* `slice` does **not own** the data
    
* it only stores a **pointer** + **length**
    
* the data still lives inside `s`
    

So a slice is extremely cheap and fast.

---

# 🔥 Step 2: Why Can't We Just Index Characters?

Because Rust strings are **UTF-8 encoded**.

That means:

* some characters are 1 byte
    
* some are 2 bytes
    
* some are 4 bytes
    

So `"😊"` looks like 1 character but is actually 4 bytes.

Indexing by character becomes complicated.

This is why Rust does not let you do:

```rust
s[2] // ❌ invalid
```

Instead, we work with bytes.

---

# ⭐ Step 3: The Beginner-Friendly `first_word()` Implementation

Here’s the version I finally understood clearly:

```rust
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes(); // turn into byte array

    let mut index = 0;

    while index < bytes.len() {
        if bytes[index] == b' ' { // space found
            return &s[..index];   // return slice
        }

        index += 1;
    }

    &s[..] // no space → whole string
}
```

This function:

* takes a **borrowed string slice** (`&str`)
    
* scans it byte by byte
    
* returns a **borrowed slice** pointing inside the original string
    

No ownership is taken.  
No memory is allocated.  
No cloning.  
No copies.

Just pure, efficient slicing.

---

# 🧠 Key Lessons I Learned

### 1️⃣ A function can return a reference ONLY if the caller owns the data

This is why `first_word()` takes `&str` instead of creating its own `String`.

Returning a slice into **local data** would be invalid.

Rust prevents this automatically.

---

### 2️⃣ `&str` slices are zero-cost

They do not copy the string.  
They do not allocate memory.  
They are just pointers.

This makes Rust extremely efficient for text processing.

---

### 3️⃣ Strings are UTF-8, slicing must be careful

You cannot assume that each “character” is 1 byte.  
Working with `.as_bytes()` simplifies scanning.

---

### 4️⃣ Borrowing protects us

The returned slice cannot outlive the original string.

This prevents returning invalid memory.

Example of invalid code (Rust prevents it):

```rust
fn bad() -> &str {
    let s = String::from("hello");
    &s[..] // ❌ invalid, s is dropped here
}
```

---

### 5️⃣ Returning slices is more efficient than returning new Strings

This is why many Rust library functions return `&str`.

Returning slices avoids copying.

---

# 🧩 A More Idiomatic Version (For Later)

Once I learn more, Rust code often looks like this:

```rust
fn first_word(s: &str) -> &str {
    s.split_once(' ').map(|(first, _)| first).unwrap_or(s)
}
```

Or using `find`:

```rust
if let Some(space) = s.find(' ') {
    &s[..space]
} else {
    s
}
```

But the beginner version is perfect to understand how slices work under the hood.

---

# 🎉 Why This Function Matters

Building `first_word()` forced me to understand:

* how Rust treats strings
    
* what a slice actually is
    
* how references work
    
* how lifetimes protect us
    
* why borrowing rules exist
    

It’s the first moment where Rust’s design clicked for me.

If you can understand `first_word()`, you’re ready for:

* structs
    
* enums
    
* lifetimes
    
* iterators
    
* ownership in more complex scenarios
    

This is a major milestone.

---

# ⭐ What’s Next in the Series?

Up next, we move into data structures and real Rust programming:

# 📝 **Article 7: Structs and Enums — How Rust Builds Real-World Data Models**

This will cover:

* defining your own types
    
* building methods (`impl`)
    
* modeling real applications with enums
    
* understanding how Rust stores structured data