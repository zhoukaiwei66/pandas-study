
# 一、文件的读取和写入

## 1. 文件读取


```python
import numpy as np
import pandas as pd
df_csv = pd.read_csv(r"C:\Users\zhoukaiwei\Desktop\CSV.csv")
df_csv
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
      <th>Unnamed: 0</th>
      <th>clum1</th>
      <th>clum2</th>
      <th>clum3</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>a</td>
      <td>A</td>
      <td>1</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
      <td>B</td>
      <td>2</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>c</td>
      <td>C</td>
      <td>3</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>d</td>
      <td>D</td>
      <td>4</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>e</td>
      <td>E</td>
      <td>5</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>f</td>
      <td>F</td>
      <td>6</td>
      <td>2020.1.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_excel = pd.read_excel(r"C:\Users\zhoukaiwei\Desktop\my_excel.xlsx")
df_excel
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
      <th>Unnamed: 0</th>
      <th>clum1</th>
      <th>clum2</th>
      <th>clum3</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>a</td>
      <td>A</td>
      <td>1</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
      <td>B</td>
      <td>2</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>c</td>
      <td>C</td>
      <td>3</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>d</td>
      <td>D</td>
      <td>4</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>e</td>
      <td>E</td>
      <td>5</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>f</td>
      <td>F</td>
      <td>6</td>
      <td>2020.1.1</td>
    </tr>
  </tbody>
</table>
</div>



这里有一些常用的公共参数， header=None 表示第一行不作为列名， index_col 表示把某一列或
几列作为索引，索引的内容将会在第三章进行详述， usecols 表示读取列的集合，默认读取所有的
列， parse_dates 表示需要转化为时间的列，关于时间序列的有关内容将在第十章讲解， nrows 
表示读取的数据行数。上面这些参数在上述的三个函数里都可以使用。


```python
df_excel = pd.read_excel(r"C:\Users\zhoukaiwei\Desktop\my_excel.xlsx",header = None)
df_excel
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>clum1</td>
      <td>clum2</td>
      <td>clum3</td>
      <td>time</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>a</td>
      <td>A</td>
      <td>1</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>b</td>
      <td>B</td>
      <td>2</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.0</td>
      <td>c</td>
      <td>C</td>
      <td>3</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.0</td>
      <td>d</td>
      <td>D</td>
      <td>4</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>4.0</td>
      <td>e</td>
      <td>E</td>
      <td>5</td>
      <td>2020.1.1</td>
    </tr>
    <tr>
      <th>6</th>
      <td>5.0</td>
      <td>f</td>
      <td>F</td>
      <td>6</td>
      <td>2020.1.1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_excel = pd.read_excel(r"C:\Users\zhoukaiwei\Desktop\my_excel.xlsx",usecols=['clum3'])
df_excel
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
      <th>clum3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_excel = pd.read_excel(r"C:\Users\zhoukaiwei\Desktop\my_excel.xlsx",parse_dates=['time'])
df_excel
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
      <th>Unnamed: 0</th>
      <th>clum1</th>
      <th>clum2</th>
      <th>clum3</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>a</td>
      <td>A</td>
      <td>1</td>
      <td>2020-01-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>b</td>
      <td>B</td>
      <td>2</td>
      <td>2020-01-01</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>c</td>
      <td>C</td>
      <td>3</td>
      <td>2020-01-01</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>d</td>
      <td>D</td>
      <td>4</td>
      <td>2020-01-01</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>e</td>
      <td>E</td>
      <td>5</td>
      <td>2020-01-01</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>f</td>
      <td>F</td>
      <td>6</td>
      <td>2020-01-01</td>
    </tr>
  </tbody>
</table>
</div>



## 二、基本数据结构

pandas 中具有两种基本的数据存储结构，存储一维 values 的 Series 和存储二维 values 
的 DataFrame .


Series 一般由四个部分组成，分别是序列的值 data 、索引 index 、存储类型 dtype 、
序列的名字 name 。其中，索引也可以指定它的名字，默认为空。


```python
A = pd.Series(data = [100,'A',{'index':5}],
             index = pd.Index(['id1','id2','id3'],name = 'index'),
             dtype = 'object',name = 'my_name')
A
```




    index
    id1             100
    id2               A
    id3    {'index': 5}
    Name: my_name, dtype: object



