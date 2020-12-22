
# 一、索引器

## 1.表的列索引


```python
import numpy as np
import pandas as pd
df = pd.read_csv(r"C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv",
                 usecols = ['School', 'Grade', 'Name', 'Gender',
                              'Weight', 'Transfer'])
df['Name'].head()
```




    0      Gaopeng Yang
    1    Changqiang You
    2           Mei Sun
    3      Xiaojuan Sun
    4       Gaojuan You
    Name: Name, dtype: object




```python
df[['Gender','Name']].head()#获得多个列
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
      <th>Gender</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>Gaopeng Yang</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>Changqiang You</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Male</td>
      <td>Mei Sun</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Female</td>
      <td>Xiaojuan Sun</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Male</td>
      <td>Gaojuan You</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.Name.head()#获得单列，且列名中不包空和上面df['Name']是一样的
```




    0      Gaopeng Yang
    1    Changqiang You
    2           Mei Sun
    3      Xiaojuan Sun
    4       Gaojuan You
    Name: Name, dtype: object



### 2.序列的行索引

#### 以字符串为索引的 Series


```python
A = pd.Series([1,2,3,4,5,6],index=['a','b','a','a','a','c'])
A['a']
```




    a    1
    a    3
    a    4
    dtype: int64




```python
#如果取出多个索引的对应元素，则可以使用 [items的列表] ：
A[['c','b']]
```




    c    6
    b    5
    dtype: int64




```python
A = pd.Series([1,2,3,4,5,6],index=['a','b','a','a','a','c'])
A['c': 'b': -1]#获得两个索引之间的元素
```




    c    6
    a    5
    a    4
    a    3
    b    2
    dtype: int64



### 3. loc索引器

前面讲到了对 DataFrame 的列进行选取，下面要讨论其行的选取。对于表而言，有两种索引器，一种是基于 元素 的 loc 索引器，另一种是基于 位置 的 
iloc 索引器。loc 索引器的一般形式是 loc[*, *] ，其中第一个 * 代表行的选择，第二个 * 代表列的选择，如果省略第二个位置写作 loc[*] ，这个 *
是指行的筛选。其中， * 的位置一共有五类合法对象，分别是：单个元素、元素列表、元素切片、布尔列表以及函数，下面将依次说明。
为了演示相应操作，先利用 set_index 方法把 Name 列设为索引，关于该函数的其他用法将在多级索引一章介绍。


```python
import numpy as np
import pandas as pd
df = pd.read_csv(r"C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv",
                 usecols = ['School', 'Grade', 'Name', 'Gender',
                              'Weight', 'Transfer'])
df_A =df.set_index('Name')
df_A.head()
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
      <th>School</th>
      <th>Grade</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Gaopeng Yang</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Female</td>
      <td>46.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Changqiang You</th>
      <td>Peking University</td>
      <td>Freshman</td>
      <td>Male</td>
      <td>70.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Mei Sun</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Male</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Xiaojuan Sun</th>
      <td>Fudan University</td>
      <td>Sophomore</td>
      <td>Female</td>
      <td>41.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Gaojuan You</th>
      <td>Fudan University</td>
      <td>Sophomore</td>
      <td>Male</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



 * 为单个元素


```python
df_A.loc['Qiang Sun']
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
      <th>School</th>
      <th>Grade</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Qiang Sun</th>
      <td>Tsinghua University</td>
      <td>Junior</td>
      <td>Female</td>
      <td>53.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Qiang Sun</th>
      <td>Tsinghua University</td>
      <td>Sophomore</td>
      <td>Female</td>
      <td>40.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Qiang Sun</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Junior</td>
      <td>Female</td>
      <td>NaN</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A.loc['Quan Zhao']
```




    School      Shanghai Jiao Tong University
    Grade                              Junior
    Gender                             Female
    Weight                                 53
    Transfer                                N
    Name: Quan Zhao, dtype: object




```python
df_A.loc['Qiang Sun','School']
```




    Name
    Qiang Sun              Tsinghua University
    Qiang Sun              Tsinghua University
    Qiang Sun    Shanghai Jiao Tong University
    Name: School, dtype: object



* 为元素列表


```python
#取出列表中所有元素值对应的行或列：
df_A.loc[['Qiang Sun','Quan Zhao'],['School','Gender']]

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
      <th>School</th>
      <th>Gender</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Qiang Sun</th>
      <td>Tsinghua University</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>Qiang Sun</th>
      <td>Tsinghua University</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>Qiang Sun</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>Quan Zhao</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Female</td>
    </tr>
  </tbody>
</table>
</div>



* 为切片


