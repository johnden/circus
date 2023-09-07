---
title: 'Sei修炼中'
subtitle: '逐个填坑'
date: 2023-09-07 14:30:00
category: 'Work'
---

昨天弄到rust-optimizer的时候就报错了，

换成https://github.com/mandrean/cw-optimizoor也不行，

原因是这个库会读/contracts的文件但是又要要求有toml文件在里面，

非常的绕。

今天回来用PowerShell运行这个

```bash
$baseName = (Get-Location).Path | Split-Path -Leaf
docker run --rm -v "${PWD}:/code" -v "${baseName}_cache:/code/target" -v registry_cache:/usr/local/cargo/registry cosmwasm/rust-optimizer:0.12.11
```
终于跑起来了

## 优化Wasm后的./deploy.sh

立马就是另一个坑，不得不说Sei的文档写得真差。

参数写成又有$END_POINT又有$RPC_ENDPOINT，

执行./deploy.sh的时候，

里面仅有三条sh语句，

然后三条都报错。

想骂人。


## 测试合约收尾

部署完测试合约之后，

拉了测试用前端也调试OK了。

后面补充一下CosmWasm和Rust的知识。