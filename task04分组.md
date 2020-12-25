
# 第四章 分组

## 一、分组模式及其对象

### 1. 分组的一般模式

df.groupby(分组依据)[数据来源].使用操作 #分组的常用形式

学生体测的数据集上，如果想要按照性别统计身高中位数


```python
import numpy as np
import pandas as pd
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv').head()
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
df.groupby('Gender')['Height'].median()
```




    Gender
    Female    158.9
    Male      174.0
    Name: Height, dtype: float64



### 2. 分组依据的本质

根据学校和性别进行分组，统计身高的均值


```python
df.groupby(['School','Gender'])['Height'].mean()
```




    School                         Gender
    Fudan University               Female      NaN
                                   Male      174.0
    Peking University              Male      166.5
    Shanghai Jiao Tong University  Female    158.9
                                   Male      188.9
    Name: Height, dtype: float64



根据学生体重是否超过总体均值来分组，同样还是计算身高的均值。


```python
con = df.Weight > df.Weight.mean()
df.groupby(con)['Height'].mean()
```




    Weight
    False    158.900000
    True     176.466667
    Name: Height, dtype: float64




```python
item = np.random.choice(list('abc'), df.shape[0])
df.groupby(item)['Height'].mean()#根据传入的字母序列分组
```




    a    166.5
    b    173.9
    c    174.0
    Name: Height, dtype: float64



如果传入多个序列进入 groupby ，那么最后分组的依据就是这两个序列对应行的唯一组合：


```python
df.groupby([con,item])['Height'].mean()
```




    Weight   
    False   b    158.9
    True    a    166.5
            b    188.9
            c    174.0
    Name: Height, dtype: float64



分组的依据来自于数据来源组合的unique值，通过 drop_duplicates 就能知道具体的组类别：


```python
df[['School','Gender']].drop_duplicates()
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
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Peking University</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shanghai Jiao Tong University</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fudan University</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Fudan University</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby([df['School'], df['Gender']])['Height'].mean()
```




    School                         Gender
    Fudan University               Female      NaN
                                   Male      174.0
    Peking University              Male      166.5
    Shanghai Jiao Tong University  Female    158.9
                                   Male      188.9
    Name: Height, dtype: float64



### 3. Groupby对象


```python
A = df.groupby(['School', 'Grade'])
A
```




    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x000001DBF09A1BA8>




```python
A.ngroups#获取分组数
```




    4




```python
#通过 groups 属性，可以返回从 组名 映射到 组索引列表 的字典：
B=A.groups
B.keys()
```




    dict_keys([('Fudan University', 'Sophomore'), ('Peking University', 'Freshman'), ('Shanghai Jiao Tong University', 'Freshman'), ('Shanghai Jiao Tong University', 'Senior')])



当 size 作为 DataFrame 的属性时，返回的是表长乘以表宽的大小，但在 groupby 对象上表示统计每个组的元素个数：


```python
A.size()
```




    School                         Grade    
    Fudan University               Sophomore    2
    Peking University              Freshman     1
    Shanghai Jiao Tong University  Freshman     1
                                   Senior       1
    dtype: int64



通过 get_group 方法可以直接获取所在组对应的行，此时必须知道组的具体名字：


```python
A.get_group(('Peking University','Freshman')).iloc[:3,:3]
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Peking University</td>
      <td>Freshman</td>
      <td>Changqiang You</td>
    </tr>
  </tbody>
</table>
</div>



## 二、聚合函数

### 1. 内置聚合函数


```python
gb = df.groupby('Gender')['Height']
gb.idxmin()
```




    Gender
    Female    0
    Male      1
    Name: Height, dtype: int64




```python
gb.quantile(0.95)
```




    Gender
    Female    158.90
    Male      187.41
    Name: Height, dtype: float64



### 2. agg方法


虽然在 groupby 对象上定义了许多方便的函数，但仍然有以下不便之处：

无法同时使用多个函数

无法对特定的列使用特定的聚合函数

无法使用自定义的聚合函数

无法直接对结果的列名在聚合前进行自定义命名
通过 agg 函数解决这四类问题：

#### 【a】使用多个函数


```python
gb.agg(['sum', 'idxmax', 'skew'])#当使用多个聚合函数时，需要用列表的形式把内置聚合函数
#对应的字符串传入，先前提到的所有字符串都是合法的。
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
      <th>sum</th>
      <th>idxmax</th>
      <th>skew</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>158.9</td>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>529.4</td>
      <td>2</td>
      <td>0.927959</td>
    </tr>
  </tbody>
