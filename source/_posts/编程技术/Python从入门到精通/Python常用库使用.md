---
title: Python常用库使用
date: 2025-02-23 14:46:06
categories: 
  - 编程技术
  - Python从入门到精通
tags:
  - Python
---

## NumPy

基本介绍：Python 中基于数组对象的科学计算库。支持大量维度数组和矩阵运算，NumPy 的核心是 ndarray 对象。

1.创建数组或矩阵

```python
import numpy as np
# 创建二维数组
data1 = np.array([[1, 2, 3], [2, 3, 4]])
# 创建3*2的矩阵，元素填充为0
data2 = np.zeros(shape=(3, 2))
# 创建3*2的矩阵，元素填充为1
data3 = np.ones(shape=(3, 2))
# 创建3*2的空矩阵
data4 = np.empty(shape=(3, 2))
# 创建连续序列的数组，起始为1，结束为10，步长为2
data5 = np.arange(1, 10, 2)
# 创建有连续间隔的数组，起始为0，结束为10，共5个元素
data6 = np.linspace(0, 10, 5)
# 创建2*3的矩阵，元素填充为0~1之间的随机数
data7 = np.random.rand(3, 4)
# 创建2*3的矩阵，元素填充为2~5之间的随机整数
data8 = np.random.randint(2, 5, size=(2, 3))
```

2.改变数组形状

```python
# 重新定义数组的形状，要求总数必须相同
reShapeData = np.arange(1, 17, 1)
reShapeData = reShapeData.reshape((4, 4))
```

3.ndarray 对象相关属性

- `.ndim`：维度
- `.shape`：形状
- `.size`：元素个数
- `.dtype`：数据类型

4.运算

```python
array1 = np.array([[1, 2], [2, 1]])
array2 = np.array([[3, 2], [2, 3]])
print(array1 + array2)
print(array1 * array2)
"""
[[4 4]
 [4 4]]
[[3 4]
 [4 3]]
"""
```

5.统计操作

- `np.mean(arr, axis=None, dtype=None, out=None)`：平均值
  - axis：沿哪个轴线计算
  - dtype：返回的数据类型，默认是 `float64`
  - out：将结果存储在指定数组中
- `np.median(arr, axis=None, out=None)`：中位数
- `np.std(arr, axis=None, dtype=None, out=None)`：标准差
- `np.var(arr, axis=None, dtype=None, out=None)`：方差
- `np.min(arr, axis=None, out=None)`：最小值
- `np.max(arr, axis=None, out=None)`：最小值
- `np.sum(arr, axis=None, dtype=None, out=None)`：元素之和
- `np.prod(arr, axis=None, dtype=None, out=None)`：元素乘积
- `np.prod(arr, axis=None, dtype=None, out=None)`：累计和

6.切片

```python
arr1 = np.array([1, 2, 3, 4, 5])
print(arr1[1:4])
arr2 = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])
# 行切片，一维切片
print(arr2[1:3])
# 列切片，二维切片
print(arr2[:,1:3])
```

7.堆叠

```python
arr1 = np.array([[1, 2, 3], [4, 5, 6]])
arr2 = np.array([[4, 5, 6], [7, 8, 9]])
stacked_vertically = np.vstack((arr1, arr2))
stacked_horizontally = np.hstack((arr1, arr2))
print(stacked_vertically)
print(stacked_horizontally)
"""
[[1 2 3]
 [4 5 6]
 [4 5 6]
 [7 8 9]]
[[1 2 3 4 5 6]
 [4 5 6 7 8 9]]
"""
```

## Pandas

### Series

`Pandas Series` 类似表格中的一个列，可以保存任何数据类型。

1.定义 `Series`：

```python
# 通过数组定义，默认索引为数字，可修改index值自定义索引
data = np.array([1.2, 2.0, 3.5])
myseries1 = pd.Series(
    data,
    index=['x', 'y', 'z'],
    name='my_series',
)
# 通过字典定义，定义同时生成索引
dict = {1: "Google", 2: "Runoob", 3: "Wiki"}
myseries2 = pd.Series(dict, index=[1, 3])
```

