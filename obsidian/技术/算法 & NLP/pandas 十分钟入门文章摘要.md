```python3
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt


# # 1. 创造对象
s = pd.Series([1, 3, 5, np.nan, 6, 8])
print(s)

dates = pd.date_range('20130101', periods=6)
print(dates)

# 你可以认为，DataFrame 是由 Series 组成的
df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list('ABCD'))
print(df)

# # 2. 查看数据
# 查看顶端几列
print(df.head(3))

# 查看低端几列
print(df.tail(3))

# 查看 index 和 columns
print(df.index)
print(df.columns)

# 查看数据概要
print(df.describe())

# 转置
print(df.T)

# 对 axis 按照 index 排序（axis=1 是指第二个维度，即：列）
print(df.sort_index(axis=0, ascending=False))

# 按照值排序
print(df.sort_values(by='B', ascending=False))

print('-' * 100)

# # 3. 选择

# > 注意，以下这些对交互式环境很友好，但是作为 production code 请用优化过的 .at, .iat, .loc, .iloc 和 .ix

# 获取列/行

print(df['A'])

print(df[0:4])

print(df['20130102': '20130104'])

print(df.loc[:, ['A', 'C', 'B']])

# 通过 label 选择
# 当有一个维度是标量（而不是范围或序列）的时候，选择出的矩阵维度会减少
# numpy.object -> Series -> DataFrame
print(df.loc['20130102'])

print(df.loc[dates[0], 'A'])
print(df.at[dates[0], 'A'])

print(df.loc[:, 'A'])

print(df.loc[:, ['A']])

# 通过整数下标选择
print(df.iloc[3])

print(df.iloc[3:5, 0:2])

print(df.iloc[[1, 2, 4], [0, 2]])

print(df.iloc[1, 1])

# 条件选择
print(df[df['A'] > 0])

# 没有填充的值等于 NaN
print(df[df > 0])

# 是否在集合中
df2 = df.copy()
df2['E'] = ['one'] * (len(df2.index))
print(df2[df2['E'].isin(['one'])])

# # 4. Setting (等号两边需要是相同维度的对象)
# 按 index 对应
s1 = pd.Series([1, 2, 3, 4, 5, 6], index=pd.date_range('20130101', periods=6))
df['F'] = s1
print(df)

# 通过 label
df.at['20130102', 'A'] = 0

# 通过 下标
df.iat[0, 1] = 0
print(df)

# 通过 数组
df.at[:, 'D'] = [10] * len(df)
print(df)

# 用布尔值做下标的 set
df[df > 0] = -df
print(df)

print(type(df['A']))
print(type(df.loc[:, 'D']))

# # 5. 缺失值处理

# pandas 用 np.nan 表示缺失值。通常它不会被计算。
s1 = pd.Series([1, 2, 3, 4, 5, 6], index=pd.date_range('20130102', periods=6))
df['G'] = s1
print(df)
# 查看 NaN 情况
print(pd.isnull(df))

df.dropna(inplace=True)
print(df)

df.fillna(5, inplace=True)
print(df)

# # 6. 数值操作

# 通常，操作都会把 NaN 排除在外

# 统计
print(df.mean())
print(df.mean(1))

# Apply

# 对数据（行或列） Apply 函数

print(df.apply(lambda x: x.max() - x.min()))

# 字符串操作

s = pd.Series(['A', 'B', 'C', 'Aaba', 'Baca', np.nan, 'CABA', 'dog', 'cat'])

print(s.str.lower())

# # 7. 表合并

# concat 简单拼接
df = pd.DataFrame(np.random.randn(2, 4))
df1 = pd.DataFrame(np.random.randn(3, 4))
print(pd.concat([df, df1], axis=0))

# merge 合并
left = pd.DataFrame({'A': ['1', '2'], 'B': [1, 2]})
print(left)

right = pd.DataFrame({'A': ['1', '3'], 'C': [4, 5]})
print(right)

print(pd.merge(left, right, on='A', how='inner'))

# append 添加 Series

df = pd.DataFrame(np.random.randn(8, 4), columns=['A', 'B', 'C', 'D'])
print(df)

s = df.iloc[3]

print(df.append(s, ignore_index=True))

# # 8. Grouping

# 根据某些规则，把数据分组

# 对每组应用一个聚集函数，把结果放在一个数据结构中

df = pd.DataFrame({'A': ['foo', 'bar', 'foo', 'bar',
                         'foo', 'bar', 'foo', 'foo'],
                   'B': ['one', 'one', 'two', 'three',
                         'two', 'two', 'one', 'three'],
                   'C': np.random.randn(8),
                   'D': np.random.randn(8)})
print(df)

print(df.groupby('A').sum())

print(df.groupby(['A', 'B']).sum())

# # 9. Reshape


# 不太懂....

# # 10. 时间序列

rng = pd.date_range('1/1/2012', periods=100, freq='S')

ts = pd.Series(np.random.randint(0, 500, len(rng)), index=rng)
print(ts)
print(ts.resample('T'))

# # 11. 类别

# category

# # 12. 画图

# # 13. 数据的读写
```