</table>
</div>



#### 【b】对特定的列使用特定的聚合函数

对于方法和列的特殊对应，可以通过构造字典传入 agg 中实现，其中字典以列名为键，以聚合字符串或字符串列表为值。


```python
gb.agg({'Height':['mean','max'], 'Weight':'count'})
```


    ---------------------------------------------------------------------------

    SpecificationError                        Traceback (most recent call last)

    <ipython-input-32-12a17380636d> in <module>
    ----> 1 gb.agg({'Height':['mean','max'], 'Weight':'count'})
    

    D:\Anaconda3\lib\site-packages\pandas\core\groupby\generic.py in aggregate(self, func, engine, engine_kwargs, *args, **kwargs)
        244             # but not the class list / tuple itself.
        245             func = maybe_mangle_lambdas(func)
    --> 246             ret = self._aggregate_multiple_funcs(func)
        247             if relabeling:
        248                 ret.columns = columns
    

    D:\Anaconda3\lib\site-packages\pandas\core\groupby\generic.py in _aggregate_multiple_funcs(self, arg)
        290             # GH 15931
        291             if isinstance(self._selected_obj, Series):
    --> 292                 raise SpecificationError("nested renamer is not supported")
        293 
        294             columns = list(arg.keys())
    

    SpecificationError: nested renamer is not supported


#### 【c】使用自定义函数

在 agg 中可以使用具体的自定义函数， 需要注意传入函数的参数是之前数据源中的列，逐列进行计算 


```python
gb.agg(lambda x: x.mean()-x.min())#分组计算身高和体重的极差
```




    Gender
    Female    0.000000
    Male      9.966667
    Name: Height, dtype: float64



由于传入的是序列，因此序列上的方法和属性都是可以在函数中使用的，只需保证返回值是标量即可。下面的例子是指，如果组的指标均值，超过该指标的总体均值，返回High，否则返回Low。


```python
def my_function(s):
        res = 'High'
        if s.mean() <= df[s.name].mean():
            res = 'Low'
        return res
gb.agg(my_function)
```




    Gender
    Female     Low
    Male      High
    Name: Height, dtype: object



#### 【d】聚合结果重命名

如果想要对聚合结果的列名进行重命名，只需要将上述函数的位置改写成元组，元组的第一个元素为新的名字，第二个位置为原来的函数，包括聚合字符串和自定义函数


