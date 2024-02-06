# Pandas

## Dataframe

Series 是 K-V 类型，K(index)和 V(Data)，类比 Python 的字典类型。

其中，`index`不是 Series 的一个 column，Series 没有 column，`index`只是将`index label`与一组`data element`做映射。

一个 Series 代表一组数据（eg:某国家 GDP，index 为年代，data 为 GDP 值）。Dataframe 是 Series 的集合（eg:全球 GDP，包括全部国家）。

## 合并数据

合并数据的几种常见方法：

- `concat`: Concatenate (appends) different objects either row or column-wise
- `append`: Appends one object to another row or column-wise
- `join`: Merge dataframes using indexes
- `merge`: Merge dataframes using indexes or columns

DataFrame 之间的合并：[https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html](https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html)

```
# ----------------------------------------------------------------------------
#   Understanding the different types of joins:
# ----------------------------------------------------------------------------
#
# Suppose we have two datasets:
#
# Left:
#
#
# | key | L  |
# |-----+----|
# | 1   | L1 |
# | 2   | L2 |
# | 3   | L3 |
#
#
# Right:
#
#
# | key | R  |
# |-----+----|
# | 3   | R3 |
# | 4   | R4 |
# | 5   | R5 |
#
#
# We want to merge the Right and Left tables using the column `key`.
# As you can see, there are some values of `key` that appear only on the `Left`
# table, some that appear only in the `Right` table, and some that are common to
# both tables. We can think of a merge between these two tables as following:
#
#
# Left:                   Right:              Merged
#
# | key | L  | Join type    | key | R  | Result   | key | L   | R   |
# | 1   | L1 | -----------> | 3   | R3 | -------> | ... | ... | ... |
# | 2   | L2 |              | 4   | R4 |          | ... | ... | ... |
# | 3   | L3 |              | 5   | R5 |
#
# The resulting table will depend on the type of join:
#
# - Left join: Keep all the keys of the left table (Left)
#
# Left:                   Right:              Merged
# |key| L |   Left Join   |key| R |  Result   |key| L | R |
# |1  | L1|  -----------> |3  | R3|  -------> |1  | L1|NaN|
# |2  | L2|               |4  | R4|           |2  | L2|NaN|
# |3  | L3|               |5  | R5|           |3  | L3| R3|
#
# - Right join: Keep all the keys of the right table (Right)
#
# Left:                   Right:              Merged
# | key | L  | Right Join   | key | R  | Result   | key | L   | R  |
# | 1   | L1 | -----------> | 3   | R3 | -------> | 3   | L3  | R3 |
# | 2   | L2 |              | 4   | R4 |          | 4   | NaN | R4 |
# | 3   | L3 |              | 5   | R5 |          | 5   | NaN | R5 |
#
#
# - Inner join: Keep only the keys that exist in both left and right
#
# Left:                   Right:              Merged
# |key| L |  Inner Join   |key| R |  Result   |key| L | R |
# |1  | L1|  -----------> |3  | R3|  -------> |3  | L3| R3|
# |2  | L2|               |4  | R4|
# |3  | L3|               |5  | R5|
#
# - Outer join: Keep all the keys in left and right
#
# Left:                   Right:              Merged
# |key| L |  Outer Join   |key| R |  Result   |key| L | R |
# |1  | L1|  -----------> |3  | R3|  -------> |1  | L1|NaN|
# |2  | L2|               |4  | R4|           |2  | L2|NaN|
# |3  | L3|               |5  | R5|           |3  | L3| R3|
#                                             |4  |NaN| R4|
#                                             |5  |NaN| R5|
#
```

### df.loc()函数

loc 可以筛选指定的行列。在二维矩阵中按照`[横坐标,竖坐标]` 顺序。

```
import pandas as pd
data = {
    'AUD/USD': [ 0.7280, 0.7209, np.nan, 0.7263, 0.7281, 0.7285,],
    'EUR/AUD': [ 1.6232, 1.6321, 1.6221, 1.6282, np.nan, 1.6288,],
    }
index = [ '2020-09-08', '2020-09-09', '2020-09-10', '2020-09-11', '2020-09-14', '2020-09-15',]
df = pd.DataFrame(data, index)

```

例如`df.loc['2020-09-09':'2020-09-11']`，返回 2020-09-09 到 2020-09-11 之间的数据（注意是闭区间）。

```
						AUD/USD	EUR/AUD
2020-09-09	0.7209	1.6321
2020-09-10	NaN			1.6221
2020-09-11	0.7263	1.6282
```