获取属性


```python
A.values
```




    array([100, 'A', {'index': 5}], dtype=object)




```python
A.index
```




    Index(['id1', 'id2', 'id3'], dtype='object', name='index')




```python
A.dtype
```




    dtype('O')




```python
A.shape
```




    (3,)




```python
A['id2']
```




    'A'



DataFrame 在 Series 的基础上增加了列索引，一个数据框可以由二维的 data 与行列索引来构造：


```python
import pandas as pd
data = [[1,'a',1.2],[2,'b',2.2],[3,'c',3.2]]
df = pd.DataFrame(data = data,index = ['a_%d'%i for i in range(3)],columns = ['b_%d'%i for i in range(3)])
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
      <th>b_0</th>
      <th>b_1</th>
      <th>b_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a_0</th>
      <td>1</td>
      <td>a</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>a_1</th>
      <td>2</td>
      <td>b</td>
      <td>2.2</td>
    </tr>
    <tr>
      <th>a_2</th>
      <td>3</td>
      <td>c</td>
      <td>3.2</td>
    </tr>
  </tbody>
</table>
</div>



用从列索引名到数据的映射来构造数据框，同时再加上行索引：


```python
data = pd.DataFrame(data = {'col_0':[1,2,3],'col_1':list('abc'),'col_2':[1.2,2.2,3.2]},
                   index = ['row_%d'%i for i in range(3)])
data
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
      <th>col_0</th>
      <th>col_1</th>
      <th>col_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>row_0</th>
      <td>1</td>
      <td>a</td>
      <td>1.2</td>
    </tr>
    <tr>
      <th>row_1</th>
      <td>2</td>
      <td>b</td>
      <td>2.2</td>
    </tr>
    <tr>
      <th>row_2</th>
      <td>3</td>
      <td>c</td>
      <td>3.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
data['col_1']
```




    row_0    a
    row_1    b
    row_2    c
    Name: col_1, dtype: object




```python
data.values
```




    array([[1, 'a', 1.2],
           [2, 'b', 2.2],
           [3, 'c', 3.2]], dtype=object)




```python
data.shape#大小
```




    (3, 3)




```python
data.T#转置
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
      <th>row_0</th>
      <th>row_1</th>
      <th>row_2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>col_0</th>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>col_1</th>
      <td>a</td>
      <td>b</td>
      <td>c</td>
    </tr>
    <tr>
      <th>col_2</th>
      <td>1.2</td>
      <td>2.2</td>
      <td>3.2</td>
    </tr>
  </tbody>
</table>
</div>



## 三、常用基本函数


```python
import pandas as pd
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv')
df.columns
```




    Index(['School', 'Grade', 'Name', 'Gender', 'Height', 'Weight', 'Transfer',
           'Test_Number', 'Test_Date', 'Time_Record'],
          dtype='object')



head, tail 函数分别表示返回表或者序列的前 n 行和后 n 行，其中 n 默认为5：


```python
df = df[df.columns[:7]]
df.head(3)
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
    </tr>
  </tbody>
</table>
</div>




```python
df.tail(5)
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
      <th>School</th>
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
      <td>Shanghai Jiao Tong University</td>
      <td>Freshman</td>
      <td>Gaopeng Yang</td>
      <td>Female</td>
      <td>158.9</td>
      <td>46.0</td>
      <td>N</td>
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
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>195</th>
      <td>Fudan University</td>
      <td>Junior</td>
      <td>Xiaojuan Sun</td>
      <td>Female</td>
      <td>153.9</td>
      <td>46.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Tsinghua University</td>
      <td>Senior</td>
      <td>Li Zhao</td>
      <td>Female</td>
      <td>160.9</td>
      <td>50.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>197</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Chengqiang Chu</td>
      <td>Female</td>
      <td>153.9</td>
      <td>45.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Senior</td>
      <td>Chengmei Shen</td>
      <td>Male</td>
      <td>175.3</td>
      <td>71.0</td>
      <td>N</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Tsinghua University</td>
      <td>Sophomore</td>
      <td>Chunpeng Lv</td>
      <td>Male</td>
      <td>155.7</td>
      <td>51.0</td>
      <td>N</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 7 columns</p>
