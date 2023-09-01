---
title: 'Rust学习手记'
subtitle: '记录一下今天学习Rust的重点'
date: 2023-09-01 17:34:00
category: 'Rust'
---

现在开始在工作的闲暇时间中（摸鱼中）学习一下Rust，Rust在服务端的性能仅次于C++，而在Golang, C#, Java, Python, Node之上（ChatGPT说的，要杠找它），而在区块链领域里面也会用到，譬如Solana，还有StarkNet（其编写智能合约的Cairo也是跟Rust相似，后面也会学习）

## Move

fn main() {
    let s1 = String::from("hello");
    let s2 = s1;
}

如果你在其他语言中听说过术语 浅拷贝（shallow copy）和 深拷贝（deep copy），那么拷贝指针、长度和容量而不拷贝数据可能听起来像浅拷贝。不过因为 Rust 同时使第一个变量无效了，这个操作被称为 移动（move），而不是叫做浅拷贝。上面的例子可以解读为 s1 被 移动 到了 s2 中。

## Clone

fn main() {
    let s1 = String::from("hello");
    let s2 = s1.clone();

    println!("s1 = {}, s2 = {}", s1, s2);
}

如果我们 确实 需要深度复制 String 中堆上的数据，而不仅仅是栈上的数据，可以使用一个叫做 clone 的通用函数。