特别的，当截止点（2020-09-11）不存在时，DataFrame 返回从开始点起的全部数据，例如`df.loc['2020-09-09':'ThisObviouslyWontExistAsAnIndex']` ，返回从 2020-09-09 开始的**全部**数据。

Pandas 会尝试匹配索引的第一个字符（基于 ASCII），并返回从当前匹配值到`index`结尾的全部结果。

例如：`index=['ce','de','ge','ie']`，那么当`df.loc['c']`会返回全部值（从匹配的 c 到结束）。

实现原理为 Pandas 的`serachsorted`算法，参见[Pandas 实现](https://github.com/pandas-dev/pandas/blob/v1.1.3/pandas/core/base.py#L1499-L1501)。

```
import pandas as pd

t1 = pd.Series([0, 1, 2, 3], index=['ce','de','ge','ie'])

# Test 1. 返回全部（'6'的ASCII小于'ce'，则返回全部）
print(t1.loc['6':])
print("--- --- ---")
# Test 2. 返回de至结束
print(t1.loc['d':])
print("--- --- ---")
# Test 3. 返回空（'p'的ASCII大于'i'，返回空）
print(t1.loc['p':])
print("--- --- ---")
```

#### 布尔运算筛选值

可以在 loc 函数中进行布尔运算，只展示指定行&列。

例如：`cond = rec['Action']=='up'`

```python
# In:
cond

# Out:
#  Date
#  2012-02-16 07:42:00    False
#  2012-02-16 13:53:00    False
#  2012-02-17 06:17:00    False
#  2012-03-26 07:31:00     True
#  2012-05-22 05:57:00    False
#                         ...
#  2020-09-23 09:11:01    False
#  2020-09-23 11:15:12     True
#  2020-09-23 14:18:13    False
#  2020-09-23 16:16:17    False
#  2020-10-08 10:15:39     True
#  Name: action, Length: 358, dtype: bool
#
```

这里返回的是每条记录是否满足条件。

```python
# In:
rec.loc[cond]

# Out:
#                                      firm        to_grade    from_grade action
#  Date
#  2012-03-26 07:31:00           Wunderlich             Buy           NaN     up
#  2012-09-17 05:46:00       Morgan Stanley      Overweight       Neutral     up
#  2013-07-26 06:35:48        Deutsche Bank             Buy          Hold     up
#  2013-10-15 06:51:28              Wedbush      Outperform       Neutral     up
#  2013-11-07 09:58:27  Standpoint Research            Hold          Sell     up
#  ...                                  ...             ...           ...    ...
#  2020-09-23 08:56:18       Morgan Stanley    Equal-Weight   Underweight     up
#  2020-09-23 08:58:42          Cowen & Co.  Market Perform  Underperform     up
#  2020-09-23 09:00:03         Roth Capital         Neutral          Sell     up
#  2020-09-23 11:15:12        Deutsche Bank             Buy          Hold     up
#  2020-10-08 10:15:39           New Street             Buy       Neutral     up
#
#  [39 rows x 4 columns]
#
```

这里返回的是**满足条件**的 dataframe。

注意：

1. 条件`cond`只有值起作用，与索引不关，换句话说，`cond`也可写作`cond.values`。
2. 注意`cond`的长度必须与 df 一致，否则会报错，比如`rec[cond[:-2]]`这样就会报错。

3. 运算符也可以作用于 Columns，比如这样`rec.loc[:, [True, False, False, False]]`，(只返回为 True 的 Columns)

```python
   # Out:
   #                                    firm
   #  Date
   #  2012-02-16 07:42:00          JP Morgan
   #  2012-02-16 13:53:00         Wunderlich
   #  2012-02-17 06:17:00         Oxen Group
   #  2012-03-26 07:31:00         Wunderlich
   #  2012-05-22 05:57:00        Maxim Group
   #  ...                                ...
   #  2020-09-23 09:11:01         Wunderlich
   #  2020-09-23 11:15:12      Deutsche Bank
   #  2020-09-23 14:18:13  Canaccord Genuity
   #  2020-09-23 16:16:17              Baird
   #  2020-10-08 10:15:39         New Street
   #
   #  [358 rows x 1 columns]
   #

```

4. 可以把行列条件联合起来，比如：`rec.loc[cond, [False, False, True, True]]`

```python
# Out:
#                         from_grade action
#  Date
#  2012-03-26 07:31:00           NaN     up
#  2012-09-17 05:46:00       Neutral     up
#  2013-07-26 06:35:48          Hold     up
#  2013-10-15 06:51:28       Neutral     up
#  2013-11-07 09:58:27          Sell     up
#  ...                           ...    ...
#  2020-09-23 08:56:18   Underweight     up
#  2020-09-23 08:58:42  Underperform     up
#  2020-09-23 09:00:03          Sell     up
#  2020-09-23 11:15:12          Hold     up
#  2020-10-08 10:15:39       Neutral     up
#
#  [39 rows x 2 columns]
#
```

除此之外，还可以用这个方法快速将某一类值批量重命名。

`rec[rec == 'up'] = 'UP'`

```python
# In:
rec

# Out:
#                                    firm    to_grade from_grade action
#  Date
#  2012-02-16 07:42:00          JP Morgan  Overweight        NaN   main
#  2012-02-16 13:53:00         Wunderlich        Hold        NaN   down
#  2012-02-17 06:17:00         Oxen Group         Buy        NaN   init
#  2012-03-26 07:31:00         Wunderlich         Buy        NaN     UP
#  2012-05-22 05:57:00        Maxim Group         Buy        NaN   init
#  ...                                ...         ...        ...    ...
#  2020-09-23 09:11:01         Wunderlich        Sell        Buy   down
#  2020-09-23 11:15:12      Deutsche Bank         Buy       Hold     UP
#  2020-09-23 14:18:13  Canaccord Genuity        Hold        NaN   main
#  2020-09-23 16:16:17              Baird     Neutral        NaN   main
#  2020-10-08 10:15:39         New Street         Buy    Neutral     UP
#
#  [358 rows x 4 columns]
#
```

使用`.loc[]`也可，比如再把名字改回去：`rec.loc[rec['action'] == 'UP', :] = 'up'`

```
# Out:
#                                    firm    to_grade from_grade action
#  Date
#  2012-02-16 07:42:00          JP Morgan  Overweight        NaN   main
#  2012-02-16 13:53:00         Wunderlich        Hold        NaN   down
#  2012-02-17 06:17:00         Oxen Group         Buy        NaN   init
#  2012-03-26 07:31:00                 up          up         up     up
#  2012-05-22 05:57:00        Maxim Group         Buy        NaN   init
#  ...                                ...         ...        ...    ...
#  2020-09-23 09:11:01         Wunderlich        Sell        Buy   down
#  2020-09-23 11:15:12                 up          up         up     up
#  2020-09-23 14:18:13  Canaccord Genuity        Hold        NaN   main
#  2020-09-23 16:16:17              Baird     Neutral        NaN   main
#  2020-10-08 10:15:39                 up          up         up     up
#
#  [358 rows x 4 columns]
#
```

组合逻辑表达式筛选，可以用 python 的逻辑运算符，也可以使用`str.contains()`。

例如：`crit = (rec['action'] == 'up') | (rec['action'] == 'down')`

例如：`crit = rec['action'].str.contains('up|down')`

两者等价。

```python
# In:
rec[crit]

# Out:
#                                    firm      to_grade from_grade action
#  Date
#  2012-02-16 13:53:00         Wunderlich          Hold        NaN   down
#  2012-03-26 07:31:00                 up            up         up     up
#  2012-07-18 06:43:00         Wunderlich          Sell        Buy   down
#  2012-09-17 05:46:00                 up            up         up     up
#  2013-02-21 06:53:02    Bank of America  Underperform    Neutral   down
#  ...                                ...           ...        ...    ...
#  2020-09-23 09:02:03               CFRA          Sell       Hold   down
#  2020-09-23 09:03:16  China Renaissance          Hold        Buy   down
#  2020-09-23 09:11:01         Wunderlich          Sell        Buy   down
#  2020-09-23 11:15:12                 up            up         up     up
#  2020-10-08 10:15:39                 up            up         up     up
#
#  [97 rows x 4 columns]
#
```

### 删除不需要的列

```
cols_to_drop = [
    'PassengerId',
    'Name',
    'Ticket',
    'Cabin',
    'Embarked',
]

df = ds.drop(cols_to_drop, axis=1)
```

##

### 写入数据

`df['Col_name']['idx'] = 10`

[ref](https://stackoverflow.com/questions/13842088/set-value-for-particular-cell-in-pandas-dataframe-using-index)

### read_csv()从 csv 读入

```
data = pd.read_csv('Advertising.csv', index_col=0);
```

首行为 index 列名。

或者指定 names 列名:

names : array-like, optional
List of column names to use. If file contains no header row, then you should explicitly pass header=None. Duplicates in this list are not allowed.

[pandas.read_csv &#8212; pandas 0.25.1 documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)

## to_numpy() 转化 numpy

```
ndata = data.to_numpy()
```

`to_numpy() `只支持 0.24 版本以上 pandas，旧版本使用： `ndata = data.to_numpy()`。
