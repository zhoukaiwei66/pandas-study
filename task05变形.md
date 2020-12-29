
# 第五章 变形


```python
import numpy as np
import pandas as pd
```

## 一、长宽表的变形

一个表中把性别存储在某一个列中，那么它就是关于性别的长表；如果把性别作为列名，列中的元素是某一其他的相关特征数值，那么这个表是关于性别的宽表


```python
pd.DataFrame({'Gender':['F','F','M','M'],'Height':[163,160,175,180]})#长表
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
      <th>Height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>F</td>
      <td>163</td>
    </tr>
    <tr>
      <th>1</th>
      <td>F</td>
      <td>160</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M</td>
      <td>175</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M</td>
      <td>180</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame({'Height: F':[163, 160],'Height: M':[175, 180]})#宽表
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
      <th>Height: F</th>
      <th>Height: M</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>163</td>
      <td>175</td>
    </tr>
    <tr>
      <th>1</th>
      <td>160</td>
      <td>180</td>
    </tr>
  </tbody>
</table>
</div>



### 1. pivot

pivot 是一种典型的长表变宽表的函数，首先来看一个例子：下表存储了张三和李四的语文和数学分数，现在想要把语文和数学分数作为列来展示。


```python
df = pd.DataFrame({'Class':[1,1,2,2], 'Name':['San Zhang','San Zhang','Si Li','Si Li'],
                       'Subject':['Chinese','Math','Chinese','Math'],
                       'Grade':[80,75,90,85]})
df
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
      <th>Class</th>
      <th>Name</th>
      <th>Subject</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Chinese</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Math</td>
      <td>75</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Chinese</td>
      <td>90</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Math</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>



对于一个基本的长变宽的操作而言，最重要的有三个要素，分别是变形后的行索引、需要转到列索引的列，以及这些列和行索引对应的数值，它们分别对应了 pivot 方法中的 index, columns, values 参数。新生成表的列索引是 columns 对应列的 unique 值，而新表的行索引是 index 对应列的 unique 值，而 values 对应了想要展示的数值列。


```python
df.pivot(index='Name', columns='Subject', values='Grade')#长表变宽表
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
      <th>Subject</th>
      <th>Chinese</th>
      <th>Math</th>
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
      <td>80</td>
      <td>75</td>
    </tr>
    <tr>
      <th>Si Li</th>
      <td>90</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[1, 'Subject'] = 'Chinese'
try:
       df.pivot(index='Name', columns='Subject', values='Grade')
    except Exception as e:
        Err_Msg = e
Err_Msg
```


      File "<tokenize>", line 4
        except Exception as e:
        ^
    IndentationError: unindent does not match any outer indentation level
    


pandas 从 1.1.0 开始， pivot 相关的三个参数允许被设置为列表，这也意味着会返回多级索引


```python
 df = pd.DataFrame({'Class':[1, 1, 2, 2, 1, 1, 2, 2],
                      'Name':['San Zhang', 'San Zhang', 'Si Li', 'Si Li',
                               'San Zhang', 'San Zhang', 'Si Li', 'Si Li'],
                      'Examination': ['Mid', 'Final', 'Mid', 'Final',
                                     'Mid', 'Final', 'Mid', 'Final'],
                      'Subject':['Chinese', 'Chinese', 'Chinese', 'Chinese',
                                  'Math', 'Math', 'Math', 'Math'],
                      'Grade':[80, 75, 85, 65, 90, 85, 92, 88],
                      'rank':[10, 15, 21, 15, 20, 7, 6, 2]})
df
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
      <th>Class</th>
      <th>Name</th>
      <th>Examination</th>
      <th>Subject</th>
      <th>Grade</th>
      <th>rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Mid</td>
      <td>Chinese</td>
      <td>80</td>
      <td>10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Final</td>
      <td>Chinese</td>
      <td>75</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Mid</td>
      <td>Chinese</td>
      <td>85</td>
      <td>21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Final</td>
      <td>Chinese</td>
      <td>65</td>
      <td>15</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Mid</td>
      <td>Math</td>
      <td>90</td>
      <td>20</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Final</td>
      <td>Math</td>
      <td>85</td>
      <td>7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Mid</td>
      <td>Math</td>
      <td>92</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Final</td>
      <td>Math</td>
      <td>88</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



现在想要把测试类型和科目联合组成的四个类别（期中语文、期末语文、期中数学、期末数学）转到列索引，并且同时统计成绩和排名：


```python
pivot_multi = df.pivot(index = ['Class', 'Name'],
                          columns = ['Subject','Examination'],
                          values = ['Grade','rank'])