2.切片和索引

```python
# 获取索引0到2的数据
print(myseries1[0:2])
# 修改值
myseries1['z'] = 8.9
# 获取自定义索引x到y的数据
print(myseries1['x':'y'])
del myseries1['z']
```

3.运算

```python
# 算术运算，所有元素乘以2
result = series * 2
# 过滤得到大于2的元素
filtered_series = series[series > 2]
# 数学函数，对每个元素取平方根
result = np.sqrt(series)
```

4.属性和方法

- `.index`：获取索引
- `.values`：获取值数组
- `.describe()`：获取描述信息
- `.idxmax()`：最大值索引
- `.idxmin()`：最小值索引
- `.dtype`：数据类型
- `.shape`：形状
- `.size`：元素个数
- `.head()`：前几个元素，默认前 5 个
- `.tail()`：后几个元素，默认后 5 个
- `.sum()`：求和
- `.mean()`：平均值
- `.std()`：标准差
- `.min()`：最小值
- `.max()`：最大值

5.转换数据类型

```python
# 将所有元素转换为float64类型
series = series.astype('float64')
```

### DataFrame

`DataFrame` 是 `Pandas` 中的另一个核心数据结构，用于表示二维表格型数据。

![img](./images/pandas-DataStructure.png) ![img](./images/df-dp.png)

1.创建 `DataFrame`，没有数据的地方会填充为 NaN

```python
# 通过列表创建
dfList = pd.DataFrame([[1, 2, 3], [4, 5, 6], [7, 8, 9]], columns=['Column1', 'Column2', 'Column3'])
# 通过 Numpy 创建
data = np.array([['Google', 10], ['Runoob', 12], ['Wiki', 13]])
df = pd.DataFrame(data, columns=['Site', 'Age'])
print(df)
# 通过字典创建
dict = {'Site':['Google', 'Runoob', 'Wiki'], 'Age':[10, 12, 13]}
df2 = pd.DataFrame(dict, index=["day1", "day2", "day3"])
print(df2)
"""
     Site Age
0  Google  10
1  Runoob  12
2    Wiki  13
        Site  Age
day1  Google   10
day2  Runoob   12
day3    Wiki   13
"""
```

```python
# 从 Series 创建 DataFrame
s1 = pd.Series(['Alice', 'Bob', 'Charlie'])
s2 = pd.Series([25, 30, 35])
s3 = pd.Series(['New York', 'Los Angeles', 'Chicago'])
df = pd.DataFrame({'Name': s1, 'Age': s2, 'City': s3})
```

2.获取行

```python
# 取 "day2" 行
print(df2.loc["day2"])
# 取 "day2" 和 "day3" 行
print(df2.loc[["day2", "day3"]])
# 取 "day1" 到 "day3" 行
print(df2.loc["day1":"day3"])
```

3.获取列

```python
print(df2["Site"])
print(df2.loc[:, "Age"])
"""
day1    Google
day2    Runoob
day3      Wiki
Name: Site, dtype: object
day1    10
day2    12
day3    13
Name: Age, dtype: int64
"""
```

4.获取行列

```python
# 取第[2,3)行，第[1,2)列
print(df2.iloc[1:3, 1:2])
"""
      Age
day2   12
day3   13
"""
```

5.修改和新增列

```python
# 如果存在进行赋值，如果不存在则创建该列并赋值
df2["Sex"] = ["Male", "Female", "Male"]
```

6.修改和新增行

```python
# 如果存在进行赋值，如果不存在则创建该行并赋值
df2.loc["day2"] = ["友塔", 20, "Female"]
```

还可以使用 `concat` 添加：

```python
new_row = pd.DataFrame([["Yotta", 25]], columns=['Site', 'Age'], index=["day4"])
df2 = pd.concat([df2, new_row], ignore_index=False)
print(df2)
"""
        Site  Age     Sex
day1  Google   10    Male
day2      友塔   20  Female
day3    Wiki   13    Male
day4   Yotta   25     NaN
"""
```

