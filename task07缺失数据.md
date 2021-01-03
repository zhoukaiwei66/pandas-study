
# 第七章 缺失数据


```python
import numpy as np
import pandas as pd
```

## 一、缺失值的统计和删除

### 1. 缺失信息的统计

缺失数据可以使用 isna 或 isnull （两个函数没有区别）来查看每个单元格是否缺失，结合 mean 可以计算出每列缺失值的比例：


```python
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv',
                     usecols = ['Grade', 'Name', 'Gender', 'Height', 'Weight', 'Transfer'])
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Freshman</td>
      <td>Gaopeng Yang</td>
      <td>Female</td>
      <td>158.9</td>
      <td>46.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Freshman</td>
      <td>Changqiang You</td>
      <td>Male</td>
      <td>166.5</td>
      <td>70.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Senior</td>
      <td>Mei Sun</td>
      <td>Male</td>
      <td>188.9</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sophomore</td>
      <td>Xiaojuan Sun</td>
      <td>Female</td>
      <td>NaN</td>
      <td>41.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Sophomore</td>
      <td>Gaojuan You</td>
      <td>Male</td>
      <td>174.0</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.isna().head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
 df.isna().mean() # 查看缺失的比例
```




    Grade       0.000
    Name        0.000
    Gender      0.000
    Height      0.085
    Weight      0.055
    Transfer    0.060
    dtype: float64



如果想要查看某一列缺失或者非缺失的行，可以利用 Series 上的 isna 或者 notna 进行布尔索引。例如，查看身高缺失的行：


```python
df[df.Height.isna()].head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Sophomore</td>
      <td>Xiaojuan Sun</td>
      <td>Female</td>
      <td>NaN</td>
      <td>41.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Senior</td>
      <td>Peng You</td>
      <td>Female</td>
      <td>NaN</td>
      <td>48.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Junior</td>
      <td>Yanli You</td>
      <td>Female</td>
      <td>NaN</td>
      <td>48.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Freshman</td>
      <td>Xiaojuan Qin</td>
      <td>Male</td>
      <td>NaN</td>
      <td>79.0</td>
      <td>Y</td>
    </tr>
    <tr>
      <th>60</th>
      <td>Freshman</td>
      <td>Yanpeng Lv</td>
      <td>Male</td>
      <td>NaN</td>
      <td>65.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



如果想要同时对几个列，检索出全部为缺失或者至少有一个缺失或者没有缺失的行，可以使用 isna, notna 和 any, all 的组合。


```python
sub_set = df[['Height', 'Weight', 'Transfer']]
df[sub_set.isna().all(1)] # 全部缺失
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>102</th>
      <td>Junior</td>
      <td>Chengli Zhao</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[sub_set.isna().any(1)].head() # 至少有一个缺失
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Sophomore</td>
      <td>Xiaojuan Sun</td>
      <td>Female</td>
      <td>NaN</td>
      <td>41.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Junior</td>
      <td>Juan Xu</td>
      <td>Female</td>
      <td>164.8</td>
      <td>NaN</td>
      <td>N</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Senior</td>
      <td>Peng You</td>
      <td>Female</td>
      <td>NaN</td>
      <td>48.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Senior</td>
      <td>Xiaopeng Shen</td>
      <td>Male</td>
      <td>166.0</td>
      <td>62.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Junior</td>
      <td>Yanli You</td>
      <td>Female</td>
      <td>NaN</td>
      <td>48.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[sub_set.notna().all(1)].head() # 没有缺失
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Freshman</td>
      <td>Gaopeng Yang</td>
      <td>Female</td>
      <td>158.9</td>
      <td>46.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Freshman</td>
      <td>Changqiang You</td>
      <td>Male</td>
      <td>166.5</td>
      <td>70.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Senior</td>
      <td>Mei Sun</td>
      <td>Male</td>
      <td>188.9</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Sophomore</td>
      <td>Gaojuan You</td>
      <td>Male</td>
      <td>174.0</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Freshman</td>
      <td>Xiaoli Qian</td>
      <td>Female</td>
      <td>158.0</td>
      <td>51.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



### 2. 缺失信息的删除

数据处理中经常需要根据缺失值的大小、比例或其他特征来进行行样本或列特征的删除， pandas 中提供了 dropna 函数来进行操作。