</div>




```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 200 entries, 0 to 199
    Data columns (total 7 columns):
     #   Column    Non-Null Count  Dtype  
    ---  ------    --------------  -----  
     0   School    200 non-null    object 
     1   Grade     200 non-null    object 
     2   Name      200 non-null    object 
     3   Gender    200 non-null    object 
     4   Height    183 non-null    float64
     5   Weight    189 non-null    float64
     6   Transfer  188 non-null    object 
    dtypes: float64(2), object(5)
    memory usage: 11.1+ KB
    


```python
df.describe()
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
      <th>Height</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>183.000000</td>
      <td>189.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>163.218033</td>
      <td>55.015873</td>
    </tr>
    <tr>
      <th>std</th>
      <td>8.608879</td>
      <td>12.824294</td>
    </tr>
    <tr>
      <th>min</th>
      <td>145.400000</td>
      <td>34.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>157.150000</td>
      <td>46.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>161.900000</td>
      <td>51.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>167.500000</td>
      <td>65.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>193.900000</td>
      <td>89.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['School'].unique()#得到唯一值组成的列表

```




    array(['Shanghai Jiao Tong University', 'Peking University',
           'Fudan University', 'Tsinghua University'], dtype=object)




```python
df['School'].nunique()#得到唯一值的个数
```




    4




```python
df['School'].value_counts()#value_counts 可以得到唯一值和其对应出现的频数：
```




    Tsinghua University              69
    Shanghai Jiao Tong University    57
    Fudan University                 40
    Peking University                34
    Name: School, dtype: int64



使用 drop_duplicates得到多个列组合的唯一值，其中的关键参数是 keep ，默认值 first 表示每
个组合保留第一次出现的所在行， last 表示保留最后一次出现的所在行， False 表示把所有重
复组合所在的行剔除。


```python
df_A = df[['School','Transfer','Name']]
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
      <th>School</th>
      <th>Transfer</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Shanghai Jiao Tong University</td>
      <td>N</td>
      <td>Gaopeng Yang</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Peking University</td>
      <td>N</td>
      <td>Changqiang You</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shanghai Jiao Tong University</td>
      <td>N</td>
      <td>Mei Sun</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fudan University</td>
      <td>N</td>
      <td>Xiaojuan Sun</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fudan University</td>
      <td>N</td>
      <td>Gaojuan You</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>195</th>
      <td>Fudan University</td>
      <td>N</td>
      <td>Xiaojuan Sun</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Tsinghua University</td>
      <td>N</td>
      <td>Li Zhao</td>
    </tr>
    <tr>
      <th>197</th>
      <td>Shanghai Jiao Tong University</td>
      <td>N</td>
      <td>Chengqiang Chu</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Shanghai Jiao Tong University</td>
      <td>N</td>
      <td>Chengmei Shen</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Tsinghua University</td>
      <td>N</td>
      <td>Chunpeng Lv</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 3 columns</p>
</div>




```python
df_A.drop_duplicates(['School','Transfer'])
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
      <th>Transfer</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Shanghai Jiao Tong University</td>
      <td>N</td>
      <td>Gaopeng Yang</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Peking University</td>
      <td>N</td>
      <td>Changqiang You</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fudan University</td>
      <td>N</td>
      <td>Xiaojuan Sun</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tsinghua University</td>
      <td>N</td>
      <td>Xiaoli Qian</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Shanghai Jiao Tong University</td>
      <td>NaN</td>
      <td>Peng You</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Peking University</td>
      <td>Y</td>
      <td>Xiaojuan Qin</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Tsinghua University</td>
      <td>Y</td>
      <td>Gaoli Feng</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Tsinghua University</td>
      <td>NaN</td>
      <td>Chunquan Xu</td>
    </tr>
    <tr>
      <th>84</th>
      <td>Fudan University</td>
      <td>NaN</td>
      <td>Yanjuan Lv</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Peking University</td>
      <td>NaN</td>
      <td>Chengli Zhao</td>
    </tr>
    <tr>
      <th>131</th>
      <td>Fudan University</td>
      <td>Y</td>
      <td>Chengpeng Qian</td>
    </tr>
  </tbody>
</table>
</div>



#### 4. 替换函数

一般而言，替换操作是针对某一个列进行的，因此下面的例子都以 Series 举例。 pandas 中的
替换函数可以归纳为三类：映射替换、逻辑替换、数值替换。其中映射替换包含 replace 方法、
str.replace 方法以及cat.codes 方法，此处介绍 replace 的用法。
在 replace 中，可以通过字典构造，或者传入两个列表来进行替换：


```python
#df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv')
#df = df[df.columns[:7]]
df['Gender'].replace({'Female':0, 'Male':1}).head()
```




    0    0
    1    1
    2    1
    3    0
    4    1
    Name: Gender, dtype: int64



#### 5. 排序函数

排序共有两种方式，其一为值排序，其二为索引排序，对应的函数是 sort_values 和 sort_index 。
参数 ascending=True 为升序：


```python
df_A = df[['Grade', 'Name', 'Height',
   ....:               'Weight']].set_index(['Grade','Name'])
