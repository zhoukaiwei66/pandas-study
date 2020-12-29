
# 第六章 连接


```python
import numpy as np
import pandas as pd
```

## 一、关系型连接

### 值连接


```python
#通过值连接来实现左连接
df1 = pd.DataFrame({'df1_name':['San Zhang','Si Li'],'Age':[20,30]})
df2 = pd.DataFrame({'df2_name':['Si Li','Wu Wang'],'Gender':['F','M']})
df1.merge(df2, left_on='df1_name', right_on='df2_name', how='left')
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
      <th>df1_name</th>
      <th>Age</th>
      <th>df2_name</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30</td>
      <td>Si Li</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



如果两个表中的列出现了重复的列名，那么可以通过 suffixes 参数指定。例如合并考试成绩的时候，第一个表记录了语文成绩，第二个是数学成绩：


```python
df1 = pd.DataFrame({'Name':['San Zhang'],'Grade':[70]})
df2 = pd.DataFrame({'Name':['San Zhang'],'Grade':[80]})
df1.merge(df2, on='Name', how='left', suffixes=['_Chinese','_Math'])
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
      <th>Name</th>
      <th>Grade_Chinese</th>
      <th>Grade_Math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>70</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



两位同学来自不同的班级，但是姓名相同，这种时候就要指定 on 参数为多个列使得正确连接：


```python
df1 = pd.DataFrame({'Name':['San Zhang', 'San Zhang'],'Age':[20, 21],'Class':['one', 'two']})
df1   
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
      <th>Name</th>
      <th>Age</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>one</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Zhang</td>
      <td>21</td>
      <td>two</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame({'Name':['San Zhang', 'San Zhang'],'Gender':['F', 'M'],'Class':['two', 'one']})
df2
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
      <th>Name</th>
      <th>Gender</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>F</td>
      <td>two</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Zhang</td>
      <td>M</td>
      <td>one</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.merge(df2, on='Name', how='left') # 错误的结果
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
      <th>Name</th>
      <th>Age</th>
      <th>Class_x</th>
      <th>Gender</th>
      <th>Class_y</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>one</td>
      <td>F</td>
      <td>two</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>one</td>
      <td>M</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2</th>
      <td>San Zhang</td>
      <td>21</td>
      <td>two</td>
      <td>F</td>
      <td>two</td>
    </tr>
    <tr>
      <th>3</th>
      <td>San Zhang</td>
      <td>21</td>
      <td>two</td>
      <td>M</td>
      <td>one</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.merge(df2, on=['Name', 'Class'], how='left') # 正确的结果
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
      <th>Name</th>
      <th>Age</th>
      <th>Class</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>one</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Zhang</td>
      <td>21</td>
      <td>two</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



### 3. 索引连接

索引连接，就是把索引当作键，因此这和值连接本质上没有区别， pandas 中利用 join 函数来处理索引连接，它的参数选择要少于 merge ，除了必须的 on 和 how 之外，可以对重复的列指定左右后缀 lsuffix 和 rsuffix 。其中， on 参数指索引名，单层索引时省略参数表示按照当前索引连接。


```python
df1 = pd.DataFrame({'Age':[20,30]},index=pd.Series(['San Zhang','Si Li'],name='Name'))
df1
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
      <th>Age</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>San Zhang</th>
      <td>20</td>
    </tr>
    <tr>
      <th>Si Li</th>
      <td>30</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame({'Gender':['F','M']},index=pd.Series(['Si Li','Wu Wang'],name='Name'))
df2
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
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Si Li</th>
      <td>F</td>
    </tr>
    <tr>
      <th>Wu Wang</th>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.join(df2, how='left')
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
      <th>Age</th>
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
      <th>San Zhang</th>
      <td>20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Si Li</th>
      <td>30</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



## 二、方向连接

### 1. concat

在 concat 中，最常用的有三个参数，它们是 axis, join, keys ，分别表示拼接方向，连接形式，以及在新表中指示来自于哪一张旧表的名字。这里需要特别注意， join 和 keys 与之前提到的 join 函数和键的概念没有任何关系。

在默认状态下的 axis=0 ，表示纵向拼接多个表，常常用于多个样本的拼接；而 axis=1 表示横向拼接多个表，常用于多个字段或特征的拼接。


```python
#纵向合并各表中人的信息：
df1 = pd.DataFrame({'Name':['San Zhang','Si Li'],'Age':[20,30]})
df2 = pd.DataFrame({'Name':['Wu Wang'], 'Age':[40]})
pd.concat([df1,df2])
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
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Wu Wang</td>
      <td>40</td>
    </tr>
  </tbody>
</table>
</div>




```python
#横向合并各表中的字段：
df2 = pd.DataFrame({'Grade':[80, 90]})
df3 = pd.DataFrame({'Gender':['M', 'F']})
pd.concat([df1, df2, df3], 1)
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
      <th>Name</th>
      <th>Age</th>
      <th>Grade</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>80</td>
      <td>M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30</td>
      <td>90</td>
      <td>F</td>
    </tr>
  </tbody>
