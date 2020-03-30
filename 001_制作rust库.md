# 制作rust库

## 创建库项目

> 使用cargo new curve25519 --lib会自动创建一个库项目。
> * cargo new xxx (系统会自动加--bin，创建一个二进制项目)
> * cargo new xxx --lib 创建一个库项目

### 文件结构

``` pre
--curve25519
 |--src
 |---|--lib.rs
 |--Cargo.toml

```

### Cargo.toml
 
 ``` toml
[package]
name = "curve25519"
version = "0.1.0"
authors = ["ClownZong <2829294028@qq.com>"]
edition = "2018"

[dependencies]

 ```

### src/lib.rs

``` rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        assert_eq!(2 + 2, 4);
    }
}

```

## 测试库项目

> cargo test
