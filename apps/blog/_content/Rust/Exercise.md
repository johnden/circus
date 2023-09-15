---
title: 'Rust练习（1）'
subtitle: '记录一下练习Rust'
date: 2023-09-12 17:34:00
category: 'Rust'
---

## PrimitiveDateTime, Duration

输入一个日期，然后返回十亿秒后的那个时间。

```rust
use time::{PrimitiveDateTime as DateTime, Duration};

// Returns a DateTime one billion seconds after start.
pub fn after(start: DateTime) -> DateTime {
    let future = start + Duration::seconds(1_000_000_000); // 十亿秒
    future
}
```

## Reverse

输入一个字符串，输出反向的字符串。

```rust
pub fn reverse(input: &str) -> String {
    // 将输入字符串转换为字符切片，反转它，然后将其连接成字符串
    input.chars().rev().collect::<String>()
}

```

## Clock String

输入 hour 和 minute，输出一个显示时间的字符串

```rust
use std::fmt;
use std::ops::Add;

#[derive(Debug, PartialEq, Eq)] // 添加 Eq trait
pub struct Clock {
    hours: i32,
    minutes: i32,
}

impl Clock {
    pub fn new(hours: i32, minutes: i32) -> Self {
        let total_minutes = hours * 60 + minutes;
        let normalized_minutes = ((total_minutes % 1440) + 1440) % 1440; // Ensure non-negative

        Clock {
            hours: normalized_minutes / 60,
            minutes: normalized_minutes % 60,
        }
    }

    pub fn add_minutes(&self, minutes: i32) -> Self {
        let total_minutes = self.hours * 60 + self.minutes + minutes;
        Clock::new(total_minutes / 60, total_minutes % 60)
    }

    pub fn to_string(&self) -> String {
        format!("{:02}:{:02}", self.hours, self.minutes)
    }
}

impl fmt::Display for Clock {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "{:02}:{:02}", self.hours, self.minutes)
    }
}

impl Add<i32> for Clock {
    type Output = Clock;

    fn add(self, minutes: i32) -> Clock {
        let total_minutes = self.hours * 60 + self.minutes + minutes;
        Clock::new(total_minutes / 60, total_minutes % 60)
    }
}
```

## Armstrong Number

检测一个数字是否阿姆斯特朗数字，就是满足这些条件的：

9 is an Armstrong number, because 9 = 9^1 = 9
10 is not an Armstrong number, because 10 != 1^2 + 0^2 = 1
153 is an Armstrong number, because: 153 = 1^3 + 5^3 + 3^3 = 1 + 125 + 27 = 153
154 is not an Armstrong number, because: 154 != 1^3 + 5^3 + 4^3 = 1 + 125 + 64 = 190

```rust
pub fn is_armstrong_number(num: u32) -> bool {
    let num_str = num.to_string();
    let num_digits = num_str.len();
    let armstrong_sum = num_str
        .chars()
        .map(|c| c.to_digit(10).unwrap().pow(num_digits as u32))
        .try_fold(0u32, |acc, x| acc.checked_add(x));

    if let Some(sum) = armstrong_sum {
        sum == num
    } else {
        false
    }
}
```
