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

> 如果有关联文件，比如mod的文件，rustc编译的时候也不需要指出这个文件，这和C编译器不同。rust以包(crate)为编译单元。

> rustc lints 用来帮助编写出更好的代码，有allow < warning < deny < forbid 提示。

## 编译原理
> 在一个编译模块中，通常包含了函数和全局数据的定义。函数和数据由符号来标识，一般有全局和静态之分。全局符号可以在模块间引用，而静态符号只能在当前模块引用。编译各个模块的时候，编译器的一项重要工作就是建立**符号表**。符号表中包含了模块的哪些符号是全局符号，哪些是静态符号，每个符号都会关联一个地址。在链接过程中，链接器会扫描各个编译模块的符号表，建立全局符号表，由此决定，符号在哪里被定义，以及在哪里被调用。这个过程叫作**符号解析**。除此之外，因为可执行文件和库的内存地址空间使用的差异，还需要进行**存储空间的分配**。地址重新分配之后，相应符号的引用也需要重新被调整，这个过程叫作**重定位**。经过符号解析、存储空间分配和重定位之后，链接过程就完成了，最终生成可执行文件或库。库分为静态库和动态库。

## 交叉编译
> 在一个平台上生成另一个平台上可运行的程序。比如x86上编译在ARM上运行的程序。

