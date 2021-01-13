# Task Special & Task 11 综合练习


```python
import pandas as pd
import numpy as np
```

## 任务一企业收入的多样性

【题目描述】一个企业的产业收入多样性可以仿照信息熵的概念来定义收入熵指标：其中 

![1610549385%281%29.jpg](attachment:1610549385%281%29.jpg)
p(xi)是企业该年某产业收入额占该年所有产业总收入的比重。在company.csv中存有需要计算的企业和年份，在company_data.csv中存有企业、各类收入额和收入年份的信息。现请利用后一张表中的数据，在前一张表中增加一列表示该公司该年份的收入熵指标 
I。



```python
A = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\data\Company.csv')
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
      <th>证券代码</th>
      <th>日期</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>#000007</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>1</th>
      <td>#000403</td>
      <td>2015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>#000408</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>3</th>
      <td>#000408</td>
      <td>2017</td>
    </tr>
    <tr>
      <th>4</th>
      <td>#000426</td>
      <td>2015</td>
    </tr>
  </tbody>
</table>
</div>




```python
B = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\data\Company_data.csv')
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
      <th></th>
      <th>证券代码</th>
      <th>日期</th>
      <th>收入类型</th>
      <th>收入额</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2008/12/31</td>
      <td>1</td>
      <td>1.084218e+10</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2008/12/31</td>
      <td>2</td>
      <td>1.259789e+10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2008/12/31</td>
      <td>3</td>
      <td>1.451312e+10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>2008/12/31</td>
      <td>4</td>
      <td>1.063843e+09</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>2008/12/31</td>
      <td>5</td>
      <td>8.513880e+08</td>
    </tr>
  </tbody>
</table>
</div>




```python
B['证券代码'] = B['证券代码'].apply(lambda x:'#%06d'%x)
B = B[B['证券代码'].isin(A['证券代码'])]
B['日期'] = B['日期'].apply(lambda x: int(x[:4]))
res = B.groupby(['证券代码', '日期'])['收入额'].apply(lambda x: -((x/x.sum()*np.log(x/x.sum()))).sum()).reset_index()
res = A.merge(res, how='left', on=['证券代码', '日期']).rename(columns={'收入额': '收入熵'})
res
```

## 【任务二】组队学习信息表的变换

【题目描述】请把组队学习的队伍信息表变换为如下形态，其中“是否队长”一列取1表示队长，否则为0
是否队长	队伍名称	    昵称    	编号
0	1	    你说的都对队	山枫叶纷飞	5
1	0	    你说的都对队	蔡	        6
2	0	    你说的都对队	安慕希	    7
3	0	    你说的都对队	信仰	    8
4	0	    你说的都对队	biubiu🙈🙈	20
...	...	    ...	        ...	        ...
141	0	    七星联盟	    Daisy	    63
142	0	    七星联盟    	One Better	131
143	0	    七星联盟    	rain	    112
144	1	    应如是	    思无邪	    54
145	0	    应如是	    Justzer0	58