```python
df_A.loc['Gaojuan You':'Gaoqiang Qian','School':'Gender']#使用切片
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
      <th>School</th>
      <th>Grade</th>
      <th>Gender</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Gaojuan You</th>
      <td>Fudan University</td>
      <td>Sophomore</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>Xiaoli Qian</th>
      <td>Tsinghua University</td>
      <td>Freshman</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>Qiang Chu</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>Gaoqiang Qian</th>
      <td>Tsinghua University</td>
      <td>Junior</td>
      <td>Female</td>
    </tr>
  </tbody>
</table>
</div>



 * 为布尔列表

在实际的数据处理中，根据条件来筛选行是极其常见的，此处传入 loc 的布尔列表与 DataFrame 
长度相同，且列表为 True 的位置所对应的行会被选中， False 则会被剔除。


```python
df_A.loc[df_A.Weight>70].head()
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
      <th>School</th>
      <th>Grade</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mei Sun</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Male</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Gaojuan You</th>
      <td>Fudan University</td>
      <td>Sophomore</td>
      <td>Male</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Xiaopeng Zhou</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Male</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Xiaofeng Sun</th>
      <td>Tsinghua University</td>
      <td>Senior</td>
      <td>Male</td>
      <td>71.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Qiang Zheng</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Male</td>
      <td>87.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A.loc[df_A.Grade.isin(['Freshman', 'Senior'])].head()#获得大一和大四的学生
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
      <th>School</th>
      <th>Grade</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Gaopeng Yang</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Female</td>
      <td>46.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Changqiang You</th>
      <td>Peking University</td>
      <td>Freshman</td>
      <td>Male</td>
      <td>70.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Mei Sun</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Male</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Xiaoli Qian</th>
      <td>Tsinghua University</td>
      <td>Freshman</td>
      <td>Female</td>
      <td>51.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Qiang Chu</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Female</td>
      <td>52.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



 * 为函数


```python
def condition(x):
        condition_1_1 = x.School == 'Fudan University'
        condition_1_2 = x.Grade == 'Senior'
        condition_1_3 = x.Weight > 70
        condition_1 = condition_1_1 & condition_1_2 & condition_1_3
        condition_2_1 = x.School == 'Peking University'
        condition_2_2 = x.Grade == 'Senior'
        condition_2_3 = x.Weight > 80
        condition_2 = condition_2_1 & (~condition_2_2) & condition_2_3
        result = condition_1 | condition_2
        return result
df_A.loc[condition]
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
      <th>School</th>
      <th>Grade</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Qiang Han</th>
      <td>Peking University</td>
      <td>Freshman</td>
      <td>Male</td>
      <td>87.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Chengpeng Zhou</th>
      <td>Fudan University</td>
      <td>Senior</td>
      <td>Male</td>
      <td>81.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Changpeng Zhao</th>
      <td>Peking University</td>
      <td>Freshman</td>
      <td>Male</td>
      <td>83.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Chengpeng Qian</th>
      <td>Fudan University</td>
      <td>Senior</td>
      <td>Male</td>
      <td>73.0</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
#由于函数无法返回如 start: end: step 的切片形式，故返回切片时要用 slice 对象进行包装：
df_A.loc[lambda x: slice('Gaojuan You','Gaoqiang Qian')]
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
      <th>School</th>
      <th>Grade</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Gaojuan You</th>
      <td>Fudan University</td>
      <td>Sophomore</td>
      <td>Male</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Xiaoli Qian</th>
      <td>Tsinghua University</td>
      <td>Freshman</td>
      <td>Female</td>
      <td>51.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Qiang Chu</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Female</td>
      <td>52.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Gaoqiang Qian</th>
      <td>Tsinghua University</td>
      <td>Junior</td>
      <td>Female</td>
      <td>50.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



#### 4. iloc索引器

iloc 的使用与 loc 完全类似，只不过是针对位置进行筛选，在相应的 * 位置处一共也有五类
合法对象，分别是：整数、整数列表、整数切片、布尔列表以及函数，函数的返回值必须是前面
的四类合法对象中的一个，其输入同样也为 DataFrame 本身。


```python
df_A.iloc[1, 1] # 第二行第二列
```




    'Freshman'




```python
df_A.iloc[[0,1],[0,1]]
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
      <th>School</th>
      <th>Grade</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Gaopeng Yang</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
    </tr>
    <tr>
      <th>Changqiang You</th>
      <td>Peking University</td>
      <td>Freshman</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A.iloc[1: 4, 2:4] # 切片不包含结束端点
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
      <th>Gender</th>
      <th>Weight</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Changqiang You</th>
      <td>Male</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>Mei Sun</th>
      <td>Male</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>Xiaojuan Sun</th>
      <td>Female</td>
      <td>41.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 5. query方法


