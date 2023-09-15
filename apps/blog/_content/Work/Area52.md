---
title: '在Area52中学习Rust和CosmWasm'
subtitle: '太喜欢这种一边编程一边做游戏的教程'
date: 2023-09-15 14:47:00
category: 'Work'
---

昨天发现了 https://area-52.io/ 这个网站一边编程一边做游戏，

用于学习 Rust 和 CosmWasm。

我想起以前我也是通过 Loom 的 CryptoZombie 来学习 Solidity 智能合约。

现在记录一下课程主要内容，主要生啃英语可能记忆不太深。

## 第一课

CosmWasm 遵循 Actor 模型，涉及通过消息进行的角色（智能合约）交互。

CosmWasm 的入口点是定义合同如何响应特定类型消息的特殊函数。

instantiate 入口点在智能合约首次部署到区块链时进行初始化。

我们学习了如何构建和使用 instantiate 函数的消息结构（InstantiateMsg）。

在 CosmWasm 合约中，状态存储在区块链上，可以通过入口点进行修改。

我们讨论了使用 serde 库进行数据结构的序列化和反序列化的概念。

来自 CosmWasm 库的关键概念，包括 entry_point 特征、Response 消息类型、使用 add_attributes 返回键值对的方法，以及各种类型的使用，如 DepsMut、Env、MessageInfo 和 Addr。

我们探讨了 Storage 结构及其相关函数，包括用于与合同存储交互的 Singleton 和 ReadonlySingleton。

## 第二课

执行（execute）用于对合约进行更改，这将产生费用。

查询（query）是只读的，不会产生费用。

由于是只读的，查询接受一个 Deps 参数，而不是 DepsMut 参数。

MessageInfo 可以用于检查发送方是否具有对特定合约功能的有效访问权限，方法是将 info.sender 与预先确定的管理员地址进行比较。

我们还接触了 cosmwasm 库中的一些概念，包括：

StdResult 结构体，它是 Result 的包装器。

用于查询的返回类型 Binary，以及将任意类型转换为 Binary 的 to_binary 函数。

Deps，它是 DepsMut 的只读版本。