pivot_multi
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
      <th colspan="4" halign="left">Grade</th>
      <th colspan="4" halign="left">rank</th>
    </tr>
    <tr>
      <th></th>
      <th>Subject</th>
      <th colspan="2" halign="left">Chinese</th>
      <th colspan="2" halign="left">Math</th>
      <th colspan="2" halign="left">Chinese</th>
      <th colspan="2" halign="left">Math</th>
    </tr>
    <tr>
      <th></th>
      <th>Examination</th>
      <th>Mid</th>
      <th>Final</th>
      <th>Mid</th>
      <th>Final</th>
      <th>Mid</th>
      <th>Final</th>
      <th>Mid</th>
      <th>Final</th>
    </tr>
    <tr>
      <th>Class</th>
      <th>Name</th>
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
      <th>1</th>
      <th>San Zhang</th>
      <td>80</td>
      <td>75</td>
      <td>90</td>
      <td>85</td>
      <td>10</td>
      <td>15</td>
      <td>20</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Si Li</th>
      <td>85</td>
      <td>65</td>
      <td>92</td>
      <td>88</td>
      <td>21</td>
      <td>15</td>
      <td>6</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



### 2. pivot_table

pivot 的使用依赖于唯一性条件，那如果不满足唯一性条件，那么必须通过聚合操作使得相同行列组合对应的多个值变为一个值。例如，张三和李四都参加了两次语文考试和数学考试，按照学院规定，最后的成绩是两次考试分数的平均值，此时就无法通过 pivot 函数来完成。


```python
df = pd.DataFrame({'Name':['San Zhang', 'San Zhang',
                              'San Zhang', 'San Zhang',
                              'Si Li', 'Si Li', 'Si Li', 'Si Li'],
                     'Subject':['Chinese', 'Chinese', 'Math', 'Math',
                                 'Chinese', 'Chinese', 'Math', 'Math'],
                     'Grade':[80, 90, 100, 90, 70, 80, 85, 95]})
df
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
      <th>Subject</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>San Zhang</td>
      <td>Chinese</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>San Zhang</td>
      <td>Chinese</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>San Zhang</td>
      <td>Math</td>
      <td>100</td>
    </tr>
    <tr>
      <th>3</th>
      <td>San Zhang</td>
      <td>Math</td>
      <td>90</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Si Li</td>
      <td>Chinese</td>
      <td>70</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Si Li</td>
      <td>Chinese</td>
      <td>80</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Si Li</td>
      <td>Math</td>
      <td>85</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Si Li</td>
      <td>Math</td>
      <td>95</td>
    </tr>
  </tbody>
</table>
</div>




```python
 df.pivot_table(index = 'Name',
                   columns = 'Subject',
                   values = 'Grade',
                   aggfunc = 'mean')
    
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
      <th>Subject</th>
      <th>Chinese</th>
      <th>Math</th>
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
      <td>85</td>
      <td>95</td>
    </tr>
    <tr>
      <th>Si Li</th>
      <td>75</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



### 3. melt

长宽表只是数据呈现方式的差异，但其包含的信息量是等价的，前面提到了利用 pivot 把长表转为宽表，那么就可以通过相应的逆操作把宽表转为长表， melt 函数就起到了这样的作用。


