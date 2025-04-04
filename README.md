# project-rust
Cargo Workspaces In Rust

## Creating a workspace
```
mkdir add
cd add
```
- Create filename: Cargo.toml
```
[workspace]
resolver = "2"
```
- Create first crate: adder
```
cargo new adder
```
- Create second crate: add_one
```
cargo new add_one --lib
```
-Your add directory should now have these directories and files:
```
├── Cargo.lock
├── Cargo.toml
├── add_one
│   ├── Cargo.toml
│   └── src
│       └── lib.rs
├── adder
│   ├── Cargo.toml
│   └── src
│       └── main.rs
└── target
```
- Modified filename: adder/Cargo.toml
```
[dependencies]
add_one = { path = "../add_one" }
```
- Modified filename: adder/src/main.rs
```
fn main() {
    let rs = add_one::add(12,13);
    println!("Hello, world! result add {}", rs);
}
```
- Let’s build the workspace by running cargo build in the top-level add directory!
```
cargo build
```
- To run the binary crate from the add directory, we can specify which package in the workspace we want to run by using the -p argument and the package name with cargo run:
```
cargo run -p adder
```
- Adding a Test to a Workspace
- Filename: add_one/src/lib.rs
```
pub fn add(left: u64, right: u64) -> u64 {
    left + right
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        let result = add(2, 2);
        assert_eq!(result, 4);
    }
}
```
- Now run cargo test in the top-level add directory. Running cargo test in a workspace structured like this one will run the tests for all the crates in the workspace:
```
cargo test
```
