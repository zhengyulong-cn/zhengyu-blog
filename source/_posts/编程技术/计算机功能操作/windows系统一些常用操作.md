---
title: windows系统一些常用操作
date: 2025-03-24 13:46:06
categories: 
  - 编程技术
  - 计算机功能操作
---

## 处理端口被占用

打开 CMD，执行：

```bash
# 查看端口使用情况
netstat -ano | findstr 4000
# 强制关闭指定进程
taskkill -PID 1960 -F
```