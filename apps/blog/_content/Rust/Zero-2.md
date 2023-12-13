---
title: 'Rust项目实践(2)'
subtitle: '记录一下从零开始使用Rust开发项目'
date: 2023-12-13 17:00:00
category: 'Rust'
---

安装好 actix-web 后安装cargo-expand的时候报错了

## cargo-expand

```shell
cargo install cargo-expand
```

error: could not compile `cargo-expand` (bin "cargo-expand") due to previous error
error: failed to compile `cargo-expand v1.0.74`, intermediate artifacts can be found at `C:\Users\123\AppData\Local\Temp\cargo-installV3nuTF`.
To reuse those artifacts with a future compilation, set the environment variable `CARGO_TARGET_DIR` to that path.

这个问题可能是因为 cargo expand 命令需要 Rust 的 Nightly 版本才能正常工作，而默认的 Rust 版本是 Stable1。在 Nightly 版本中，rustc 工具支持 -Z 选项，而该选项在 Stable 版本中是禁用的，因此需要切换到 Nightly 版本。

```shell
rustup update #升级 Rustup 工具
rustup install nightly #安装 Nightly 版本
rustup show #查看是否正常安装
rustup override set nightly #进入到项目的根目录并激活Nightly版本
cargo expand #重新执行命令
```