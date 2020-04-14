# 初探rust编译

## rustc

[rustc 官方文档](https://doc.rust-lang.org/rustc/index.html)

> 从cargo源码中看到 cargo build，中调用compile实际走的是rustc

> cargo build --verbose

<pre>
Compiling test_rustc v0.1.0 (D:\lang\rust\rust_note\test_rustc)
     Running `rustc --crate-name test_rustc --edition=2018 src\main.rs --error-format=json --json=diagnostic-rendered-ansi --crate-type bin --emit=dep-info,link -C debuginfo=2 -C metadata=55868cec4545e1a7 --out-dir D:\lang\rust\rust_note\test_rustc\target\debug\deps -C incremental=D:\lang\rust\rust_note\test_rustc\target\debug\incremental -L dependency=D:\lang\rust\rust_note\test_rustc\target\debug\deps`
    Finished dev [unoptimized + debuginfo] target(s) in 2.08s
</pre>

> rust内置编译器，rustc

> * rustc main.rs
> * .\main.exe

> 如果有关联文件，比如mod的文件，rustc编译的时候也不需要指出这个文件，这和C编译器不同。

> rustc lints 用来帮助编写出更好的代码，有allow < warning < deny < forbid 提示。