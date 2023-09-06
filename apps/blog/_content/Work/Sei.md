---
title: '关于公司突然说要在Sei开发...'
subtitle: '希望这次不是拍脑袋的决定'
date: 2023-09-06 11:00:00
category: 'Work'
---

前天晚上Adam突然给我发微信说在Sei上面开发，项目方会给到比较大的支持，让我部署几个合约玩玩。于是我立马查了下Sei的开发资料，是用Cosmos的生态，CosmWasm 是用于编写Rust智能合约的库。之前学的半桶水Rust正好用上了。

## 安装环境

昨天差不多花了我一天去弄环境，先把依赖项安装好，

go docker jq git cmake gcc rustup make。

公司电脑用的是Windows，

一开始我尝试用Power Shell去安装。

结果各种安装不成功，又是choco安装的go版本不正确，又是go mod tidy，

最后我在WSL Ubuntu上安装了3.0.8版本的Seid。（头大）

## 开始尝试学习Rust智能合约

据文档所说，利用Cosmos的Counter合约来练练手先。

结果cargo wasm又报错

> > error: package `sec1 v0.7.3` cannot be built because it requires rustc 1.65 
> > or newer, while the currently active rustc version is 1.61.0.

升级Ubuntu的rust。

升级完成后按照文档所说的进行cargo unit-test。通过

但是cargo wasm又不通过了，要去CosmWasm的github找解决办法

头疼。执行

```bash
rustup target add wasm32-unknown-unknown
```

又OK了

然后启动docker

```bash
docker run --rm -v "$(pwd)":/code --mount type=volume,source="$(basename "$(pwd)")_cache",target=/code/target --mount type=volume,source=registry_cache,target=/usr/local/cargo/registrycosmwasm/rust-optimizer:0.12.11
```

然后老报错，

在Ubuntu上面就报

```
docker: Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?.
```

在PowerShell上面就报
```
basename: The term 'basename' is not recognized as a name of a cmdlet, function, script file, or executable program.
Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
docker: invalid reference format.
```

@#!$@$@%!%#

然后我看到这款优化器https://github.com/mandrean/cw-optimizoor，安装试试先。