df_A.sort_values('Height').head()#升序排列
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
      <th>Height</th>
      <th>Weight</th>
    </tr>
    <tr>
      <th>Grade</th>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Junior</th>
      <th>Xiaoli Chu</th>
      <td>145.4</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>Senior</th>
      <th>Gaomei Lv</th>
      <td>147.3</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>Sophomore</th>
      <th>Peng Han</th>
      <td>147.8</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>Senior</th>
      <th>Changli Lv</th>
      <td>148.7</td>
      <td>41.0</td>
    </tr>
    <tr>
      <th>Sophomore</th>
      <th>Changjuan You</th>
      <td>150.5</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A.sort_values('Height', ascending=False).head()#降序排列

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
      <th>Height</th>
      <th>Weight</th>
    </tr>
    <tr>
      <th>Grade</th>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">Senior</th>
      <th>Xiaoqiang Qin</th>
      <td>193.9</td>
      <td>79.0</td>
    </tr>
    <tr>
      <th>Mei Sun</th>
      <td>188.9</td>
      <td>89.0</td>
    </tr>
    <tr>
      <th>Gaoli Zhao</th>
      <td>186.5</td>
      <td>83.0</td>
    </tr>
    <tr>
      <th>Freshman</th>
      <th>Qiang Han</th>
      <td>185.3</td>
      <td>87.0</td>
    </tr>
    <tr>
      <th>Senior</th>
      <th>Qiang Zheng</th>
      <td>183.9</td>
      <td>87.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A.sort_values(['Weight','Height'],ascending=[True,False]).head(10)
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
      <th>Height</th>
      <th>Weight</th>
    </tr>
    <tr>
      <th>Grade</th>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sophomore</th>
      <th>Peng Han</th>
      <td>147.8</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>Senior</th>
      <th>Gaomei Lv</th>
      <td>147.3</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>Junior</th>
      <th>Xiaoli Chu</th>
      <td>145.4</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>Sophomore</th>
      <th>Qiang Zhou</th>
      <td>150.5</td>
      <td>36.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">Freshman</th>
      <th>Yanqiang Xu</th>
      <td>152.4</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>Qiang Han</th>
      <td>151.8</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>Senior</th>
      <th>Chengpeng Zheng</th>
      <td>151.7</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>Sophomore</th>
      <th>Mei Xu</th>
      <td>154.2</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>Freshman</th>
      <th>Xiaoquan Sun</th>
      <td>154.6</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>Sophomore</th>
      <th>Qiang Sun</th>
      <td>154.3</td>
      <td>40.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A.sort_index(level = ['Grade','Name'],ascending=[True,False]).head(10)
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
      <th>Height</th>
      <th>Weight</th>
    </tr>
    <tr>
      <th>Grade</th>
      <th>Name</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">Freshman</th>
      <th>Yanquan Wang</th>
      <td>163.5</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>Yanqiang Xu</th>
      <td>152.4</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>Yanqiang Feng</th>
      <td>162.3</td>
      <td>51.0</td>
    </tr>
    <tr>
      <th>Yanpeng Lv</th>
      <td>NaN</td>
      <td>65.0</td>
    </tr>
    <tr>
      <th>Yanli Zhang</th>
      <td>165.1</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>Yanjuan Zhao</th>
      <td>NaN</td>
      <td>53.0</td>
    </tr>
    <tr>
      <th>Yanjuan Han</th>
      <td>163.7</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>Xiaoquan Sun</th>
      <td>154.6</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>Xiaopeng Zhou</th>
      <td>174.1</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>Xiaopeng Zhao</th>
      <td>161.0</td>
      <td>53.0</td>
    </tr>
  </tbody>