```python
#在 pandas 中，支持把字符串形式的查询表达式传入 query 方法来查询数据，其表
#达式的执行结果必须返回布尔列表
df.query('((School == "Fudan University")&(Grade == "Senior")&(Weight > 70))')
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
      <th>School</th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>66</th>
      <td>Fudan University</td>
      <td>Senior</td>
      <td>Chengpeng Zhou</td>
      <td>Male</td>
      <td>81.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>131</th>
      <td>Fudan University</td>
      <td>Senior</td>
      <td>Chengpeng Qian</td>
      <td>Male</td>
      <td>73.0</td>
      <td>Y</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.query('Grade == ["Junior", "Senior"]').head()
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
      <th>School</th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Mei Sun</td>
      <td>Male</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Tsinghua University</td>
      <td>Junior</td>
      <td>Gaoqiang Qian</td>
      <td>Female</td>
      <td>50.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Peking University</td>
      <td>Junior</td>
      <td>Juan Xu</td>
      <td>Female</td>
      <td>NaN</td>
      <td>N</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Tsinghua University</td>
      <td>Junior</td>
      <td>Xiaoquan Lv</td>
      <td>Female</td>
      <td>43.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Peng You</td>
      <td>Female</td>
      <td>48.0</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
low, high =70, 80
df.query('Weight.between(@low, @high)').head()
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-73-7b9719bb38f0> in <module>
          1 low, high =70, 80
    ----> 2 df.query('Weight.between(@low, @high)').head()
    

    D:\Anaconda3\lib\site-packages\pandas\core\frame.py in query(self, expr, inplace, **kwargs)
       3343         kwargs["level"] = kwargs.pop("level", 0) + 1
       3344         kwargs["target"] = None
    -> 3345         res = self.eval(expr, **kwargs)
       3346 
       3347         try:
    

    D:\Anaconda3\lib\site-packages\pandas\core\frame.py in eval(self, expr, inplace, **kwargs)
       3473         kwargs["resolvers"] = kwargs.get("resolvers", ()) + tuple(resolvers)
       3474 
    -> 3475         return _eval(expr, inplace=inplace, **kwargs)
       3476 
       3477     def select_dtypes(self, include=None, exclude=None) -> "DataFrame":
    

    D:\Anaconda3\lib\site-packages\pandas\core\computation\eval.py in eval(expr, parser, engine, truediv, local_dict, global_dict, resolvers, level, target, inplace)
        344         eng = _engines[engine]
        345         eng_inst = eng(parsed_expr)
    --> 346         ret = eng_inst.evaluate()
        347 
        348         if parsed_expr.assigner is None:
    

    D:\Anaconda3\lib\site-packages\pandas\core\computation\engines.py in evaluate(self)
         71 
         72         # make sure no names in resolvers and locals/globals clash
    ---> 73         res = self._evaluate()
         74         return reconstruct_object(
         75             self.result_type, res, self.aligned_axes, self.expr.terms.return_type
    

    D:\Anaconda3\lib\site-packages\pandas\core\computation\engines.py in _evaluate(self)
        111         env = self.expr.env
        112         scope = env.full_scope
    --> 113         _check_ne_builtin_clash(self.expr)
        114         return ne.evaluate(s, local_dict=scope)
        115 
    

    D:\Anaconda3\lib\site-packages\pandas\core\computation\engines.py in _check_ne_builtin_clash(expr)
         27         Terms can contain
         28     """
    ---> 29     names = expr.names
         30     overlap = names & _ne_builtins
         31 
    

    D:\Anaconda3\lib\site-packages\pandas\core\computation\expr.py in names(self)
        812         """
        813         if is_term(self.terms):
    --> 814             return frozenset([self.terms.name])
        815         return frozenset(term.name for term in com.flatten(self.terms))
        816 
    

    D:\Anaconda3\lib\site-packages\pandas\core\generic.py in __hash__(self)
       1667     def __hash__(self):
       1668         raise TypeError(
    -> 1669             f"{repr(type(self).__name__)} objects are mutable, "
       1670             f"thus they cannot be hashed"
       1671         )
    

    TypeError: 'Series' objects are mutable, thus they cannot be hashed


#### 6. 随机抽样


```python
df_A = pd.DataFrame({'id': list('abcde'),
                          'value': [10, 20, 30, 20, 20]})
df_A
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
      <th>id</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>30</td>
    </tr>
    <tr>
      <th>3</th>
      <td>d</td>
      <td>20</td>
    </tr>
    <tr>
      <th>4</th>
      <td>e</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A.sample(3,replace = True,weights = df_A.value)
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
      <th>id</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>d</td>
      <td>20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>30</td>
    </tr>
    <tr>
      <th>4</th>
      <td>e</td>
      <td>20</td>
    </tr>
  </tbody>
</table>
</div>



## 二、多级索引

### 1. 多级索引及其表的结构


```python
import numpy as np
import pandas as pd
np.random.seed(0)
multi_index = pd.MultiIndex.from_product([list('ABCD'),
               df.Gender.unique()], names=('School', 'Gender'))#重新建表
multi_column = pd.MultiIndex.from_product([['Height', 'Weight'],
                   df.Grade.unique()], names=('Indicator', 'Grade'))
df_multi = pd.DataFrame(np.c_[(np.random.randn(8,4)*5 + 163).tolist(),
                            (np.random.randn(8,4)*5 + 65).tolist()],
                            index = multi_index,
                            columns = multi_column).round(1)
df_multi
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Indicator</th>
      <th colspan="4" halign="left">Height</th>
      <th colspan="4" halign="left">Weight</th>
    </tr>
    <tr>
      <th></th>
      <th>Grade</th>
      <th>Freshman</th>
      <th>Senior</th>
      <th>Sophomore</th>
      <th>Junior</th>
      <th>Freshman</th>
      <th>Senior</th>
      <th>Sophomore</th>
      <th>Junior</th>
    </tr>
    <tr>
      <th>School</th>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>Female</th>
      <td>171.8</td>
      <td>165.0</td>
      <td>167.9</td>
      <td>174.2</td>
      <td>60.6</td>
      <td>55.1</td>
      <td>63.3</td>
      <td>65.8</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>172.3</td>
      <td>158.1</td>
      <td>167.8</td>
      <td>162.2</td>
      <td>71.2</td>
      <td>71.0</td>
      <td>63.1</td>
      <td>63.5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>Female</th>
      <td>162.5</td>
      <td>165.1</td>
      <td>163.7</td>
      <td>170.3</td>
      <td>59.8</td>
      <td>57.9</td>
      <td>56.5</td>
      <td>74.8</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>166.8</td>
      <td>163.6</td>
      <td>165.2</td>
      <td>164.7</td>
      <td>62.5</td>
      <td>62.8</td>
      <td>58.7</td>
      <td>68.9</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">C</th>
      <th>Female</th>
      <td>170.5</td>
      <td>162.0</td>
      <td>164.6</td>
      <td>158.7</td>
      <td>56.9</td>
      <td>63.9</td>
      <td>60.5</td>
      <td>66.9</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>150.2</td>
      <td>166.3</td>
      <td>167.3</td>
      <td>159.3</td>
      <td>62.4</td>
      <td>59.1</td>
      <td>64.9</td>
      <td>67.1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">D</th>
      <th>Female</th>
      <td>174.3</td>
      <td>155.7</td>
      <td>163.2</td>
      <td>162.1</td>
      <td>65.3</td>
      <td>66.5</td>
      <td>61.8</td>
      <td>63.2</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>170.7</td>
      <td>170.3</td>
      <td>163.8</td>
      <td>164.9</td>
      <td>61.6</td>
      <td>63.2</td>
      <td>60.9</td>
      <td>56.4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_multi.index.names
```




    FrozenList(['School', 'Gender'])




