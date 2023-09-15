---
title: '关于公司突然说要在Sei开发...'
subtitle: '希望这次不是拍脑袋的决定'
date: 2023-09-06 11:00:00
category: 'Work'
---

前天晚上 Adam 突然给我发微信说在 Sei 上面开发，项目方会给到比较大的支持，让我部署几个合约玩玩。于是我立马查了下 Sei 的开发资料，是用 Cosmos 的生态，CosmWasm 是用于编写 Rust 智能合约的库。之前学的半桶水 Rust 正好用上了。

## 安装环境

昨天差不多花了我一天去弄环境，先把依赖项安装好，

go docker jq git cmake gcc rustup make。

公司电脑用的是 Windows，

一开始我尝试用 Power Shell 去安装。

结果各种安装不成功，又是 choco 安装的 go 版本不正确，又是 go mod tidy，

最后我在 WSL Ubuntu 上安装了 3.0.8 版本的 Seid。（头大）

## 开始尝试学习 Rust 智能合约

据文档所说，利用 Cosmos 的 Counter 合约来练练手先。

结果 cargo wasm 又报错

> > error: package `sec1 v0.7.3` cannot be built because it requires rustc 1.65
> > or newer, while the currently active rustc version is 1.61.0.

升级 Ubuntu 的 rust。

升级完成后按照文档所说的进行 cargo unit-test。通过

但是 cargo wasm 又不通过了，要去 CosmWasm 的 github 找解决办法

头疼。执行

```bash
rustup target add wasm32-unknown-unknown
```

又 OK 了

然后启动 docker

```bash
docker run --rm -v "$(pwd)":/code --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target --mount type=volume,source=registry_cache,target=/usr/local/cargo/registrycosmwasm/rust-optimizer:0.12.11
```

然后老报错，

在 Ubuntu 上面就报

```
docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
```

在 PowerShell 上面就报

```
basename: The term 'basename' is not recognized as a name of a cmdlet, function, script file, or executable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
docker: invalid reference format.
```

@#!$@$@%!%#

然后我看到这款优化器https://github.com/mandrean/cw-optimizoor，安装试试先。
