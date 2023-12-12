---
title: 'Rust项目实践(1)'
subtitle: '记录一下从零开始使用Rust开发项目'
date: 2023-12-12 17:00:00
category: 'Rust'
---

尝试通过Rust开发一下项目，根据书本《Zero to Production in Rust》来操作并且提取其中实操的要点。

## cargo-watch

```shell
cargo install cargo-watch
```

通过安装了cargo-watch，我们就可以修改代码的同时自动编译并且运行，不需要每次更改代码后再运行。

```shell
cargo watch -x check
```

如果我们 确实 需要深度复制 String 中堆上的数据，而不仅仅是栈上的数据，可以使用一个叫做 clone 的通用函数。

也可以这么做：
```shell
cargo watch -x check -x test -x run
```

这样由cargo check检查代码后，启动cargo test并且进入cargo run。

## 持续集成

持续集成可以自动检查每一次git commit，如果出错就不能合并到主分支，同时也可以进行代码风格检查，格式化等。

```shell
cargo install cargo-tarpaulin
```

cargo-tarpaulin是一个为Rust编程语言设计的代码覆盖率工具。它可以帮助开发者了解测试覆盖了代码的哪些部分，哪些部分没有被测试覆盖，从而帮助开发者提高代码的测试覆盖率，提高代码质量。

```shell
cargo tarpaulin --ignore-tests
```

```shell
rustup component add clippy
```

clippy是Rust编程语言的一个官方lint工具，它可以检查Rust代码并指出可能的错误、代码风格问题、不符合Rust习惯的编码方式等问题。

```shell
cargo clippy
```

```shell
rustup component add rustfmt
```
rustfmt是Rust的官方代码格式化工具，它可以自动将Rust代码格式化为一致的风格。它的目的是使Rust代码更易读、易写和易于维护，同时减少代码审查中关于代码风格的争论。

可以通过rustfmt.toml文件来设定好固定格式。

```shell
cargo install cargo-audit
```

cargo-audit会下载和解析RustSec的Advisory Database，这是一个包含已知Rust包漏洞的数据库。然后，它会检查Cargo.lock文件中列出的每个依赖项，看看它们是否存在于Advisory Database中。如果存在，cargo-audit会报告这些漏洞，并提供一些关于漏洞的详细信息，如漏洞的描述、影响、修复方法等。