```python
df = pd.read_excel(r'C:\Users\zhoukaiwei\Desktop\data\组队信息汇总表（Pandas）.xlsx')
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
      <th>所在群</th>
      <th>队伍名称</th>
      <th>队长编号</th>
      <th>队长_群昵称</th>
      <th>队员1 编号</th>
      <th>队员_群昵称</th>
      <th>队员2 编号</th>
      <th>队员_群昵称.1</th>
      <th>队员3 编号</th>
      <th>队员_群昵称.2</th>
      <th>...</th>
      <th>队员6 编号</th>
      <th>队员_群昵称.5</th>
      <th>队员7 编号</th>
      <th>队员_群昵称.6</th>
      <th>队员8 编号</th>
      <th>队员_群昵称.7</th>
      <th>队员9 编号</th>
      <th>队员_群昵称.8</th>
      <th>队员10编号</th>
      <th>队员_群昵称.9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Pandas数据分析</td>
      <td>你说的都对队</td>
      <td>5</td>
      <td>山枫叶纷飞</td>
      <td>6</td>
      <td>蔡</td>
      <td>7.0</td>
      <td>安慕希</td>
      <td>8.0</td>
      <td>信仰</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Pandas数据分析</td>
      <td>熊猫人</td>
      <td>175</td>
      <td>鱼呲呲</td>
      <td>44</td>
      <td>Heaven</td>
      <td>37.0</td>
      <td>吕青</td>
      <td>50.0</td>
      <td>余柳成荫</td>
      <td>...</td>
      <td>25.0</td>
      <td>Never say never</td>
      <td>55.0</td>
      <td>K</td>
      <td>120.0</td>
      <td>Y.</td>
      <td>28.0</td>
      <td>X.Y.Q</td>
      <td>151.0</td>
      <td>swrong</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Pandas数据分析</td>
      <td>中国移不动</td>
      <td>107</td>
      <td>Y's</td>
      <td>124</td>
      <td>🥕</td>
      <td>75.0</td>
      <td>Vito</td>
      <td>146.0</td>
      <td>张小五</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pandas数据分析</td>
      <td>panda</td>
      <td>11</td>
      <td>太下真君</td>
      <td>35</td>
      <td>柚子</td>
      <td>108.0</td>
      <td>My</td>
      <td>42.0</td>
      <td>星星点灯</td>
      <td>...</td>
      <td>157.0</td>
      <td>Zys</td>
      <td>158.0</td>
      <td>不器</td>
      <td>102.0</td>
      <td>嘉平佑染</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pandas数据分析</td>
      <td>一路向北</td>
      <td>13</td>
      <td>黄元帅</td>
      <td>15</td>
      <td>化</td>
      <td>16.0</td>
      <td>未期</td>
      <td>18.0</td>
      <td>太陽光下</td>
      <td>...</td>
      <td>23.0</td>
      <td>🚀</td>
      <td>169.0</td>
      <td>听风</td>
      <td>189.0</td>
      <td>Cappuccino</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>



### 【任务三】美国大选投票情况
【题目描述】两张数据表中分别给出了美国各县（county）的人口数以及大选的投票情况，请解决以下问题：

1.有多少县满足总投票数超过县人口数的一半
2.把州（state）作为行索引，把投票候选人作为列名，列名的顺序按照候选人在全美的总票数由高到低排序，行列对应的元素为该候选人在该州获得的总票数
3.每一个州下设若干县，定义拜登在该县的得票率减去川普在该县的得票率为该县的BT指标，若某个州所有县BT指标的中位数大于0，则称该州为Biden State，请找出所有的Biden State
# 此处是一个样例，实际的州或人名用原表的英语代替
            拜登   川普
威斯康星州   2      1
德克萨斯州   3      4

```python
df = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\data\president_county_candidate.csv')
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
      <th>state</th>
      <th>county</th>
      <th>candidate</th>
      <th>party</th>
      <th>total_votes</th>
      <th>won</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Delaware</td>
      <td>Kent County</td>
      <td>Joe Biden</td>
      <td>DEM</td>
      <td>44552</td>
      <td>True</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Delaware</td>
      <td>Kent County</td>
      <td>Donald Trump</td>
      <td>REP</td>
      <td>41009</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Delaware</td>
      <td>Kent County</td>
      <td>Jo Jorgensen</td>
      <td>LIB</td>
      <td>1044</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Delaware</td>
      <td>Kent County</td>
      <td>Howie Hawkins</td>
      <td>GRN</td>
      <td>420</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Delaware</td>
      <td>New Castle County</td>
      <td>Joe Biden</td>
      <td>DEM</td>
      <td>195034</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>



## 【任务四】显卡日志

下面给出了3090显卡的性能测评日志结果，每一条日志有如下结构：
Benchmarking #2# #4# precision type #1#
#1#  model average #2# time :  #3# ms
其中#1#代表的是模型名称，#2#的值为train(ing)或inference，表示训练状态或推断状态，#3#表示耗时，#4#表示精度，其中包含了float, half, double三种类型，下面是一个具体的例子：
Benchmarking Inference float precision type resnet50
resnet50  model average inference time :  13.426570892333984 ms
请把日志结果进行整理，变换成如下状态，model_i用相应模型名称填充，按照字母顺序排序，数值保留三位小数：
Train_half	Train_float	Train_double	Inference_half	Inference_float	Inference_double
model_1	0.954	0.901	0.357	0.281	0.978	1.130
model_2	0.360	0.794	0.011	1.083	1.137	0.394
## 【任务五】水压站点的特征工程

df1和df2中分别给出了18年和19年各个站点的数据，其中列中的H0至H23分别代表当天0点至23点；df3中记录了18-19年的每日该地区的天气情况，请完成如下的任务：
1.通过df1和df2构造df，把时间设为索引，第一列为站点编号，第二列为对应时刻的压力大小，排列方式如下（压力数值请用正确的值替换）：
                  站点    压力
2018-01-01 00:00:00       1    1.0
2018-01-01 00:00:00       2    1.0
...                     ...    ...
2018-01-01 00:00:00       30    1.0
2018-01-01 01:00:00       1    1.0
2018-01-01 01:00:00       2    1.0
...                     ...    ...
2019-12-31 23:00:00       30    1.02.在上一问构造的df基础上，构造下面的特征序列或DataFrame，并把它们逐个拼接到df的右侧