```python
gb.agg([('range', lambda x: x.max()-x.min()), ('my_sum', 'sum')])
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
      <th>range</th>
      <th>my_sum</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>0.0</td>
      <td>158.9</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>22.4</td>
      <td>529.4</td>
    </tr>
  </tbody>
</table>
</div>




```python
gb.agg({'Height': [(my_function='my_function'), 'sum'],'Weight': lambda x:x.max()})
```


      File "<ipython-input-43-03327d66caa9>", line 1
        gb.agg({'Height': [(my_function='my_function'), 'sum'],'Weight': lambda x:x.max()})
                                       ^
    SyntaxError: invalid syntax
    


## 三、变换和过滤

### 1. 变换函数与transform方法

变换函数的返回值为同长度的序列，最常用的内置变换函数是累计函数：  cumcount/cumsum/cumprod/cummax/cummin ，它们的使用方式和聚合函数类似，只不过完成的是组内累计操作。


```python
gb.cummax().head()
```




    0    158.9
    1    166.5
    2    188.9
    3      NaN
    4    188.9
    Name: Height, dtype: float64



当用自定义变换时需要使用 transform 方法，被调用的自定义函数， 其传入值为数据源的序列 ，与 agg 的传入类型是一致的，其最后的返回结果是行列索引与数据源一致的 DataFrame 。


```python
#身高和体重进行分组标准化，即减去组均值后除以组的标准差
gb.transform(lambda x: (x-x.mean())/x.std()).head()
```




    0         NaN
    1   -0.874123
    2    1.090461
    3         NaN
    4   -0.216338
    Name: Height, dtype: float64



### 2. 组索引与过滤

索引和过滤的区别

过滤在分组中是对于组的过滤，而索引是对于行的过滤，在第二章中的返回值，无论是布尔列表还是元素列表或者位置列表，本质上都是对于行的筛选，即如果符合筛选条件的则选入结果表，否则不选入。

组过滤作为行过滤的推广，指的是如果对一个组的全体所在行进行统计的结果返回 True 则会被保留， False 则该组会被过滤，最后把所有未被过滤的组其对应的所在行拼接起来作为 DataFrame 返回。

在 groupby 对象中，定义了 filter 方法进行组的筛选，其中自定义函数的输入参数为数据源构成的 DataFrame 本身，在之前例子中定义的 groupby 对象中，传入的就是 df[['Height', 'Weight']] ，因此所有表方法和属性都可以在自定义函数中相应地使用，同时只需保证自定义函数的返回为布尔值即可。


```python
#原表中通过过滤得到所有容量大于100的组：
gb.filter(lambda x: x.shape[0] > 100).head()
```




    Series([], Name: Height, dtype: float64)



## 四、跨列分组

### 1. apply的引入

现在如下定义身体质量指数BMI：
BMI=Weight/Height**2
其中体重和身高的单位分别为千克和米，需要分组计算组BMI的均值。
这显然不是过滤操作，因此 filter 不符合要求；其次，返回的均值是标量而不是序列，因此 transform 不符合要求；最后，似乎使用 agg 函数能够处理，但是之前强调过聚合函数是逐列处理的，而不能够 多列数据同时处理 。由此，引出了 apply 函数来解决这一问题。



### 2. apply的使用


```python
import pandas as pd
import numpy as np
def BMI(x):
        Height = x['Height']/100
        Weight = x['Weight']
        BMI_value = Weight/Height**2
        return BMI_value.mean()
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\learn_pandas.csv')
gb = df.groupby(['School', 'Grade'])
gb.apply(BMI)
```




    School                         Grade    
    Fudan University               Freshman     19.969411
                                   Junior       20.115806
                                   Senior       19.573687
                                   Sophomore    21.712565
    Peking University              Freshman     21.225845
                                   Junior       19.674964
                                   Senior       21.577345
                                   Sophomore    17.611119
    Shanghai Jiao Tong University  Freshman     21.208448
                                   Junior       19.429628
                                   Senior       21.451075
                                   Sophomore    19.772455
    Tsinghua University            Freshman     18.465769
                                   Junior       21.352761
                                   Senior       20.189919
                                   Sophomore    20.458102
    dtype: float64



#### 【 a】标量情况：结果得到的是 Series ，索引与 agg 的结果一致


```python
gb = df.groupby(['Gender','Test_Number'])[['Height','Weight']]
gb.apply(lambda x: 0)
```




    Gender  Test_Number
    Female  1              0
            2              0
            3              0
    Male    1              0
            2              0
            3              0
    dtype: int64




```python
gb.apply(lambda x: [0, 0]) # 虽然是列表，但是作为返回值仍然看作标量
```




    Gender  Test_Number
    Female  1              [0, 0]
            2              [0, 0]
            3              [0, 0]
    Male    1              [0, 0]
            2              [0, 0]
            3              [0, 0]
    dtype: object



#### 【b】 Series 情况：得到的是 DataFrame ，行索引与标量情况一致，列索引为 Series 的索引


```python
gb.apply(lambda x: pd.Series([0,0],index=['a','b']))
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
      <th>a</th>
      <th>b</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th>Test_Number</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">Female</th>
      <th>1</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">Male</th>
      <th>1</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



【c】 DataFrame 情况：得到的是 DataFrame ，行索引最内层在每个组原先 agg 的结果索引上，再加一层返回的 DataFrame 行索引，同时分组结果 DataFrame 的列索引和返回的 DataFrame 列索引一致。