```python
df_multi.columns.names
```




    FrozenList(['Indicator', 'Grade'])




```python
df_multi.index.get_level_values(0)#获得某一层的索引
```




    Index(['A', 'A', 'B', 'B', 'C', 'C', 'D', 'D'], dtype='object', name='School')



### 2. 多级索引中的loc索引器

熟悉了结构后，现在回到原表，将学校和年级设为索引，此时的行为多级索引，列为单级索引，
由于默认状态的列索引不含名字，因此对应于刚刚图中 Indicator 和 Grade 的索引名位置是空缺的。


```python
df_multi = df.set_index(['School','Grade'])
df_multi.head()

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
      <th></th>
      <th>Name</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>School</th>
      <th>Grade</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Shanghai Jiao Tong University</th>
      <th>Freshman</th>
      <td>Gaopeng Yang</td>
      <td>Female</td>
      <td>46.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Peking University</th>
      <th>Freshman</th>
      <td>Changqiang You</td>
      <td>Male</td>
      <td>70.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Shanghai Jiao Tong University</th>
      <th>Senior</th>
      <td>Mei Sun</td>
      <td>Male</td>
      <td>89.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Fudan University</th>
      <th>Sophomore</th>
      <td>Xiaojuan Sun</td>
      <td>Female</td>
      <td>41.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Sophomore</th>
      <td>Gaojuan You</td>
      <td>Male</td>
      <td>74.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



由于多级索引中的单个元素以元组为单位，因此之前在第一节介绍的 loc 和 iloc 方法完全可以照搬
，只需把标量的位置替换成对应的元组，不过在索引前最好对 MultiIndex 进行排序以避免性能警告：


```python
df_multi = df_multi.sort_index()
df_multi.loc[('Fudan University','Junior')].head()
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
      <th></th>
      <th>Name</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>School</th>
      <th>Grade</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Fudan University</th>
      <th>Junior</th>
      <td>Yanli You</td>
      <td>Female</td>
      <td>48.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Junior</th>
      <td>Chunqiang Chu</td>
      <td>Male</td>
      <td>72.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Junior</th>
      <td>Changfeng Lv</td>
      <td>Male</td>
      <td>76.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Junior</th>
      <td>Yanjuan Lv</td>
      <td>Female</td>
      <td>49.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Junior</th>
      <td>Gaoqiang Zhou</td>
      <td>Female</td>
      <td>43.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_multi.loc[[('Fudan University', 'Senior'),
                  ('Shanghai Jiao Tong University', 'Freshman')]].head()
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
      <th></th>
      <th>Name</th>
      <th>Gender</th>
      <th>Weight</th>
      <th>Transfer</th>
    </tr>
    <tr>
      <th>School</th>
      <th>Grade</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Fudan University</th>
      <th>Senior</th>
      <td>Chengpeng Zheng</td>
      <td>Female</td>
      <td>38.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Senior</th>
      <td>Feng Zhou</td>
      <td>Female</td>
      <td>47.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Senior</th>
      <td>Gaomei Lv</td>
      <td>Female</td>
      <td>34.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Senior</th>
      <td>Chunli Lv</td>
      <td>Female</td>
      <td>56.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>Senior</th>
      <td>Chengpeng Zhou</td>
      <td>Male</td>
      <td>81.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
</div>



### 3. IndexSlice对象

前面介绍的方法，即使在索引不重复的时候，也只能对元组整体进行切片，而不能对每层进行切片，
也不允许将切片和布尔列表混合使用，引入 IndexSlice 对象就能解决这个问题。 Slice 对象一共
有两种形式，第一种为 loc[idx[*,*]] 型，第二种为 loc[idx[*,*],idx[*,*]] 型，
下面将进行介绍。为了方便演示，下面构造一个 索引不重复的 DataFrame ：