</table>
</div>



#### 6. apply方法

apply 方法常用于 DataFrame 的行迭代或者列迭代，它的 axis 含义与第2小节中的统计聚合函
数一致， apply 的参数往往是一个以序列为输入的函数。例如对于 .mean() ，使用 apply 可
以如下地写出：


```python
#df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv')
df_A = df[['Height','Weight']]
df_A
def A_mean(x):
    res = x.mean()
    return res
df_A.apply(A_mean)
```




    Height    163.218033
    Weight     55.015873
    dtype: float64




```python
df_A.apply(lambda x: x.mean())#使用lambda表达式
```




    Height    163.218033
    Weight     55.015873
    dtype: float64



### 四、窗口对象


```python
pandas 中有3类窗口，分别是滑动窗口 rolling 、扩张窗口 expanding 以及指数加权窗口 ewm 。
```

#### 1. 滑窗对象


```python
要使用滑窗函数，就必须先要对一个序列使用 .rolling 得到滑窗对象，
其最重要的参数为窗口大小 window 。例如：
```


```python
s = pd.Series([1,2,3,4,5])
A = s.rolling(window = 3)
A
```




    Rolling [window=3,center=False,axis=0]




```python
在得到了滑窗对象后，能够使用相应的聚合函数进行计算，需要注意的是窗口包含当前行所在的元素，例如在第四个位置进行均值运算时，应当计算(2+3+4)/3，
而不是(1+2+3)/3：
```


```python
A.mean()
```




    0    NaN
    1    NaN
    2    2.0
    3    3.0
    4    4.0
    dtype: float64




```python
A.sum()
```




    0     NaN
    1     NaN
    2     6.0
    3     9.0
    4    12.0
    dtype: float64




```python
#计算滑动窗口的相关系数和协方差
s = pd.Series([1,2,6,16,30])
A.cov(s)
```




    0     NaN
    1     NaN
    2     2.5
    3     7.0
    4    12.0
    dtype: float64




```python
A.corr(s)
```




    0         NaN
    1         NaN
    2    0.944911
    3    0.970725
    4    0.995402
    dtype: float64



shift, diff, pct_change 是一组类滑窗函数，它们的公共参数为 periods=n ，默认为1
，分别表示取向前第 n 个元素的值、与向前第 n 个元素做差（与 Numpy 中不同，
后者表示 n 阶差分）、与向前第 n 个元素相比计算增长率。这里的 n 可以为负，表示反方
向的类似操作。


```python
s = pd.Series([1,3,6,10,15])
s.shift(1)
```




    0     NaN
    1     1.0
    2     3.0
    3     6.0
    4    10.0
    dtype: float64




```python
s.diff(2)
```




    0    NaN
    1    NaN
    2    5.0
    3    7.0
    4    9.0
    dtype: float64




```python
s.pct_change()
```




    0         NaN
    1    2.000000
    2    1.000000
    3    0.666667
    4    0.500000
    dtype: float64




```python
s.shift(-1)
```




    0     3.0
    1     6.0
    2    10.0
    3    15.0
    4     NaN
    dtype: float64



#### 2. 扩张窗口


```python
s = pd.Series([1, 3, 6, 10])
s.expanding().mean()
```




    0    1.000000
    1    2.000000
    2    3.333333
    3    5.000000
    dtype: float64



### 五、练习

#### Ex1：口袋妖怪数据集

现有一份口袋妖怪的数据集，下面进行一些背景说明：
#代表全国图鉴编号，不同行存在相同数字则表示为该妖怪的不同状态
妖怪具有单属性和双属性两种，对于单属性的妖怪， Type 2 为缺失值
Total, HP, Attack, Defense, Sp. Atk, Sp. Def, Speed 分别代表种族值、体力、物攻、防御、
特攻、特防、速度，其中种族值为后6项之和