7.删除行列

```python
# 删除列，axis为1
df2 = df2.drop(["Site"], axis=1)
# 删除行，axis为0
df2 = df2.drop(["day2"])
```

8.统计分析

- `.describe()`：统计摘要
- `.dtypes`：查看数据类型
- `.sum()`
- `.mean()`
- `.max()`

9.索引操作

```python
# 重置索引
df_reset = df.reset_index(drop=True)
# 设置索引
df_set = df.set_index('Column1')
```

10.合并和分割

```python
# 纵向合并
pd.concat([df1, df2], ignore_index=True)
# 横向合并
pd.merge(df1, df2, on='Column1')
```

```python
# 长格式转宽格式
df_pivot = df.pivot(index='Column1', columns='Column2', values='Column3')
# 宽格式转长格式
df_melt = df.melt(id_vars='Column1', value_vars=['Column2', 'Column3'])
```

11.读取相关信息

- `head(n)`：读取前 n 行数据，为空则默认为 5
- `tail(n)`：读取后 n 行数据，为空则默认为 5，空行各个字段返回 NaN
- `info()`：表格基本信息

### Pandas 格式文件

#### CSV

`to_string()` 用于返回 `DataFrame` 类型的数据，如果不使用该函数，则输出结果为数据的前面 5 行和末尾 5 行，中间部分以 `...` 代替。

```python
import pandas as pd
df = pd.read_csv('nba.csv')
print(df.to_string())
```

也可以使用 `to_csv()` 将 `DataFrame` 转存为 CSV 文件：

```python'
df.to_csv('site.csv')
```

#### JSON

```python
import pandas as pd
df = pd.read_json('sites.json')
print(df.to_string())
```

如果有内嵌的 JSON 数据，可以使用 `json_normalize()` 方法完整展示出来：

```python
import pandas as pd
import json
# 使用 Python JSON 模块载入数据
with open('nested_list.json','r') as f:
    data = json.loads(f.read())
# 展平数据
df_nested_list = pd.json_normalize(data, record_path =['students'])
print(df_nested_list)
```

### 数据清洗

1.清洗空值，使用 `dropna()` 方法：

- axis：默认 0，表示逢空剔除整行，为 1 表示逢空剔除整列。
- how：默认 `any`，一行（或一列）有任何一个数据出现 NA 就去掉整行；如果设置为 `how="all"` 一行（或列）都是 NA 才去掉整行。
- thresh：设置需要多少非空值的数据才可以保留下来的。
- subset：设置想要检查的列。如果是多个列，可以使用列名的 list 作为参数。
- inplace：如果设置 True，将计算得到的值直接覆盖之前的值并返回 None，修改的是源数据。

```python
DataFrame.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)
```

2.也可以使用 `fillna()` 方法来替换一些空字段：

```python
# 使用12345填充PID为空的数据
df['PID'].fillna(12345, inplace = True)
print(df.to_string())
```

3.可以通过包含空单元格的行或将列中所有单元格转换为相同格式的数据：

```python
import pandas as pd
# 第三个日期格式错误
data = {
  "Date": ['2020/12/01', '2020/12/02' , '20201226'],
  "duration": [50, 40, 45]
}
df = pd.DataFrame(data, index = ["day1", "day2", "day3"])
# 将Date列清洗为相同格式
df['Date'] = pd.to_datetime(df['Date'], format='mixed')
print(df.to_string())
```

4.可以使用 `duplicated()` 和 `drop_duplicates()` 清洗重复数据

```python
import pandas as pd
persons = {
  "name": ['Google', 'Runoob', 'Runoob', 'Taobao'],
  "age": [50, 40, 40, 23]  
}
df = pd.DataFrame(persons)
df.drop_duplicates(inplace = True)
print(df)
"""
     name  age
0  Google   50
1  Runoob   40
3  Taobao   23
"""
```





