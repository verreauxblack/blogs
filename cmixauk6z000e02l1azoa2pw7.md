---
title: "📝 Article 7: Structs and Enums — How Rust Builds Real-World Data Models"
seoTitle: "Rust Structs and Enums for Data Modeling"
seoDescription: "Rust's structs and enums create real-world data models with zero-cost, safe, expressive combinations for efficient application design"
datePublished: Mon Dec 08 2025 15:21:37 GMT+0000 (Coordinated Universal Time)
cuid: cmixauk6z000e02l1azoa2pw7
slug: article-7-structs-and-enums-how-rust-builds-real-world-data-models
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1765207264818/77975e63-9717-44f2-8b61-9cf0c6444a94.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1765207284287/444320f5-7eb1-475c-bebf-d5c2d3971fd3.png
tags: rust

---

If Ownership and Borrowing are Rust’s *rules*,  
then **Structs and Enums are Rust’s *building blocks***.

They are how Rust models everything in real-world applications:

* API responses
    
* App state
    
* Configuration objects
    
* Database models
    
* Messages in async systems
    
* Errors
    
* Game entities
    
* UI components
    

And the amazing part?  
Unlike many languages, struct + enum combinations in Rust are **zero-cost, safe, and extremely expressive**.

Let’s break them down clearly.

---

# ⭐ Part 1 — Structs: Rust’s Way of Grouping Related Data

A struct is like an object in JS or a class without inheritance.

Example:

```rust
struct Book {
    title: String,
    author: String,
    pages: u32,
}
```

This groups fields into a single, meaningful type.

Creating a struct:

```rust
let book = Book {
    title: String::from("Learning Rust"),
    author: String::from("RAJ"),
    pages: 32,
};
```

Accessing fields:

```rust
println!("{} by {}", book.title, book.author);
```

### ✔ Structs group data

### ✔ Fields have explicit types

### ✔ They live on the stack, but their owned values may be on the heap

Perfect for modeling objects in an application.

---

# ⭐ Part 2 — Adding Behavior With `impl`

Structs can have methods using `impl`, similar to classes:

```rust
impl Book {
    fn summary(&self) {
        println!("{} by {}", self.title, self.author);
    }

    fn add_pages(&mut self, n: u32) {
        self.pages += n;
    }
}
```

Calling methods:

```rust
book.summary();
```

### ✔ `&self` → read-only

### ✔ `&mut self` → can modify struct

### ✔ methods belong to the struct, not global space

This gives Rust a clean and object-oriented feel — without inheritance.

---

# ⭐ Part 3 — Enums: Representing Different “Shapes” of Data

Enums let you express **multiple possible states** of a value.

Example:

```rust
enum Status {
    Active,
    Inactive,
    Pending(String),
}
```

Rust enums are far more powerful than enums in most languages:

* They can store data
    
* They can have multiple forms
    
* They enforce exhaustive pattern matching
    
* They avoid invalid states
    

Using the enum:

```rust
let s1 = Status::Active;
let s2 = Status::Pending(String::from("Waiting for approval"));
```

Enums help express logic clearly and safely.

---

# ⭐ Part 4 — Pattern Matching: Handling Enum Variants

Rust's `match` statement is one of its strongest features.

```rust
fn print_status(status: Status) {
    match status {
        Status::Active => println!("Active"),
        Status::Inactive => println!("Inactive"),
        Status::Pending(msg) => println!("Pending: {}", msg),
    }
}
```

### ✔ Compiler forces you to handle every variant

### ✔ You can destructure data inside enum variants

### ✔ No missing cases → no bugs hiding

This gives Rust unmatched safety.

---

# ⭐ Part 5 — Combining Structs + Enums (Real Application Modeling)

Structs and enums work beautifully together.

Example: A Task Manager model:

```rust
enum Status {
    Active,
    Inactive,
    Pending(String),
}

struct Task {
    title: String,
    status: Status,
}
```

With methods:

```rust
impl Task {
    fn print(&self) {
        match &self.status {
            Status::Active => println!("{} is Active", self.title),
            Status::Inactive => println!("{} is Inactive", self.title),
            Status::Pending(msg) => println!("{} is {}", self.title, msg),
        }
    }
}
```

Usage:

```rust
let t1 = Task {
    title: String::from("Learn Rust"),
    status: Status::Active,
};

let t2 = Task {
    title: String::from("Deploy Project"),
    status: Status::Pending(String::from("Waiting for review")),
};

t1.print();
t2.print();
```

### ✔ Struct models the entity

### ✔ Enum models the state

### ✔ Pattern matching handles all possibilities

This pattern is used in:

* React-like UI state machines
    
* Server responses (Success, Error, Loading)
    
* Game engines (Alive, Dead, Attacking)
    
* Networking (Connected, Disconnected, Retry)
    
* Database operations
    

Rust’s type system lets you model **exactly** the states your program can be in — and prevents invalid ones.

---

# ⭐ Final Thoughts

Structs represent **data**.  
Enums represent **state**.  
Together, they allow you to build expressive, precise, bug-free models.

This combination is why Rust codebases feel:

* predictable
    
* easy to reason about
    
* resistant to bugs
    
* well-structured
    

Once you master structs and enums, you can design any domain model with confidence.

---

# 🚀 Coming Next:

Now that we finished Structs + Enums + Slices + Option/Result…

It’s time for:

# **Practical Rust: Building Functions That Return Option and Result**