```python
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\pokemon.csv')
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>VenusaurMega Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>625</td>
      <td>80</td>
      <td>100</td>
      <td>123</td>
      <td>122</td>
      <td>120</td>
      <td>80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
    </tr>
  </tbody>
</table>
</div>



1.对 HP, Attack, Defense, Sp. Atk, Sp. Def, Speed 进行加总，验证是否为 Total 值。


```python
A = (df[['HP','Attack','Defense','Sp. Atk','Sp. Def','Speed']]).sum(1)
A
```




    0      318
    1      405
    2      525
    3      625
    4      309
          ... 
    795    600
    796    700
    797    600
    798    680
    799    600
    Length: 800, dtype: int64




```python
x= (A != df['Total']).mean()
x
```




    0.0



对于 # 重复的妖怪只保留第一条记录，解决以下问题：

求第一属性的种类数量和前三多数量对应的种类


```python
df_A = df.drop_duplicates('#',keep='first')
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Bulbasaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>318</td>
      <td>45</td>
      <td>49</td>
      <td>49</td>
      <td>65</td>
      <td>65</td>
      <td>45</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Ivysaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>405</td>
      <td>60</td>
      <td>62</td>
      <td>63</td>
      <td>80</td>
      <td>80</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Venusaur</td>
      <td>Grass</td>
      <td>Poison</td>
      <td>525</td>
      <td>80</td>
      <td>82</td>
      <td>83</td>
      <td>100</td>
      <td>100</td>
      <td>80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Charmander</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>309</td>
      <td>39</td>
      <td>52</td>
      <td>43</td>
      <td>60</td>
      <td>50</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Charmeleon</td>
      <td>Fire</td>
      <td>NaN</td>
      <td>405</td>
      <td>58</td>
      <td>64</td>
      <td>58</td>
      <td>80</td>
      <td>65</td>
      <td>80</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_A['Type 1'].nunique()
```




    18




```python
df_A['Type 1'].value_counts().head(3)
```




    Water     105
    Normal     93
    Grass      66
    Name: Type 1, dtype: int64



求第一属性和第二属性的组合种类


```python
df_B = df_A.drop_duplicates(['Type 1','Type 2'])
df_B.shape[0]
```




    143



求尚未出现过的属性组合


```python
import numpy as np
L_full = [i+' '+j for i in df['Type 1'].unique() for j in (
           df['Type 1'].unique().tolist() + [''])]
L_part = [i+' '+j for i, j in zip(df['Type 1'], df['Type 2'
          ].replace(np.nan, ''))]
res = set(L_full).difference(set(L_part))
len(res)
```




    188



按照下述要求，构造 Series ：

取出物攻，超过120的替换为 high ，不足50的替换为 low ，否则设为 mid111


```python
res = df['Attack'].mask(df['Attack'] > 120, 'high').mask(df['Attack']<50, 'low'
                                                        ).mask((50<=df['Attack'])&(df['Attack']<=120), 'mid')
res
```




    0       low
    1       mid
    2       mid
    3       mid
    4       mid
           ... 
    795     mid
    796    high
    797     mid
    798    high
    799     mid
    Name: Attack, Length: 800, dtype: object



取出第一属性，分别用 replace 和 apply 替换所有字母为大写


```python
df['Type 1'].replace({i:str.upper(i) for i in df['Type 1']})
```




    0        GRASS
    1        GRASS
    2        GRASS
    3        GRASS
    4         FIRE
            ...   
    795       ROCK
    796       ROCK
    797    PSYCHIC
    798    PSYCHIC
    799       FIRE
    Name: Type 1, Length: 800, dtype: object




```python
df['Type 1'].apply(lambda x:str.upper(x))
```




    0        GRASS
    1        GRASS
    2        GRASS
    3        GRASS
    4         FIRE
            ...   
    795       ROCK
    796       ROCK
    797    PSYCHIC
    798    PSYCHIC
    799       FIRE
    Name: Type 1, Length: 800, dtype: object



求每个妖怪六项能力的离差，即所有能力中偏离中位数最大的值，添加到 df 并从大到小排序




```python
df['Deviation'] = df[['HP', 'Attack', 'Defense', 'Sp. Atk',
                     'Sp. Def', 'Speed']].apply(lambda x:np.max(
                       (x-x.median()).abs()), 1)
    