dropna 的主要参数为轴方向 axis （默认为0，即删除行）、删除方式 how 、删除的非缺失值个数阈值 thresh （ 非缺失值 没有达到这个数量的相应维度会被删除）、备选的删除子集 subset ，其中 how 主要有 any 和 all 两种参数可以选择。


```python
res = df.dropna(how = 'any', subset = ['Height', 'Weight'])#删除身高体重至少有一个缺失的行：
res.shape
```




    (174, 6)




```python
#删除超过15个缺失值的列：
res = df.dropna(1, thresh=df.shape[0]-15) # 身高被删除
res.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Freshman</td>
      <td>Gaopeng Yang</td>
      <td>Female</td>
      <td>46.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Freshman</td>
      <td>Changqiang You</td>
      <td>Male</td>
      <td>70.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Senior</td>
      <td>Mei Sun</td>
      <td>Male</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sophomore</td>
      <td>Xiaojuan Sun</td>
      <td>Female</td>
      <td>41.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Sophomore</td>
      <td>Gaojuan You</td>
      <td>Male</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



## 二、缺失值的填充和插值

### 1. 利用fillna进行填充

在 fillna 中有三个参数是常用的： value, method, limit 。其中， value 为填充值，可以是标量，也可以是索引到元素的字典映射； method 为填充方法，有用前面的元素填充 ffill 和用后面的元素填充 bfill 两种类型， limit 参数表示连续缺失值的最大填充次数。


```python
s = pd.Series([np.nan, 1, np.nan, np.nan, 2, np.nan],list('aaabcd'))
s
```




    a    NaN
    a    1.0
    a    NaN
    b    NaN
    c    2.0
    d    NaN
    dtype: float64




```python
s.fillna(method='ffill') # 用前面的值向后填充
```




    a    NaN
    a    1.0
    a    1.0
    b    1.0
    c    2.0
    d    2.0
    dtype: float64




```python
s.fillna(method='ffill', limit=1) # 连续出现的缺失，最多填充一次
```




    a    NaN
    a    1.0
    a    1.0
    b    NaN
    c    2.0
    d    2.0
    dtype: float64




```python
s.fillna(s.mean()) # value为标量
```




    a    1.5
    a    1.0
    a    1.5
    b    1.5
    c    2.0
    d    1.5
    dtype: float64




```python
 s.fillna({'a': 100, 'd': 200}) # 通过索引映射填充的值
