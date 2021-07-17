# serde-frontmatter
[![Crates.io](https://img.shields.io/crates/v/serde-frontmatter)](https://crates.io/crates/serde-frontmatter) 
[![Docs.rs](https://docs.rs/serde-frontmatter/badge.svg)](https://docs.rs/serde-frontmatter) 
[![Build](https://github.com/Ewpratten/serde-frontmatter/actions/workflows/build.yml/badge.svg)](https://github.com/Ewpratten/serde-frontmatter/actions/workflows/build.yml)
[![Clippy](https://github.com/Ewpratten/serde-frontmatter/actions/workflows/clippy.yml/badge.svg)](https://github.com/Ewpratten/serde-frontmatter/actions/workflows/clippy.yml)
[![Audit](https://github.com/Ewpratten/serde-frontmatter/actions/workflows/audit.yml/badge.svg)](https://github.com/Ewpratten/serde-frontmatter/actions/workflows/audit.yml)


This crate is a Rust library for using the [Serde](https://github.com/serde-rs/serde) serialization framework with Jekyll-style front matter.

## Examples

```rust
use serde::{Deserialize, Serialize};

#[derive(Deserialize, Serialize, PartialEq, Debug)]
pub struct MyData {
    pub title: String
}

fn main() {
    // Serialize
    let front_matter = MyData { title: "Hello, World!".to_string() };
    let content = "This is some content";
    let output = serde_frontmatter::serialize(front_matter, content).unwrap();
    assert_eq!("---\ntitle: \"Hello, World!\"\n\n---\nThis is some content", output);

    // Deserialize
    let input = "---\ntitle: Hello, World!\n---\nThis is some content";
    let (front_matter, content) = serde_frontmatter::deserialize::<MyData>(input).unwrap();
    assert_eq!(front_matter, MyData { title: "Hello, World!".to_string() });
    assert_eq!(content, "\nThis is some content");
}
```