```python
df = pd.DataFrame({'Class':[1,2],
                      'Name':['San Zhang', 'Si Li'],
                      'Chinese':[80, 90],
                      'Math':[80, 75]})
df
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
      <th>Class</th>
      <th>Name</th>
      <th>Chinese</th>
      <th>Math</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Si Li</td>
      <td>90</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_melted = df.melt(id_vars = ['Class', 'Name'],
                        value_vars = ['Chinese', 'Math'],
                        var_name = 'Subject',
                        value_name = 'Grade')
df_melted
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
      <th>Class</th>
      <th>Name</th>
      <th>Subject</th>
      <th>Grade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Chinese</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Chinese</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>Math</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>Si Li</td>
      <td>Math</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>



通过 pivot 操作把 df_melted 转回 df 的形式：


```python
df_unmelted = df_melted.pivot(index = ['Class', 'Name'],
                                  columns='Subject',
                                  values='Grade')
df_unmelted
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
      <th>Subject</th>
      <th>Chinese</th>
      <th>Math</th>
    </tr>
    <tr>
      <th>Class</th>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <th>San Zhang</th>
      <td>80</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Si Li</th>
      <td>90</td>
      <td>75</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_unmelted = df_unmelted.reset_index().rename_axis(
                                 columns={'Subject':''})
```

### 4. wide_to_long

melt 方法中，在列索引中被压缩的一组值对应的列元素只能代表同一层次的含义，即 values_name 。现在如果列中包含了交叉类别，比如期中期末的类别和语文数学的类别，那么想要把 values_name 对应的 Grade 扩充为两列分别对应语文分数和数学分数，只把期中期末的信息压缩，这种需求下就要使用 wide_to_long 函数来完成。


```python
df = pd.DataFrame({'Class':[1,2],'Name':['San Zhang', 'Si Li'],
                       'Chinese_Mid':[80, 75], 'Math_Mid':[90, 85],
                       'Chinese_Final':[80, 75], 'Math_Final':[90, 85]})
df
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
      <th>Class</th>
      <th>Name</th>
      <th>Chinese_Mid</th>
      <th>Math_Mid</th>
      <th>Chinese_Final</th>
      <th>Math_Final</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>San Zhang</td>
      <td>80</td>
      <td>90</td>
      <td>80</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Si Li</td>
      <td>75</td>
      <td>85</td>
      <td>75</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.wide_to_long(df,
                    stubnames=['Chinese', 'Math'],
                    i = ['Class', 'Name'],
                    j='Examination',
                    sep='_',
                    suffix='.+')
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
      <th>Chinese</th>
      <th>Math</th>
    </tr>
    <tr>
      <th>Class</th>
      <th>Name</th>
      <th>Examination</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">1</th>
      <th rowspan="2" valign="top">San Zhang</th>
      <th>Mid</th>
      <td>80</td>
      <td>90</td>
    </tr>
    <tr>
      <th>Final</th>
      <td>80</td>
      <td>90</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2</th>
      <th rowspan="2" valign="top">Si Li</th>
      <th>Mid</th>
      <td>75</td>
      <td>85</td>
    </tr>
    <tr>
      <th>Final</th>
      <td>75</td>
      <td>85</td>
    </tr>
  </tbody>
</table>
</div>



## 二、索引的变形

### 1. stack与unstack

unstack 函数的作用是把行索引转为列索引，