```




    a    100.0
    a      1.0
    a    100.0
    b      NaN
    c      2.0
    d    200.0
    dtype: float64



### 2. 插值函数

对于 interpolate 而言，除了插值方法（默认为 linear 线性插值）之外，有与 fillna 类似的两个常用参数，一个是控制方向的 limit_direction ，另一个是控制最大连续缺失值插值个数的 limit 。其中，限制插值的方向默认为 forward ，这与 fillna 的 method 中的 ffill 是类似的，若想要后向限制插值或者双向限制插值可以指定为 backward 或 both 


```python
s = pd.Series([np.nan, np.nan, 1,np.nan, np.nan, np.nan,2, np.nan, np.nan])
s.values
```




    array([nan, nan,  1., nan, nan, nan,  2., nan, nan])




```python
#在默认线性插值法下分别进行 backward 和双向限制插值，同时限制最大连续条数为1：
res = s.interpolate(limit_direction='both', limit=1)
res.values
```




    array([ nan, 1.  , 1.  , 1.25,  nan, 1.75, 2.  , 2.  ,  nan])



第二种常见的插值是最近邻插补，即缺失值的元素和离它最近的非缺失值元素一样：


```python
s.interpolate('nearest').values
```




    array([nan, nan,  1.,  1.,  1.,  2.,  2., nan, nan])



最后来介绍索引插值，即根据索引大小进行线性插值


```python
s = pd.Series([0,np.nan,10],index=[0,1,10])
s
```




    0      0.0
    1      NaN
    10    10.0
    dtype: float64




```python
s.interpolate()
```




    0      0.0
    1      5.0
    10    10.0
    dtype: float64




```python
s.interpolate(method='index')
```




    0      0.0
    1      1.0
    10    10.0
    dtype: float64



## 三、Nullable类型

### 1. 缺失记号及其缺陷

在 python 中的缺失值用 None 表示，该元素除了等于自己本身之外，与其他任何元素不相等：


```python
None == None
```




    True




```python
None == False
```




    False




```python
None == []
```




    False




```python
None == ''
```




    False



值得注意的是，虽然在对缺失序列或表格的元素进行比较操作的时候， np.nan 的对应位置会返回 False ，但是在使用 equals 函数进行两张表或两个序列的相同性检验时，会自动跳过两侧表都是缺失值的位置，直接返回 True ：


```python
s1 = pd.Series([1, np.nan])
s2 = pd.Series([1, 2])
s3 = pd.Series([1, np.nan])
s1 == 1
```




    0     True
    1    False
    dtype: bool




```python
s1.equals(s2)
```




    False




```python
s1.equals(s3)
```




    True



### 2. Nullable类型的性质


```python
pd.Series([np.nan, 1], dtype = 'Int64') # "i"是大写的
```




    0    <NA>
    1       1
    dtype: Int64




```python
pd.Series([np.nan, True], dtype = 'boolean')
```




    0    <NA>
    1    True
    dtype: boolean




```python
pd.Series([np.nan, 'my_str'], dtype = 'string')
```




    0      <NA>
    1    my_str
    dtype: string




```python
#在 Int 的序列中，返回的结果会尽可能地成为 Nullable 的类型：
pd.Series([np.nan, 0], dtype = 'Int64') + 1
```




    0    <NA>
    1       1
    dtype: Int64




```python
pd.Series([np.nan, 0], dtype = 'Int64') == 0
```




    0    <NA>
    1    True
    dtype: boolean




```python
pd.Series([np.nan, 0], dtype = 'Int64') * 0.5 # 只能是浮点
```




    0    NaN
    1    0.0
    dtype: float64



对于 boolean 类型的序列而言，其和 bool 序列的行为主要有两点区别：

第一点是带有缺失的布尔列表无法进行索引器中的选择，而 boolean 会把缺失值看作 False ：


```python
s = pd.Series(['a', 'b'])
s_bool = pd.Series([True, np.nan])
s_boolean = pd.Series([True, np.nan]).astype('boolean')
s[s_boolean]
```




    0    a
    dtype: object



第二点是在进行逻辑运算时， bool 类型在缺失处返回的永远是 False ，而 boolean 会根据逻辑运算是否能确定唯一结果来返回相应的值。那什么叫能否确定唯一结果呢？举个简单例子： True | pd.NA 中无论缺失值为什么值，必然返回 True ； False | pd.NA 中的结果会根据缺失值取值的不同而变化，此时返回 pd.NA ； False & pd.NA 中无论缺失值为什么值，必然返回 False 。


```python
s_boolean & True
```




    0    True
    1    <NA>
    dtype: boolean




```python
s_boolean | True
```




    0    True
    1    True
    dtype: boolean




```python
 ~s_boolean 
```




    0    False
    1     <NA>
    dtype: boolean



### 3. 缺失数据的计算和分组

当调用函数 sum, prob 使用加法和乘法的时候，缺失数据等价于被分别视作0和1，即不改变原来的计算结果：


```python
 s = pd.Series([2,3,np.nan,4,5])
s.sum()
```




    14.0




```python
s.prod()
```




    120.0




```python
s.cumsum()
```




    0     2.0
    1     5.0
    2     NaN
    3     9.0
    4    14.0
    dtype: float64



当进行单个标量运算的时候，除了 np.nan ** 0 和 1 ** np.nan 这两种情况为确定的值之外，所有运算结果全为缺失（ pd.NA 的行为与此一致 ），并且 np.nan 在比较操作时一定返回 False ，而 pd.NA 返回 pd.NA ：


```python
np.nan == 0

```




    False




```python
pd.NA == 0
```




    <NA>




```python
np.nan > 0
```




    False




```python
pd.NA > 0
```




    <NA>




```python
np.nan + 1
```




    nan




```python
np.log(np.nan)
```




    nan




```python
np.add(np.nan, 1)
```




    nan




```python
np.nan ** 0
```




    1.0




```python
pd.NA ** 0
```




    1




```python
1 ** np.nan
```




    1.0




```python
1 ** pd.NA
```




    1



 diff, pct_change 这两个函数虽然功能相似，但是对于缺失的处理不同，前者凡是参与缺失计算的部分全部设为了缺失值，而后者缺失值位置会被设为 0% 的变化率：


```python
s.diff()
```




    0    NaN
    1    1.0
    2    NaN
    3    NaN
    4    1.0
    dtype: float64




```python
s.pct_change()
```




    0         NaN
    1    0.500000
    2    0.000000
    3    0.333333
    4    0.250000
    dtype: float64




```python

```
