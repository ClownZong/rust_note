# 初探rust编译

## rustc

[rustc 官方文档](https://doc.rust-lang.org/rustc/index.html)

> 从cargo源码中看到 cargo build，中调用compile实际走的是[ops compile](https://github.com/rust-lang/cargo/blob/master/src/cargo/ops/cargo_compile.rs)

> rust内置编译器，rustc