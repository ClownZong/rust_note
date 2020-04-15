[TOC]
# 与golang交互

## FFI
在汇编层做一致调用

## ABI
二进制层面的兼容约定。C语言ABI是唯一通用稳定的标准ABI。
> rust程序 > FFI > C语言ABI > 调用约定、内存布局、CPU指令集、二进制格式、其他。

## rust FFI
使用extern关键字标注。编译时由LLVM默认生成C-ABI。

## 编译原理
> 在一个编译模块中，通常包含了函数和全局数据的定义。函数和数据由符号来标识，一般有全局和静态之分。全局符号可以在模块间引用，而静态符号只能在当前模块引用。编译各个模块的时候，编译器的一项重要工作就是建立**符号表**。符号表中包含了模块的哪些符号是全局符号，哪些是静态符号，每个符号都会关联一个地址。在链接过程中，链接器会扫描各个编译模块的符号表，建立全局符号表，由此决定，符号在哪里被定义，以及在哪里被调用。这个过程叫作**符号解析**。除此之外，因为可执行文件和库的内存地址空间使用的差异，还需要进行**存储空间的分配**。地址重新分配之后，相应符号的引用也需要重新被调整，这个过程叫作**重定位**。经过符号解析、存储空间分配和重定位之后，链接过程就完成了，最终生成可执行文件或库。库分为静态库和动态库。

## 与其他语言交互流程
通过导出为C-ABI接口的静态库或动态库，然后其他语言链接该库，就可以实现语言间的相互调用。

## crate_type说明
> 编译时可以同时指定多个crate_type
> * --crate_type=bin 生成一个可执行文件，程序中要有main函数。
> * --crate_type=lib 生成rust库，默认生成rlib静态库。
> * --crate_type=rlib 生成rust静态库，由rust编译器来使用。
> * --crate_type=dylib 生成rust动态库，由rust编译器来使用。在linux上生成*.so文件，在mac上生成*.dylib文件，在windows上生成*.dll文件。
> * --crate_type=staticlib 生成静态系统库。rust永远不会链接该类型库，主要用于和C语言进行链接，达成和其他语言交互的目的。静态系统库在Linux和mac上会创建*.a文件，在windows上会创建*.lib文件。
> * --crate_type=cdylib 生成动态系统库。用于生成C接口，和其他语言交互。在linux上创建*.so文件，在mac上生成*.dylib文件，在Windows上生成*.dll文件。


## golang调rust函数

> $ cargo new --lib go_invoke_rust

go_invoke_rust代码目录结构

<pre>

|--Cargo.toml
|--src
   |--lib.rs
   |--go_invoke_rust.h
|--go_src
   |--main.go


</pre>

## rust调C函数

``` rust
extern "C" {
    fn isalnum(input: i32) -> i32;
}

fn main() {
    unsafe {
        println!("Is 3 a number? the answer is: {}", isalnum(3));
        // println!("Is 'a' a number? the answer is: {}", isalnum('a'));
    }
}
```