</table>
</div>



纵向拼接会根据列索引对其，默认状态下 join=outer ，表示保留所有的列，并将不存在的值设为缺失； join=inner ，表示保留两个表都出现过的列。横向拼接则根据行索引对齐， join 参数可以类似设置。


```python
df2 = pd.DataFrame({'Name':['Wu Wang'], 'Gender':['M']})
pd.concat([df1,df2])
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
      <th>Name</th>
      <th>Age</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Wu Wang</td>
      <td>NaN</td>
      <td>M</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame({'Grade':[80, 90]}, index=[1, 2])
pd.concat([df1, df2], 1)
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
      <th>Name</th>
      <th>Age</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30.0</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>90.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([df1, df2], axis=1, join='inner')
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
      <th>Name</th>
      <th>Age</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>



### 2. 序列与表的合并

利用 concat 可以实现多个表之间的方向拼接，如果想要把一个序列追加到表的行末或者列末，则可以分别使用 append 和 assign 方法。

在 append 中，如果原表是默认整数序列的索引，那么可以使用 ignore_index=True 对新序列对应的索引自动标号，否则必须对 Series 指定 name 属性。


```python
s = pd.Series(['Wu Wang', 21], index = df1.columns)
df1.append(s, ignore_index=True)
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
      <th>Name</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wu Wang</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>



对于 assign 而言，虽然可以利用其添加新的列，但一般通过 df['new_col'] = ... 的形式就可以等价地添加新列。同时，使用 [] 修改的缺点是它会直接在原表上进行改动，而 assign 返回的是一个临时副本：


```python
s = pd.Series([80, 90])
df1.assign(Grade=s)
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
      <th>Name</th>
      <th>Age</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1['Grade'] = s
df1
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
      <th>Name</th>
      <th>Age</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>30</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



## 三、类连接操作

### 1. 比较

compare 是在 1.1.0 后引入的新函数，它能够比较两个表或者序列的不同处并将其汇总展示：


```python
df1 = pd.DataFrame({'Name':['San Zhang', 'Si Li', 'Wu Wang'],
                            'Age':[20, 21 ,21],
                            'Class':['one', 'two', 'three']})
df1
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
      <th>Name</th>
      <th>Age</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>one</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>21</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wu Wang</td>
      <td>21</td>
      <td>three</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame({'Name':['San Zhang', 'Li Si', 'Wu Wang'],
                           'Age':[20, 21 ,21],
                           'Class':['one', 'two', 'Three']})
df2
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
      <th>Name</th>
      <th>Age</th>
      <th>Class</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>20</td>
      <td>one</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Li Si</td>
      <td>21</td>
      <td>two</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wu Wang</td>
      <td>21</td>
      <td>Three</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.compare(df2)#结果中返回了不同值所在的行列，如果相同则会被填充为缺失值 NaN ，其中 other 和 self 分别指代传入的参数表和被调用的表自身。
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
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">Name</th>
      <th colspan="2" halign="left">Class</th>
    </tr>
    <tr>
      <th></th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>Li Si</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>three</td>
      <td>Three</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.compare(df2, keep_shape=True)
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
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="2" halign="left">Name</th>
      <th colspan="2" halign="left">Age</th>
      <th colspan="2" halign="left">Class</th>
    </tr>
    <tr>
      <th></th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
      <th>self</th>
      <th>other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Si Li</td>
      <td>Li Si</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>three</td>
      <td>Three</td>
    </tr>
  </tbody>
</table>
</div>



### 2. 组合

combine 函数能够让两张表按照一定的规则进行组合，在进行规则比较时会自动进行列索引的对齐。对于传入的函数而言，每一次操作中输入的参数是来自两个表的同名 Series ，依次传入的列是两个表列名的并集，


```python
#选出对应索引位置较小的元素：
def choose_min(s1, s2):
        s2 = s2.reindex_like(s1)
        res = s1.where(s1<s2, s2)
        res = res.mask(s1.isna()) # isna表示是否为缺失值，返回布尔序列
        return res
df1 = pd.DataFrame({'A':[1,2], 'B':[3,4], 'C':[5,6]})
df1
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>4</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = pd.DataFrame({'B':[5,6], 'C':[7,8], 'D':[9,10]}, index=[1,2])
df2
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
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>5</td>
      <td>7</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>8</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.combine(df2, choose_min)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



设置 overtwrite 参数为 False 可以保留 被调用表 中未出现在传入的参数表中的列，而不会设置未缺失值：


```python
df1.combine(df2, choose_min, overwrite=False)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>4.0</td>
      <td>6.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



## 四、练习

现有美国4月12日至11月16日的疫情报表（在 /data/us_report 文件夹下），请将 New York 的 Confirmed, Deaths, Recovered, Active 合并为一张表，索引为按如下方法生成的日期字符串序列：

date = pd.date_range('20200412', '20201116').to_series()
date = date.dt.month.astype('string').str.zfill(2) +'-'+ date.dt.day.astype('string').str.zfill(2) +'-'+ '2020
date = date.tolist()
date[:5]


```python

```
