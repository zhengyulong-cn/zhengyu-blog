---
title: Pine语言入门
date: 2025-03-25 13:46:06
categories: 
  - 编程技术
  - 指标与量化
tags:
  - 指标与量化
  - 期货
---

## 初识Pine语言

### 第一个指标

下面脚本实现了MACD指标：

```pine
// 告诉编辑器使用版本6的Pine script
//@version=6
// 显示脚本名称
indicator("MACD #1")
// 定义变量
fast = 12
slow = 26
// 定义变量，调用函数ta.ema
fastMA = ta.ema(close, fast)
slowMA = ta.ema(close, slow)
// 定义变量，两个EMA之间的差值
macd = fastMA - slowMA
signal = ta.ema(macd, 9)
// 使用黑色线和红色线在图中绘制变量
plot(macd, color = color.black)
plot(signal, color = color.red)
```

Pine语言自带处理MACD的函数，因此可以这样写：

```pine
//@version=6
indicator("MACD #2")
// 使用输入方式定义变量
fastInput = input(12, "Fast length")
slowInput = input(26, "Slow length")
// 调用macd函数，得到相关值
[macdLine, signalLine, histLine] = ta.macd(close, fastInput, slowInput, 9)
plot(macdLine, color = color.black)
plot(signalLine, color = color.red)
```

### 执行模型

Pine脚本执行：固定数据量，历史K线逐个处理，实时K线每次更新处理。

在历史K线，每根K线的价和量都是已知的，每根K线执行一次脚本。首先从索引0处的数据集的第一根K线上执行，每个语句都使用当前K线的值执行。

```pine
//@version=6
indicator("My Script", overlay = true)
src = close
a = ta.sma(src, 5)
b = ta.sma(src, 50)
c = ta.cross(a, b)
plot(a, color = color.blue)
plot(b, color = color.black)
plotshape(c, color = color.red)
```

