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

#### 脚本执行

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

#### 函数历史值

```pine
//@version=6
indicator("My script")
// 将前一根K线索引值加1，来计算当前索引，第一根K线索引是0
calcBarIndex() =>
    int index = na
    // nz()函数用指定值替换na值。在脚本的第一个条形图上，当系列没有历史记录时，na值将替换为-1，然后再加1以返回初始值 0
    index := nz(index[1], replacement = -1) + 1
// 为偶数索引时候返回true
condition = bar_index % 2 == 0
int customIndex = na
// 当condition为true时候调用calcBarIndex()，这条语句编译时会有警告
if condition
    customIndex := calcBarIndex()
plot(bar_index, "Bar index", color = color.green)
plot(customIndex, "Custom index", color = color.red, style = plot.style_cross)
```

最后效果如下，可以观察到`customIndex`在索引为奇数时候没有统计。

![img](https://zhengyu-personal-blog.oss-rg-china-mainland.aliyuncs.com/Function_historical_context_1.BS8uzH0h_1erubd.webp)

当代码添加`globalScopeBarIndex`全局范围变量，这时候会直接调用函数。最终`bar_index`和`customIndex`在偶数索引显示相同，奇数索引`customIndex`不显示。

```pine
//@version=6
indicator("My script")
calcBarIndex() =>
    int index = na
    index := nz(index[1], replacement = -1) + 1
condition = bar_index % 2 == 0
globalScopeBarIndex = calcBarIndex()
int customIndex = na
if condition
    customIndex := globalScopeBarIndex
plot(bar_index, "Bar index", color = color.green)
plot(customIndex, "Custom index", color = color.red, style = plot.style_cross)
```

![img](https://zhengyu-personal-blog.oss-rg-china-mainland.aliyuncs.com/Function_historical_context_2.DMU4JJfT_ZCks6f.webp)