```python
gb.apply(lambda x: pd.DataFrame(np.ones((2,2)),
                                    index = ['a','b'],
                                    columns=pd.Index([('w','x'),('y','z')])))
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
      <th></th>
      <th>w</th>
      <th>y</th>
    </tr>
    <tr>
      <th></th>
      <th></th>
      <th></th>
      <th>x</th>
      <th>z</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th>Test_Number</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="6" valign="top">Female</th>
      <th rowspan="2" valign="top">1</th>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2</th>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">3</th>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="6" valign="top">Male</th>
      <th rowspan="2" valign="top">1</th>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2</th>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">3</th>
      <th>a</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



## 五、练习

### Ex1：汽车数据集

现有一份汽车数据集，其中 Brand, Disp., HP 分别代表汽车品牌、发动机蓄量、发动机输出。


```python
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\joyful-pandas\data\car.csv')
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
      <th>Brand</th>
      <th>Price</th>
      <th>Country</th>
      <th>Reliability</th>
      <th>Mileage</th>
      <th>Type</th>
      <th>Weight</th>
      <th>Disp.</th>
      <th>HP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Eagle Summit 4</td>
      <td>8895</td>
      <td>USA</td>
      <td>4.0</td>
      <td>33</td>
      <td>Small</td>
      <td>2560</td>
      <td>97</td>
      <td>113</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ford Escort   4</td>
      <td>7402</td>
      <td>USA</td>
      <td>2.0</td>
      <td>33</td>
      <td>Small</td>
      <td>2345</td>
      <td>114</td>
      <td>90</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ford Festiva 4</td>
      <td>6319</td>
      <td>Korea</td>
      <td>4.0</td>
      <td>37</td>
      <td>Small</td>
      <td>1845</td>
      <td>81</td>
      <td>63</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Honda Civic 4</td>
      <td>6635</td>
      <td>Japan/USA</td>
      <td>5.0</td>
      <td>32</td>
      <td>Small</td>
      <td>2260</td>
      <td>91</td>
      <td>92</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mazda Protege 4</td>
      <td>6599</td>
      <td>Japan</td>
      <td>5.0</td>
      <td>32</td>
      <td>Small</td>
      <td>2440</td>
      <td>113</td>
      <td>103</td>
    </tr>
  </tbody>
</table>
</div>



1.先过滤出所属 Country 数超过2个的汽车，即若该汽车的 Country 在总体数据集中出现次数不超过2则剔除，再按 Country 分组计算价格均值、价格变异系数、该 Country 的汽车数量，其中变异系数的计算方法是标准差除以均值，并在结果中把变异系数重命名为 CoV 。

2.按照表中位置的前三分之一、中间三分之一和后三分之一分组，统计 Price 的均值。

3.对类型 Type 分组，对 Price 和 HP 分别计算最大值和最小值，结果会产生多级索引，请用下划线把多级列索引合并为单层索引。

4.对类型 Type 分组，对 HP 进行组内的 min-max 归一化。

5.对类型 Type 分组，计算 Disp. 与 HP 的相关系数。


```python
df.groupby('Country').filter(lambda x:x.shape[0]>2).groupby('Country')['Price'].agg([(
           'CoV', lambda x: x.std()/x.mean()), 'mean', 'count'])
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
      <th>CoV</th>
      <th>mean</th>
      <th>count</th>
    </tr>
    <tr>
      <th>Country</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Japan</th>
      <td>0.387429</td>
      <td>13938.052632</td>
      <td>19</td>
    </tr>
    <tr>
      <th>Japan/USA</th>
      <td>0.240040</td>
      <td>10067.571429</td>
      <td>7</td>
    </tr>
    <tr>
      <th>Korea</th>
      <td>0.243435</td>
      <td>7857.333333</td>
      <td>3</td>
    </tr>
    <tr>
      <th>USA</th>
      <td>0.203344</td>
      <td>12543.269231</td>
      <td>26</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape[0]
condition = ['Head']*20+['Mid']*20+['Tail']*20
df.groupby(condition)['Price'].mean()
```




    Head     9069.95
    Mid     13356.40
    Tail    15420.65
    Name: Price, dtype: float64




```python
res = df.groupby('Type').agg({'Price': ['max'], 'HP': ['min']})
res.columns = res.columns.map(lambda x:'_'.join(x))
res
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
      <th>Price_max</th>
      <th>HP_min</th>
    </tr>
    <tr>
      <th>Type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Compact</th>
      <td>18900</td>
      <td>95</td>
    </tr>
    <tr>
      <th>Large</th>
      <td>17257</td>
      <td>150</td>
    </tr>
    <tr>
      <th>Medium</th>
      <td>24760</td>
      <td>110</td>
    </tr>
    <tr>
      <th>Small</th>
      <td>9995</td>
      <td>63</td>
    </tr>
    <tr>
      <th>Sporty</th>
      <td>13945</td>
      <td>92</td>
    </tr>
    <tr>
      <th>Van</th>
      <td>15395</td>
      <td>106</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
