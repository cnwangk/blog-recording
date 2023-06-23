---
title: 程序人生：人生中的第一个Rust应用程序
date: 2023-03-24 21:11:03
tags: Rust
categories: 
- [web开发]
---


Linux（CentOS-Stream-9）平台相对容易点，RHEL系列使用yum或者dnf管理工具安装Rust环境即可体验。

Rust官网：[https://www.rust-lang.org/zh-CN/learn/get-started](https://www.rust-lang.org/zh-CN/learn/get-started)

[![ppBKbA1.png](https://s1.ax1x.com/2023/03/24/ppBKbA1.png)](https://imgse.com/i/ppBKbA1)



如果你只是想在Windows环境体验Rust，可能比较麻烦，需要获取vs_BuildTools。



体验简易步骤如下。



### Rust初体验：hello rust

1、安装rust环境

```bash
yum -y install rust.x86_64
```

2、新建rust工作空间
```bash
mkdir rust_workspace
cd rust_workspace/
```

3、进入rust工作空间
```bash
mkdir projects
cd projects/
```

4、编写rust版hello world

编写rust脚本：
```bash
vim main.rs
```

写入如下内容：
```bash
fn main(){
    println!("hello rust!!!");
 }
```
保存退出： 
```bash
:wq
```

5、编译man.rs
```bash
rustc main.rs
```

6、执行main
```bash
./main
hello rust!!!
```
看到 hello rust!!! 证明体验完成。





### Rust初体验：cargo

1、安装cargo

```bash
yum -y install cargo
```



2、初始化项目:hello-rust

```bash
cargo new hello-rust
cd hello-rust/
```



3、运行项目

```bash
cargo run 
   Compiling hello-rust v0.1.0 (/opt/rust_workspace/hello-rust)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32s
     Running `target/debug/hello-rust`
Hello, world!
```



4、Cargo.toml追加内容

```bash
[dependencies]
ferris-says = "0.2"
```
这一步，引入了依赖(dependencies)库：ferris-says



5、main.rs填充内容

```bash
  use ferris_says::say; // from the previous step
  use std::io::{stdout, BufWriter};
 
  fn main() {
      println!("Hello, world!");
 
      let stdout = stdout();
      let message = String::from("Hello fellow Rustaceans!");
      let width = message.chars().count();
 
      let mut writer = BufWriter::new(stdout.lock());
      say(message.as_bytes(), width, &mut writer).unwrap();
  }
```



6、运行程序：cargo run

```bash
[root@Centos9-Stream hello-rust]# cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.03s
     Running `target/debug/hello-rust`
Hello, world!
 __________________________
< Hello fellow Rustaceans! >
 --------------------------
        \
         \
            _~^~^~_
        \) /  o o  \ (/
          '_   -   _'
          / '-----' \
```



看到上面的效果，难道不想体验一下么？



### 配置vim：rust.vim

如果你没有安装 vim-plug 插件，请先安装：[https://github.com/junegunn/vim-plug](https://github.com/junegunn/vim-plug)



如果你和我一样使用的是centos-9-stream，可以下载 plug.vim，复制到如下目录：

```bash
cp plug.vim /usr/share/vim/vim82/autoload/
```

重启vim即可生效。



**rust.vim开源仓库地址**：[https://github.com/rust-lang/rust.vim](https://github.com/rust-lang/rust.vim)



**安装rust插件：**

```bash
Plug 'rust-lang/rust.vim'
```



**vim基本用法**：可以在站内搜索 vim入门实战。


希望对你有所帮助哟！

——END——
