# WebAssembly
简称WASM，由Google、MicroSoft、Mozilla等公司联合发起的一个面向Web的通用二进制和文本格式项目。
意义：在客户端提供了一种接近本地运行速度的多种语言编写代码的方式。WebAssembly是面向Web的汇编，相当于一种中间语言。
应用场景：加密算法、渲染、图像/音频/视频的处理。

> WebAssembly实际上是一个JavaScript对象，由Js分配wasm使用的整个内存空间，Js的GC对其管理，不会出现内存泄漏的情况。wasm的优点：二进制体积小、不受js约束，可利用更多CPU指令。wasm缺点：目前不支持DOM操作。

> Web只是WASM的应用场景之一。还可以用在桌面图形化、区块链合约、操作系统内核等。