```python
np.random.seed(0)
L1,L2 = ['A','B','C'],['a','b','c']
mul_index1 = pd.MultiIndex.from_product([L1,L2],names=('Upper', 'Lower'))
L3,L4 = ['D','E','F'],['d','e','f']
mul_index2 = pd.MultiIndex.from_product([L3,L4],names=('Big', 'Small'))
df_ex = pd.DataFrame(np.random.randint(-9,10,(9,9)),index=mul_index1,columns=mul_index2)
df_ex
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Big</th>
      <th colspan="3" halign="left">D</th>
      <th colspan="3" halign="left">E</th>
      <th colspan="3" halign="left">F</th>
    </tr>
    <tr>
      <th></th>
      <th>Small</th>
      <th>d</th>
      <th>e</th>
      <th>f</th>
      <th>d</th>
      <th>e</th>
      <th>f</th>
      <th>d</th>
      <th>e</th>
      <th>f</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">A</th>
      <th>a</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>b</th>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
      <td>-4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>c</th>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">B</th>
      <th>a</th>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
      <td>-9</td>
      <td>-5</td>
      <td>-4</td>
      <td>-3</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>c</th>
      <td>8</td>
      <td>6</td>
      <td>-5</td>
      <td>0</td>
      <td>1</td>
      <td>-8</td>
      <td>-8</td>
      <td>-2</td>
      <td>0</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">C</th>
      <th>a</th>
      <td>-6</td>
      <td>-3</td>
      <td>2</td>
      <td>5</td>
      <td>9</td>
      <td>-9</td>
      <td>5</td>
      <td>-6</td>
      <td>3</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1</td>
      <td>2</td>
      <td>-5</td>
      <td>-3</td>
      <td>-5</td>
      <td>6</td>
      <td>-6</td>
      <td>3</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>-1</td>
      <td>5</td>
      <td>6</td>
      <td>-6</td>
      <td>6</td>
      <td>4</td>
      <td>7</td>
      <td>8</td>
      <td>-4</td>
    </tr>
  </tbody>
</table>
</div>




```python
index = pd.IndexSlice#定义slice对象
df_ex.loc[index['C':,('D','e'):]]#loc[idx[*,*]] 型
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Big</th>
      <th colspan="2" halign="left">D</th>
      <th colspan="3" halign="left">E</th>
      <th colspan="3" halign="left">F</th>
    </tr>
    <tr>
      <th></th>
      <th>Small</th>
      <th>e</th>
      <th>f</th>
      <th>d</th>
      <th>e</th>
      <th>f</th>
      <th>d</th>
      <th>e</th>
      <th>f</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">C</th>
      <th>a</th>
      <td>-3</td>
      <td>2</td>
      <td>5</td>
      <td>9</td>
      <td>-9</td>
      <td>5</td>
      <td>-6</td>
      <td>3</td>
    </tr>
    <tr>
      <th>b</th>
      <td>2</td>
      <td>-5</td>
      <td>-3</td>
      <td>-5</td>
      <td>6</td>
      <td>-6</td>
      <td>3</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>c</th>
      <td>5</td>
      <td>6</td>
      <td>-6</td>
      <td>6</td>
      <td>4</td>
      <td>7</td>
      <td>8</td>
      <td>-4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ex.loc[index[:'A', lambda x:x.sum()>0]] # 列和大于0
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Big</th>
      <th colspan="2" halign="left">D</th>
      <th>F</th>
    </tr>
    <tr>
      <th></th>
      <th>Small</th>
      <th>d</th>
      <th>e</th>
      <th>e</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">A</th>
      <th>a</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
    <tr>
      <th>b</th>
      <td>-3</td>
      <td>3</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>c</th>
      <td>-1</td>
      <td>0</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ex.loc[index[:'A', 'b':], index['E':, 'e':]]#loc[idx[*,*],idx[*,*]] 型前一个 idx 指代的是行索引，后一个是列索引。
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Big</th>
      <th colspan="2" halign="left">E</th>
      <th colspan="2" halign="left">F</th>
    </tr>
    <tr>
      <th></th>
      <th>Small</th>
      <th>e</th>
      <th>f</th>
      <th>e</th>
      <th>f</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>b</th>
      <td>-2</td>
      <td>5</td>
      <td>-4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>c</th>
      <td>6</td>
      <td>6</td>
      <td>9</td>
      <td>-6</td>
    </tr>
  </tbody>
</table>
</div>



### 4. 多级索引的构造

前面提到了多级索引表的结构和切片，那么除了使用 set_index 之外，
如何自己构造多级索引呢？常用的有 from_tuples, from_arrays, from_product 三种方法，
它们都是 pd.MultiIndex 对象下的函数。


```python
#from_tuples 指根据传入由元组组成的列表进行构造：
my_A = [('a','cat'),('a','dog'),('b','cat'),('b','dog')]
pd.MultiIndex.from_tuples(my_A,names = ['First','Second'])
```




    MultiIndex([('a', 'cat'),
                ('a', 'dog'),
                ('b', 'cat'),
                ('b', 'dog')],
               names=['First', 'Second'])




```python
#from_arrays 根据传入列表中，对应层的列表进行构造：
my_array = [list('aabb'), ['cat', 'dog']*2]
pd.MultiIndex.from_arrays(my_array, names=['First','Second'])
```




    MultiIndex([('a', 'cat'),
                ('a', 'dog'),
                ('b', 'cat'),
                ('b', 'dog')],
               names=['First', 'Second'])




```python
#from_product 指根据给定多个列表的笛卡尔积进行构造：
list1 = ['a','b']
list2 = ['cat','dog']
pd.MultiIndex.from_product([list1,list2],names = ['First','Second'])
```




    MultiIndex([('a', 'cat'),
                ('a', 'dog'),
                ('b', 'cat'),
                ('b', 'dog')],
               names=['First', 'Second'])



## 三、索引的常用方法

### 1. 索引层的交换和删除