df.sort_values('Deviation', ascending=False).head()
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
      <th>#</th>
      <th>Name</th>
      <th>Type 1</th>
      <th>Type 2</th>
      <th>Total</th>
      <th>HP</th>
      <th>Attack</th>
      <th>Defense</th>
      <th>Sp. Atk</th>
      <th>Sp. Def</th>
      <th>Speed</th>
      <th>Deviation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>230</th>
      <td>213</td>
      <td>Shuckle</td>
      <td>Bug</td>
      <td>Rock</td>
      <td>505</td>
      <td>20</td>
      <td>10</td>
      <td>230</td>
      <td>10</td>
      <td>230</td>
      <td>5</td>
      <td>215.0</td>
    </tr>
    <tr>
      <th>121</th>
      <td>113</td>
      <td>Chansey</td>
      <td>Normal</td>
      <td>NaN</td>
      <td>450</td>
      <td>250</td>
      <td>5</td>
      <td>5</td>
      <td>35</td>
      <td>105</td>
      <td>50</td>
      <td>207.5</td>
    </tr>
    <tr>
      <th>261</th>
      <td>242</td>
      <td>Blissey</td>
      <td>Normal</td>
      <td>NaN</td>
      <td>540</td>
      <td>255</td>
      <td>10</td>
      <td>10</td>
      <td>75</td>
      <td>135</td>
      <td>55</td>
      <td>190.0</td>
    </tr>
    <tr>
      <th>333</th>
      <td>306</td>
      <td>AggronMega Aggron</td>
      <td>Steel</td>
      <td>NaN</td>
      <td>630</td>
      <td>70</td>
      <td>140</td>
      <td>230</td>
      <td>60</td>
      <td>80</td>
      <td>50</td>
      <td>155.0</td>
    </tr>
    <tr>
      <th>224</th>
      <td>208</td>
      <td>SteelixMega Steelix</td>
      <td>Steel</td>
      <td>Ground</td>
      <td>610</td>
      <td>75</td>
      <td>125</td>
      <td>230</td>
      <td>55</td>
      <td>95</td>
      <td>30</td>
      <td>145.0</td>
    </tr>
  </tbody>
</table>
</div>



### Ex2：指数加权窗口

#### 作为扩张窗口的 ewm 窗口

在扩张窗口中，用户可以使用各类函数进行历史的累计指标统计，但这些内置的统计函数往往把
窗口中的所有元素赋予了同样的权重。事实上，可以给出不同的权重来赋给窗口中的元素，
指数加权窗口就是这样一种特殊的扩张窗口。
其中，最重要的参数是 alpha ，它决定了默认情况下的窗口权重为 wi=(1−α)i,i∈{0,1,...,t} ，
其中 i=t 表示当前元素， i=0 表示序列的第一个元素。
从权重公式可以看出，离开当前值越远则权重越小，若记原序列为 x ，更新后的当前元素为 yt ，此时通过加权公式归一化后可知：

\begin{split}y_t &=\frac{\sum_{i=0}^{t} w_i x_{t-i}}{\sum_{i=0}^{t} w_i} \\
&=\frac{x_t + (1 - \alpha)x_{t-1} + (1 - \alpha)^2 x_{t-2} + ...
+ (1 - \alpha)^{t} x_{0}}{1 + (1 - \alpha) + (1 - \alpha)^2 + ...
+ (1 - \alpha)^{t}}\\\end{split}


```python
np.random.seed(0)
s = pd.Series(np.random.randint(-1,2,30).cumsum())
s.head()
```




    0   -1
    1   -1
    2   -2
    3   -2
    4   -2
    dtype: int32




```python
s.ewm(alpha=0.2).mean().head()
```




    0   -1.000000
    1   -1.000000
    2   -1.409836
    3   -1.609756
    4   -1.725845
    dtype: float64



请用 expanding 窗口实现。

#### 作为滑动窗口的 ewm 窗口

从第1问中可以看到， ewm 作为一种扩张窗口的特例，只能从序列的第一个元素开始加权。
现在希望给定一个限制窗口 n ，只对包含自身的最近的 n 个元素作为窗口进行滑动加权平滑。
请根据滑窗函数，给出新的 wi 与 yt 的更新公式，并通过 rolling窗口实现这一功能。


```python

```
