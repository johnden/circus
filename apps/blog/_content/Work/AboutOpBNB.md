---
title: '工作琐事 与 在Area52中学习Rust和CosmWasm(2)'
subtitle: '这次轮到OpBNB了'
date: 2023-09-19 10:20:10
category: 'Work'
---

昨天Adam跟我说，OpBNB主网上线有活动，

币安那边联系我们，想我们在OpBNB部署写合约给他们带点量。

我了解到OpBNB的智能合约部署可以通过换个 ChainID 和 RPC 就可以达成了。

于是同意了，准备把我们的充值合约 Copy 一份过去。

另外由于项目有新的游戏内容发展，想要在 BNB 上面启动，毕竟新内容交互比较多而 BNB 的 gas 比较低廉。

所以准备把我们的 token 从 ETH 跨链到 BNB 。

所以今天是一边学习 Area52 的 NFT 内容一边完成这些工作。

## 第一课

cw721-base 实现的 cw721 中提供的入口点和函数。

如何使用 cw721-base 铸造 NFTs。

如何使用 cw721 处理离线元数据。

创建一个令牌收藏合同。

## 第二课

使用托管在Crates.io上的依赖项。

使用本地依赖项。

将Rust程序编译为库和可执行文件。

从CosmWasm中，我们接触到了：

使用自定义逻辑修改cw721-base。

cw721-non-transferable的组成。

## 第三课

声明自定义包作为依赖项：我们学会了如何将自定义的Rust包声明为我们的项目的依赖项，无论是从Crates.io还是本地路径导入。

在Cargo.toml中启用库功能：我们了解了如何在项目的Cargo.toml文件中启用库功能，以便正确配置依赖项。

使用Serde进行NFT元数据的序列化和反序列化：我们学会了如何使用Serde框架来有效地序列化和反序列化Rust数据结构，以处理NFT的元数据。

使用类型别名：我们了解了如何使用Rust的类型别名来简化代码，并提高代码的可读性和可维护性。

为智能合约编写单元测试：我们学会了如何编写单元测试来验证我们的智能合约的行为，以确保其正确运行。

从CosmWasm库方面，我们了解了以下内容：

cw2和合同迁移：我们了解了合同代码迁移的概念，以及如何使用CosmWasm的cw2库来管理合同版本。

使用addr_validate从Deps.api验证Cosmos Addr类型：我们学会了如何使用Deps和DepsMut的api trait中的addr_validate函数来验证Cosmos地址类型的有效性。

在reply入口点中使用的Reply类型：我们了解了在智能合约的reply入口点中使用的Reply类型，它用于处理合同的回复。

使用cosmwasm_std::testing中的mock_dependencies、mock_env和mock_info来模拟区块链查询和交易：我们学会了如何使用cosmwasm_std::testing库中提供的工具来模拟区块链的查询和交易，以进行智能合约的单元测试。