```python
np.random.seed(0)
L1,L2,L3 = ['A','B'],['a','b'],['alpha','beta']
m_index1 = pd.MultiIndex.from_product([L1,L2,L3],names = ('Upper','Lower','Extra'))
L4,L5,L6 = ['C','D'],['c','d'],['cat','dog']
m_index2 = pd.MultiIndex.from_product([L4,L5,L6],names=('Big', 'Small', 'Other'))
df_ex = pd.DataFrame(np.random.randint(-9,10,(8,8)),index=m_index1,columns=m_index2)
df_ex

 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Big</th>
      <th colspan="4" halign="left">C</th>
      <th colspan="4" halign="left">D</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Small</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Other</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th>Extra</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">A</th>
      <th rowspan="2" valign="top">a</th>
      <th>alpha</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>alpha</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">B</th>
      <th rowspan="2" valign="top">a</th>
      <th>alpha</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>-5</td>
      <td>-4</td>
      <td>-3</td>
      <td>-1</td>
      <td>8</td>
      <td>6</td>
      <td>-5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>alpha</th>
      <td>0</td>
      <td>1</td>
      <td>-8</td>
      <td>-8</td>
      <td>-2</td>
      <td>0</td>
      <td>-6</td>
      <td>-3</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>2</td>
      <td>5</td>
      <td>9</td>
      <td>-9</td>
      <td>5</td>
      <td>-6</td>
      <td>3</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ex.swaplevel(0,2,axis=1).head() # 列索引的第一层和第三层交换
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Other</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Small</th>
      <th>c</th>
      <th>c</th>
      <th>d</th>
      <th>d</th>
      <th>c</th>
      <th>c</th>
      <th>d</th>
      <th>d</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Big</th>
      <th>C</th>
      <th>C</th>
      <th>C</th>
      <th>C</th>
      <th>D</th>
      <th>D</th>
      <th>D</th>
      <th>D</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th>Extra</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">A</th>
      <th rowspan="2" valign="top">a</th>
      <th>alpha</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>alpha</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>B</th>
      <th>a</th>
      <th>alpha</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
  </tbody>
</table>
</div>




```python
 df_ex.reorder_levels([2,0,1],axis=0).head() # 列表数字指代原来索引中的层
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Big</th>
      <th colspan="4" halign="left">C</th>
      <th colspan="4" halign="left">D</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Small</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Other</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th>Extra</th>
      <th>Upper</th>
      <th>Lower</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>alpha</th>
      <th>A</th>
      <th>a</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>beta</th>
      <th>A</th>
      <th>a</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>alpha</th>
      <th>A</th>
      <th>b</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>beta</th>
      <th>A</th>
      <th>b</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>alpha</th>
      <th>B</th>
      <th>a</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ex.droplevel(1,axis=1)#删除某一层的索引
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Big</th>
      <th colspan="4" halign="left">C</th>
      <th colspan="4" halign="left">D</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Other</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th>Extra</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">A</th>
      <th rowspan="2" valign="top">a</th>
      <th>alpha</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>alpha</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">B</th>
      <th rowspan="2" valign="top">a</th>
      <th>alpha</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>-5</td>
      <td>-4</td>
      <td>-3</td>
      <td>-1</td>
      <td>8</td>
      <td>6</td>
      <td>-5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>alpha</th>
      <td>0</td>
      <td>1</td>
      <td>-8</td>
      <td>-8</td>
      <td>-2</td>
      <td>0</td>
      <td>-6</td>
      <td>-3</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>2</td>
      <td>5</td>
      <td>9</td>
      <td>-9</td>
      <td>5</td>
      <td>-6</td>
      <td>3</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ex.droplevel([0,1],axis=0)#删除列索引
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>Big</th>
      <th colspan="4" halign="left">C</th>
      <th colspan="4" halign="left">D</th>
    </tr>
    <tr>
      <th>Small</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
    </tr>
    <tr>
      <th>Other</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th>Extra</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>alpha</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>alpha</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>alpha</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>-5</td>
      <td>-4</td>
      <td>-3</td>
      <td>-1</td>
      <td>8</td>
      <td>6</td>
      <td>-5</td>
    </tr>
    <tr>
      <th>alpha</th>
      <td>0</td>
      <td>1</td>
      <td>-8</td>
      <td>-8</td>
      <td>-2</td>
      <td>0</td>
      <td>-6</td>
      <td>-3</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>2</td>
      <td>5</td>
      <td>9</td>
      <td>-9</td>
      <td>5</td>
      <td>-6</td>
      <td>3</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### 2.索引属性的修改