```python
df = pd.DataFrame(np.ones((4,2)),
                     index = pd.Index([('A', 'cat', 'big'),
                                       ('A', 'dog', 'small'),
                                       ('B', 'cat', 'big'),
                                       ('B', 'dog', 'small')]),
                     columns=['col_1', 'col_2'])
df
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
      <th>col_1</th>
      <th>col_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>cat</th>
      <th>big</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>dog</th>
      <th>small</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>cat</th>
      <th>big</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>dog</th>
      <th>small</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.unstack()
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
      <th></th>
      <th colspan="2" halign="left">col_1</th>
      <th colspan="2" halign="left">col_2</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>big</th>
      <th>small</th>
      <th>big</th>
      <th>small</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>cat</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>dog</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>cat</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>dog</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



unstack 的主要参数是移动的层号，默认转化最内层，移动到列索引的最内层，同时支持同时转化多个层：


```python
df.unstack(2)
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
      <th></th>
      <th colspan="2" halign="left">col_1</th>
      <th colspan="2" halign="left">col_2</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th>big</th>
      <th>small</th>
      <th>big</th>
      <th>small</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">A</th>
      <th>cat</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>dog</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">B</th>
      <th>cat</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>dog</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.unstack([0,2])
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
      <th colspan="4" halign="left">col_1</th>
      <th colspan="4" halign="left">col_2</th>
    </tr>
    <tr>
      <th></th>
      <th colspan="2" halign="left">A</th>
      <th colspan="2" halign="left">B</th>
      <th colspan="2" halign="left">A</th>
      <th colspan="2" halign="left">B</th>
    </tr>
    <tr>
      <th></th>
      <th>big</th>
      <th>small</th>
      <th>big</th>
      <th>small</th>
      <th>big</th>
      <th>small</th>
      <th>big</th>
      <th>small</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>cat</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>dog</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



## 三、其他变形函数

统计 learn_pandas 数据集中学校和转系情况对应的频数：


```python
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv')
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
      <th>School</th>
      <th>Grade</th>
      <th>Name</th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Transfer</th>
      <th>Test_Number</th>
      <th>Test_Date</th>
      <th>Time_Record</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Gaopeng Yang</td>
      <td>Female</td>
      <td>158.9</td>
      <td>46.0</td>
      <td>N</td>
      <td>1</td>
      <td>2019/10/5</td>
      <td>0:04:34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Peking University</td>
      <td>Freshman</td>
      <td>Changqiang You</td>
      <td>Male</td>
      <td>166.5</td>
      <td>70.0</td>
      <td>N</td>
      <td>1</td>
      <td>2019/9/4</td>
      <td>0:04:20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Mei Sun</td>
      <td>Male</td>
      <td>188.9</td>
      <td>89.0</td>
      <td>N</td>
      <td>2</td>
      <td>2019/9/12</td>
      <td>0:05:22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fudan University</td>
      <td>Sophomore</td>
      <td>Xiaojuan Sun</td>
      <td>Female</td>
      <td>NaN</td>
      <td>41.0</td>
      <td>N</td>
      <td>2</td>
      <td>2020/1/3</td>
      <td>0:04:08</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fudan University</td>
      <td>Sophomore</td>
      <td>Gaojuan You</td>
      <td>Male</td>
      <td>174.0</td>
      <td>74.0</td>
      <td>N</td>
      <td>2</td>
      <td>2019/11/6</td>
      <td>0:05:22</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.crosstab(index = df.School, columns = df.Transfer)
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
      <th>Transfer</th>
      <th>N</th>
      <th>Y</th>
    </tr>
    <tr>
      <th>School</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Fudan University</th>
      <td>38</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Peking University</th>
      <td>28</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Shanghai Jiao Tong University</th>
      <td>53</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Tsinghua University</th>
      <td>62</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.crosstab(index = df.School, columns = df.Transfer,
               values = [0]*df.shape[0], aggfunc = 'count')#与上面同样的结果
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
      <th>Transfer</th>
      <th>N</th>
      <th>Y</th>
    </tr>
    <tr>
      <th>School</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Fudan University</th>
      <td>38.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Peking University</th>
      <td>28.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Shanghai Jiao Tong University</th>
      <td>53.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Tsinghua University</th>
      <td>62.0</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



利用 pivot_table 进行等价操作，由于这里统计的是组合的频数，因此 values 参数无论传入哪一个列都不会影响最后的结果：


```python
df.pivot_table(index = 'School',
                   columns = 'Transfer',
                   values = 'Name',
                   aggfunc = 'count')
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
      <th>Transfer</th>
      <th>N</th>
      <th>Y</th>
    </tr>
    <tr>
      <th>School</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Fudan University</th>
      <td>38.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Peking University</th>
      <td>28.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>Shanghai Jiao Tong University</th>
      <td>53.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Tsinghua University</th>
      <td>62.0</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



### 2. explode