当天最高温、最低温和它们的温差
当天是否有沙暴、是否有雾、是否有雨、是否有雪、是否为晴天
选择一种合适的方法度量雨量/下雪量的大小（构造两个序列分别表示二者大小）
限制只用4列，对风向进行0-1编码（只考虑风向，不考虑大小）3.对df的水压一列构造如下时序特征：

当前时刻该站点水压与本月的相同整点时间该站点水压均值的差，例如当前时刻为2018-05-20 17:00:00，那么对应需要减去的值为当前月所有17:00:00时间点水压值的均值
当前时刻所在周的周末该站点水压均值与工作日水压均值之差
当前时刻向前7日内，该站点水压的均值、标准差、0.95分位数、下雨天数与下雪天数的总和
当前时刻向前7日内，该站点同一整点时间水压的均值、标准差、0.95分位数
当前时刻所在日的该站点水压最高值与最低值出现时刻的时间差

```python
df1 = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\data\yali18.csv')
df1.head()
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
      <th>Time</th>
      <th>MeasName</th>
      <th>H0</th>
      <th>H1</th>
      <th>H2</th>
      <th>H3</th>
      <th>H4</th>
      <th>H5</th>
      <th>H6</th>
      <th>H7</th>
      <th>...</th>
      <th>H14</th>
      <th>H15</th>
      <th>H16</th>
      <th>H17</th>
      <th>H18</th>
      <th>H19</th>
      <th>H20</th>
      <th>H21</th>
      <th>H22</th>
      <th>H23</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-01-01</td>
      <td>站点4</td>
      <td>0.402750</td>
      <td>0.407625</td>
      <td>0.418125</td>
      <td>0.425250</td>
      <td>0.426000</td>
      <td>0.425250</td>
      <td>0.417375</td>
      <td>0.426375</td>
      <td>...</td>
      <td>0.348750</td>
      <td>0.359250</td>
      <td>0.355500</td>
      <td>0.344250</td>
      <td>0.352125</td>
      <td>0.356250</td>
      <td>0.347250</td>
      <td>0.343875</td>
      <td>0.356625</td>
      <td>0.418875</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-01-01</td>
      <td>站点7</td>
      <td>0.214375</td>
      <td>0.226750</td>
      <td>0.232375</td>
      <td>0.233125</td>
      <td>0.235000</td>
      <td>0.232750</td>
      <td>0.230875</td>
      <td>0.220000</td>
      <td>...</td>
      <td>0.187375</td>
      <td>0.196750</td>
      <td>0.199750</td>
      <td>0.192250</td>
      <td>0.186250</td>
      <td>0.183250</td>
      <td>0.177250</td>
      <td>0.163375</td>
      <td>0.165250</td>
      <td>0.199375</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-01-01</td>
      <td>站点22</td>
      <td>0.247000</td>
      <td>0.248125</td>
      <td>0.271375</td>
      <td>0.251125</td>
      <td>0.272125</td>
      <td>0.256375</td>
      <td>0.257125</td>
      <td>0.242500</td>
      <td>...</td>
      <td>0.245500</td>
      <td>0.242875</td>
      <td>0.238375</td>
      <td>0.230875</td>
      <td>0.237250</td>
      <td>0.236875</td>
      <td>0.236500</td>
      <td>0.236500</td>
      <td>0.241000</td>
      <td>0.254500</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-01</td>
      <td>站点21</td>
      <td>0.284250</td>
      <td>0.289875</td>
      <td>0.283500</td>
      <td>0.281250</td>
      <td>0.288375</td>
      <td>0.288750</td>
      <td>0.285750</td>
      <td>0.255750</td>
      <td>...</td>
      <td>0.227625</td>
      <td>0.238125</td>
      <td>0.238500</td>
      <td>0.218625</td>
      <td>0.207000</td>
      <td>0.212625</td>
      <td>0.209250</td>
      <td>0.189000</td>
      <td>0.217875</td>
      <td>0.270000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-01-01</td>
      <td>站点20</td>
      <td>0.292875</td>
      <td>0.295875</td>
      <td>0.305250</td>
      <td>0.298875</td>
      <td>0.310125</td>
      <td>0.300750</td>
      <td>0.288375</td>
      <td>0.262500</td>
      <td>...</td>
      <td>0.247500</td>
      <td>0.241125</td>
      <td>0.243375</td>
      <td>0.232500</td>
      <td>0.233625</td>
      <td>0.224250</td>
      <td>0.219375</td>
      <td>0.202125</td>
      <td>0.219375</td>
      <td>0.286500</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 26 columns</p>
</div>




```python
df2 = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\data\yali19.csv')
df2.head()
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
      <th>Time</th>
      <th>MeasName</th>
      <th>H0</th>
      <th>H1</th>
      <th>H2</th>
      <th>H3</th>
      <th>H4</th>
      <th>H5</th>
      <th>H6</th>
      <th>H7</th>
      <th>...</th>
      <th>H14</th>
      <th>H15</th>
      <th>H16</th>
      <th>H17</th>
      <th>H18</th>
      <th>H19</th>
      <th>H20</th>
      <th>H21</th>
      <th>H22</th>
      <th>H23</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2019-01-01</td>
      <td>站点4</td>
      <td>0.342000</td>
      <td>0.429375</td>
      <td>0.429000</td>
      <td>0.440250</td>
      <td>0.445875</td>
      <td>0.444750</td>
      <td>0.417750</td>
      <td>0.387000</td>
      <td>...</td>
      <td>0.319875</td>
      <td>0.326250</td>
      <td>0.323625</td>
      <td>0.322500</td>
      <td>0.309000</td>
      <td>0.307125</td>
      <td>0.307125</td>
      <td>0.307125</td>
      <td>0.307125</td>
      <td>0.307125</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019-01-01</td>
      <td>站点7</td>
      <td>0.215125</td>
      <td>0.239500</td>
      <td>0.257500</td>
      <td>0.246250</td>
      <td>0.275125</td>
      <td>0.264625</td>
      <td>0.229375</td>
      <td>0.205375</td>
      <td>...</td>
      <td>0.180625</td>
      <td>0.176500</td>
      <td>0.181375</td>
      <td>0.155125</td>
      <td>0.159625</td>
      <td>0.146125</td>
      <td>0.144625</td>
      <td>0.135250</td>
      <td>0.158875</td>
      <td>0.184750</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2019-01-01</td>
      <td>站点22</td>
      <td>0.244750</td>
      <td>0.248875</td>
      <td>0.246625</td>
      <td>0.247375</td>
      <td>0.247375</td>
      <td>0.245500</td>
      <td>0.244000</td>
      <td>0.239500</td>
      <td>...</td>
      <td>0.238000</td>
      <td>0.236125</td>
      <td>0.235375</td>
      <td>0.238000</td>
      <td>0.231250</td>
      <td>0.232375</td>
      <td>0.226750</td>
      <td>0.227875</td>
      <td>0.236125</td>
      <td>0.242125</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2019-01-01</td>
      <td>站点21</td>
      <td>0.228750</td>
      <td>0.248250</td>
      <td>0.258750</td>
      <td>0.252750</td>
      <td>0.264375</td>
      <td>0.265875</td>
      <td>0.237750</td>
      <td>0.208125</td>
      <td>...</td>
      <td>0.200625</td>
      <td>0.202125</td>
      <td>0.198000</td>
      <td>0.186750</td>
      <td>0.185250</td>
      <td>0.180000</td>
      <td>0.174750</td>
      <td>0.177375</td>
      <td>0.192750</td>
      <td>0.212625</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-01-01</td>
      <td>站点20</td>
      <td>0.239125</td>
      <td>0.260500</td>
      <td>0.269125</td>
      <td>0.263500</td>
      <td>0.278125</td>
      <td>0.279625</td>
      <td>0.250375</td>
      <td>0.216625</td>
      <td>...</td>
      <td>0.212500</td>
      <td>0.214375</td>
      <td>0.202000</td>
      <td>0.199000</td>
      <td>0.195250</td>
      <td>0.188500</td>
      <td>0.187750</td>
      <td>0.186625</td>
      <td>0.205000</td>
      <td>0.225250</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 26 columns</p>
</div>




```python
df3 = pd.read_csv(r'C:\Users\zhoukaiwei\Desktop\data\qx1819.csv')
df3.head()
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
      <th>日期</th>
      <th>天气</th>
      <th>气温</th>
      <th>风向</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-01-01</td>
      <td>多云</td>
      <td>1C～-4C</td>
      <td>东南风 微风</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-01-02</td>
      <td>阴转多云</td>
      <td>8C～0C</td>
      <td>东北风 3-4级</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-01-03</td>
      <td>阴转小雪</td>
      <td>1C～-1C</td>
      <td>东北风 4-5级转4-5级</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-04</td>
      <td>阴</td>
      <td>0C～-4C</td>
      <td>东北风转北风 3-4级转3-4级</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-01-05</td>
      <td>阴转多云</td>
      <td>3C～-4C</td>
      <td>西风转北风 3-4级转3-4级</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