```python
df_ex.rename_axis(index = {'Uper':'Changed_row'},columns = {'Other':'Changed_Col'})
.head()#修改索引层名字rename_axis
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Big</th>
      <th colspan="4" halign="left">C</th>
      <th colspan="4" halign="left">D</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Small</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Changed_Col</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th>Extra</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">A</th>
      <th rowspan="2" valign="top">a</th>
      <th>alpha</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>alpha</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>B</th>
      <th>a</th>
      <th>alpha</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ex.rename(columns={'cat':'not_cat'},level=2).head()#修改索引值rename
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Big</th>
      <th colspan="4" halign="left">C</th>
      <th colspan="4" halign="left">D</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Small</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Other</th>
      <th>not_cat</th>
      <th>dog</th>
      <th>not_cat</th>
      <th>dog</th>
      <th>not_cat</th>
      <th>dog</th>
      <th>not_cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th>Extra</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">A</th>
      <th rowspan="2" valign="top">a</th>
      <th>alpha</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>alpha</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>beta</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>B</th>
      <th>a</th>
      <th>alpha</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_ex.rename(index=lambda x:str.upper(x),level=2).head()#通过函数修改索引值
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th></th>
      <th>Big</th>
      <th colspan="4" halign="left">C</th>
      <th colspan="4" halign="left">D</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Small</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
      <th colspan="2" halign="left">c</th>
      <th colspan="2" halign="left">d</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>Other</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
      <th>cat</th>
      <th>dog</th>
    </tr>
    <tr>
      <th>Upper</th>
      <th>Lower</th>
      <th>Extra</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="4" valign="top">A</th>
      <th rowspan="2" valign="top">a</th>
      <th>ALPHA</th>
      <td>3</td>
      <td>6</td>
      <td>-9</td>
      <td>-6</td>
      <td>-6</td>
      <td>-2</td>
      <td>0</td>
      <td>9</td>
    </tr>
    <tr>
      <th>BETA</th>
      <td>-5</td>
      <td>-3</td>
      <td>3</td>
      <td>-8</td>
      <td>-3</td>
      <td>-2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">b</th>
      <th>ALPHA</th>
      <td>-4</td>
      <td>4</td>
      <td>-1</td>
      <td>0</td>
      <td>7</td>
      <td>-4</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>BETA</th>
      <td>-9</td>
      <td>9</td>
      <td>-6</td>
      <td>8</td>
      <td>5</td>
      <td>-2</td>
      <td>-9</td>
      <td>-8</td>
    </tr>
    <tr>
      <th>B</th>
      <th>a</th>
      <th>ALPHA</th>
      <td>0</td>
      <td>-9</td>
      <td>1</td>
      <td>-6</td>
      <td>2</td>
      <td>9</td>
      <td>-7</td>
      <td>-9</td>
    </tr>
  </tbody>
</table>
</div>




```python
A = iter(list('abcdefgh'))
df_ex.rename(index=lambda x:next(A),level = 2)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-80-bc33686b6fdf> in <module>
    ----> 1 A = iter(list('abcdefgh'))
          2 df_ex.rename(index=lambda x:next(A),level = 2)
    

    TypeError: 'list' object is not callable


### 3. 索引的设置与重置


```python
df_A = pd.DataFrame({"A":list('aacd'),"B":list('PQRT'),"C":[1,2,3,4]})
df_A
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-86-2fdf41795bad> in <module>
    ----> 1 df_A = pd.DataFrame({"A":list('aacd'),"B":list('PQRT'),"C":[1,2,3,4]})
          2 df_A
    

    TypeError: 'list' object is not callable


### 4. 索引的变形


```python
df_reindex = pd.DataFrame({"Weight":[60,70,80], "Height":[176,180,179]}, index=['1001','1003','1002'])
df_reindex
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
      <th>Weight</th>
      <th>Height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1001</th>
      <td>60</td>
      <td>176</td>
    </tr>
    <tr>
      <th>1003</th>
      <td>70</td>
      <td>180</td>
    </tr>
    <tr>
      <th>1002</th>
      <td>80</td>
      <td>179</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_reindex.reindex(index=['1001','1002','1003','1004'],columns=['Weight','Gender'])
#增加一行的同时，去掉一列并新增一列
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
      <th>Weight</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1001</th>
      <td>60.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1002</th>
      <td>80.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1003</th>
      <td>70.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1004</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_existed = pd.DataFrame(index = ['1001','1002','1003','1004'],columns=['Weight','Gender'])
df_reindex.reindex_like(df_existed)
# reindex_like与reindex相似 ，其功能是仿照传入的表的索引来进行被调用表索引的变形。
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
      <th>Weight</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1001</th>
      <td>60.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1002</th>
      <td>80.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1003</th>
      <td>70.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1004</th>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## 四、索引运算

### 2. 一般的索引运算


```python
df_A = pd.DataFrame([[0,1],[1,2],[3,4]],
                        index = pd.Index(['a','b','a'],name='id1'))
df_B = pd.DataFrame([[4,5],[2,6],[7,1]],index = pd.Index(['b','b','c'],name='id2'))
id1,id2 = df_A.index.unique(),df_B.index.unique()
id1.intersection(id2)
```




    Index(['b'], dtype='object')




```python
id1.union(id2)
```




    Index(['a', 'b', 'c'], dtype='object')




```python
id1.difference(id2)
```




    Index(['a'], dtype='object')




```python
id1.symmetric_difference(id2)
```




    Index(['a', 'c'], dtype='object')




```python
#若两张表需要做集合运算的列并没有被设置索引，一种办法是先转成索引，运算后再恢复，
#另一种方法是利用 isin 函数
df_a = df_A.reset_index()
df_b = df_B.reset_index()
df_a
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
      <th>id1</th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>3</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_b
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
      <th>id2</th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b</td>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>2</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>7</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_a[df_a.id1.isin(df_b.id2)]
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
      <th>id1</th>
      <th>0</th>
      <th>1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>1</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



## 五、练习

### Ex1：公司员工数据集


```python
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data/company.csv')
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
      <th>EmployeeID</th>
      <th>birthdate_key</th>
      <th>age</th>
      <th>city_name</th>
      <th>department</th>
      <th>job_title</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1318</td>
      <td>1/3/1954</td>
      <td>61</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>CEO</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1319</td>
      <td>1/3/1957</td>
      <td>58</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>VP Stores</td>
      <td>F</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1320</td>
      <td>1/2/1955</td>
      <td>60</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>Legal Counsel</td>
      <td>F</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1321</td>
      <td>1/2/1959</td>
      <td>56</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>VP Human Resources</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1322</td>
      <td>1/9/1958</td>
      <td>57</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>VP Finance</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>