explode 参数能够对某一列的元素进行纵向的展开，被展开的单元格必须存储 list, tuple, Series, np.ndarray 中的一种类型。


```python
df_ex = pd.DataFrame({'A': [[1, 2],
                             'my_str',
                             {1, 2},
                             pd.Series([3, 4])],
                          'B': 1})
df_ex.explode('A')
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>my_str</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>{1, 2}</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### 3. get_dummies

get_dummies 是用于特征构建的重要函数之一，其作用是把类别特征转为指示变量。例如，对年级一列转为指示变量，属于某一个年级的对应列标记为1，否则为0：


```python
pd.get_dummies(df.Grade).head()
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
      <th>Freshman</th>
      <th>Junior</th>
      <th>Senior</th>
      <th>Sophomore</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



## 四、练习

### Ex1：美国非法药物数据集

现有一份关于美国非法药物的数据集，其中 SubstanceName, DrugReports 分别指药物名称和报告数量：


```python
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\drugs.csv').sort_values([
        'State','COUNTY','SubstanceName'],ignore_index=True)
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
      <th>YYYY</th>
      <th>State</th>
      <th>COUNTY</th>
      <th>SubstanceName</th>
      <th>DrugReports</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2011</td>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Buprenorphine</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2012</td>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Buprenorphine</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2013</td>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Buprenorphine</td>
      <td>4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014</td>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Buprenorphine</td>
      <td>27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Buprenorphine</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



将数据转为如下的形式：

![Ex5_1.png](attachment:Ex5_1.png)


```python
A = df.pivot(index=['State','COUNTY','SubstanceName'
                  ], columns='YYYY', values='DrugReports'
                  ).reset_index().rename_axis(columns={'YYYY':''})
A.head()
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
      <th>State</th>
      <th>COUNTY</th>
      <th>SubstanceName</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
      <th>2017</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Buprenorphine</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>5.0</td>
      <td>4.0</td>
      <td>27.0</td>
      <td>5.0</td>
      <td>7.0</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Codeine</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Fentanyl</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Heroin</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>NaN</td>
      <td>1.0</td>
      <td>NaN</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>KY</td>
      <td>ADAIR</td>
      <td>Hydrocodone</td>
      <td>6.0</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>7.0</td>
      <td>11.0</td>
      <td>3.0</td>
    </tr>
  </tbody>
</table>
</div>



将第1问中的结果恢复为原表。


```python
A_melted = A.melt(id_vars = ['State','COUNTY','SubstanceName'],
                         value_vars = A.columns[-8:],
                         var_name = 'YYYY',
                         value_name = 'DrugReports').dropna(
                         subset=['DrugReports'])
A_melted = A_melted[df.columns].sort_values([
                  'State','COUNTY','SubstanceName'],ignore_index=True
                  ).astype({'YYYY':'int64', 'DrugReports':'int64'})
res_melted.equals(df)
```




    True



按 State 分别统计每年的报告数量总和，其中 State, YYYY 分别为列索引和行索引，要求分别使用 pivot_table 函数与 groupby+unstack 两种不同的策略实现，并体会它们之间的联系。




```python
B = df.pivot_table(index='YYYY', columns='State',
                         values='DrugReports', aggfunc='sum')
B.head()
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
      <th>State</th>
      <th>KY</th>
      <th>OH</th>
      <th>PA</th>
      <th>VA</th>
      <th>WV</th>
    </tr>
    <tr>
      <th>YYYY</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010</th>
      <td>10453</td>
      <td>19707</td>
      <td>19814</td>
      <td>8685</td>
      <td>2890</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>10289</td>
      <td>20330</td>
      <td>19987</td>
      <td>6749</td>
      <td>3271</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>10722</td>
      <td>23145</td>
      <td>19959</td>
      <td>7831</td>
      <td>3376</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>11148</td>
      <td>26846</td>
      <td>20409</td>
      <td>11675</td>
      <td>4046</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>11081</td>
      <td>30860</td>
      <td>24904</td>
      <td>9037</td>
      <td>3280</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