分别只使用 query 和 loc 选出年龄不超过四十岁且工作部门为 Dairy 或 Bakery 的男性。


```python
df.query('(age <= 40)&(department is in ['Diary','Bakery'])&(gender=='M')').head()
```


      File "<ipython-input-108-aa2a95f52718>", line 1
        df.query('(age <= 40)&(department is in ['Diary','Bakery'])&(gender=='M')').head()
                                                      ^
    SyntaxError: invalid syntax
    


选出员工 ID 号 为奇数所在行的第1、第3和倒数第2列。


```python
df.iloc[(df.EmployeeID%2==1).values,[0,2,-2]].head()
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
      <th>EmployeeID</th>
      <th>age</th>
      <th>job_title</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>1319</td>
      <td>58</td>
      <td>VP Stores</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1321</td>
      <td>56</td>
      <td>VP Human Resources</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1323</td>
      <td>53</td>
      <td>Exec Assistant, VP Stores</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1325</td>
      <td>51</td>
      <td>Exec Assistant, Legal Counsel</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1329</td>
      <td>48</td>
      <td>Store Manager</td>
    </tr>
  </tbody>
</table>
</div>



按照以下步骤进行索引操作：

把后三列设为索引后交换内外两层


```python
df.set_index(df.columns[-3:].tolist()).swaplevel(0,2,axis=0).head()
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
      <th></th>
      <th></th>
      <th>EmployeeID</th>
      <th>birthdate_key</th>
      <th>age</th>
      <th>city_name</th>
    </tr>
    <tr>
      <th>gender</th>
      <th>job_title</th>
      <th>department</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>M</th>
      <th>CEO</th>
      <th>Executive</th>
      <td>1318</td>
      <td>1/3/1954</td>
      <td>61</td>
      <td>Vancouver</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">F</th>
      <th>VP Stores</th>
      <th>Executive</th>
      <td>1319</td>
      <td>1/3/1957</td>
      <td>58</td>
      <td>Vancouver</td>
    </tr>
    <tr>
      <th>Legal Counsel</th>
      <th>Executive</th>
      <td>1320</td>
      <td>1/2/1955</td>
      <td>60</td>
      <td>Vancouver</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">M</th>
      <th>VP Human Resources</th>
      <th>Executive</th>
      <td>1321</td>
      <td>1/2/1959</td>
      <td>56</td>
      <td>Vancouver</td>
    </tr>
    <tr>
      <th>VP Finance</th>
      <th>Executive</th>
      <td>1322</td>
      <td>1/9/1958</td>
      <td>57</td>
      <td>Vancouver</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.reset_index(level=1)#恢复中间一层
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-116-bd39f5c7cad0> in <module>
    ----> 1 df.reset_index(level=1)
    

    D:\Anaconda3\lib\site-packages\pandas\core\frame.py in reset_index(self, level, drop, inplace, col_level, col_fill)
       4818             if not isinstance(level, (tuple, list)):
       4819                 level = [level]
    -> 4820             level = [self.index._get_level_number(lev) for lev in level]
       4821             if len(level) < self.index.nlevels:
       4822                 new_index = self.index.droplevel(level)
    

    D:\Anaconda3\lib\site-packages\pandas\core\frame.py in <listcomp>(.0)
       4818             if not isinstance(level, (tuple, list)):
       4819                 level = [level]
    -> 4820             level = [self.index._get_level_number(lev) for lev in level]
       4821             if len(level) < self.index.nlevels:
       4822                 new_index = self.index.droplevel(level)
    

    D:\Anaconda3\lib\site-packages\pandas\core\indexes\base.py in _get_level_number(self, level)
       1413 
       1414     def _get_level_number(self, level) -> int:
    -> 1415         self._validate_index_level(level)
       1416         return 0
       1417 
    

    D:\Anaconda3\lib\site-packages\pandas\core\indexes\base.py in _validate_index_level(self, level)
       1405             elif level > 0:
       1406                 raise IndexError(
    -> 1407                     f"Too many levels: Index has only 1 level, not {level + 1}"
       1408                 )
       1409         elif level != self.name:
    

    IndexError: Too many levels: Index has only 1 level, not 2


修改外层索引名为 Gender


```python
df.rename_axis(index={'gender':'Gender'}).head()
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
      <th>EmployeeID</th>
      <th>birthdate_key</th>
      <th>age</th>
      <th>city_name</th>
      <th>department</th>
      <th>job_title</th>
      <th>gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1318</td>
      <td>1/3/1954</td>
      <td>61</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>CEO</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1319</td>
      <td>1/3/1957</td>
      <td>58</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>VP Stores</td>
      <td>F</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1320</td>
      <td>1/2/1955</td>
      <td>60</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>Legal Counsel</td>
      <td>F</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1321</td>
      <td>1/2/1959</td>
      <td>56</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>VP Human Resources</td>
      <td>M</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1322</td>
      <td>1/9/1958</td>
      <td>57</td>
      <td>Vancouver</td>
      <td>Executive</td>
      <td>VP Finance</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>



用下划线合并两层行索引


```python
后面题目继续再做，后面会更新到文档里面。
```
