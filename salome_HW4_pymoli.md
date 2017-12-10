

```python
import pandas as pd
import json as js
import os
import numpy as np
import glob
```


```python
json1_path = "../purchase_data.json"
json2_path = "../purchase_data2.json"

for json_file in (json1_path, json2_path):
    df_pymoli = pd.read_json(json_file)

df_pymoli.head()

# Print the first five rows of data to the screen
#df.head()
#json_pattern = os.path.join(json_path,'*.json')
#file_list = glob.glob(json_pattern)
#for file in file_list:
  #contents.append(read(file))
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_pymoli.columns
```




    Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN'], dtype='object')




```python
#Count the unique name of players by counting the number of elements in row SN
total_players = df_pymoli['SN'].unique()
print (len(total_players))
df_pymoli1 = pd.DataFrame({'Total players': [len(total_players)]})
df_pymoli1
```

    74





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>74</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Total)
#Number of Unique Items

```


```python
df2= df_pymoli['Item ID'].unique()
len(df2)
```




    64




```python
#Total Revenue, should be the sum of all price values
Total_rev =round(df_pymoli['Price'].sum(),2)
Total_rev
```




    228.1




```python
#Purchasing Analysis (Total): Average Price, Total Number of Purchases, Number of Unique Items, Total Revenue
```


```python
df_pymoli2 = pd.DataFrame({'Number of Unique Items': len(df2), 'Average Price':[df_pymoli['Price'].mean()], 'Number of Purchases':[df_pymoli['Item ID'].count()],'Total Revenue':[df_pymoli['Price'].sum()]})
df_pymoli2["Average Price"] = df_pymoli2["Average Price"].map("$ {:,.2f}".format)
df_pymoli2["Total Revenue"] = df_pymoli2["Total Revenue"].map("$ {:,.2f}".format)
df_pymoli2

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Number of Unique Items</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>$ 2.92</td>
      <td>78</td>
      <td>64</td>
      <td>$ 228.10</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender)
#The below each broken by gender
#Purchase Count
```


```python
#Using groupby Gender, find the number of M, F, ND
grouped_gender = df_pymoli.groupby('Gender')
grouped_gender
# The object returned is a "GroupBy" object and cannot be viewed normally...
print(type(grouped_gender))
# In order to be visualized, a data function must be used...
grouped_gender.count().head()
```

    <class 'pandas.core.groupby.DataFrameGroupBy'>





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>64</td>
      <td>64</td>
      <td>64</td>
      <td>64</td>
      <td>64</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Number of M, F and ND that made at least one purchase
count_gender = grouped_gender["SN"].nunique()
count_gender.head()
total_players = count_gender.sum()# or see above
total_players
```




    74




```python
#Number of M, F and ND that made at least one purchase
count_gender = grouped_gender["SN"].nunique()
count_gender.head()
```




    Gender
    Female                   13
    Male                     60
    Other / Non-Disclosed     1
    Name: SN, dtype: int64




```python
##Percentage of players count by Gender(absolute values)
Perc_count1 = round(count_gender / total_players, 4)*100
Perc_count1
```




    Gender
    Female                   17.57
    Male                     81.08
    Other / Non-Disclosed     1.35
    Name: SN, dtype: float64




```python
df_pymoli3= pd.DataFrame({'Total count': count_gender, "Percentage of Players": Perc_count1 })
df_pymoli3["Percentage of Players"] =df_pymoli3["Percentage of Players"].map("{:.2f}".format)
df_pymoli3
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total count</th>
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
      <td>17.57</td>
      <td>13</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>81.08</td>
      <td>60</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.35</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Purchasing Analysis (Gender)
#The below each broken by gender
#Average Purchase Price
#Total Purchase Value
#Normalized Totals (normalizing for the # of people in each gender group)
```


```python
#Purchase count
purchase_count= grouped_gender["SN"].count()
purchase_count
```




    Gender
    Female                   13
    Male                     64
    Other / Non-Disclosed     1
    Name: SN, dtype: int64




```python
#Average Purchase Price grouped by M, F and ND
Average_Price = round(grouped_gender["Price"].mean(), 2)
Average_Price.head()
```




    Gender
    Female                   3.18
    Male                     2.88
    Other / Non-Disclosed    2.12
    Name: Price, dtype: float64




```python
#Total Purchase value grouped by M, F and ND
Total_Price = grouped_gender["Price"].sum()
Total_Price.head()
```




    Gender
    Female                    41.38
    Male                     184.60
    Other / Non-Disclosed      2.12
    Name: Price, dtype: float64




```python
#Normalized Purchase value grouped by M, F and ND
Normalized_Price = round(grouped_gender["Price"].sum()/count_gender, 2)
Normalized_Price.head()
```




    Gender
    Female                   3.18
    Male                     3.08
    Other / Non-Disclosed    2.12
    dtype: float64




```python
df_pymoli4= pd.DataFrame({'Purchase count': purchase_count, "Average Purchase price": Average_Price, "Total Purchase value": Total_Price, "Normalized Totals":Normalized_Price})
df_pymoli4["Average Purchase price"]=df_pymoli4["Average Purchase price"].map("$ {:,.2f}".format)
df_pymoli4["Total Purchase value"] = df_pymoli4["Total Purchase value"].map("$ {:,.2f}".format)  
df_pymoli4["Normalized Totals"] = df_pymoli4["Normalized Totals"].map("$ {:,.2f}".format)
df_pymoli4
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase price</th>
      <th>Normalized Totals</th>
      <th>Purchase count</th>
      <th>Total Purchase value</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>$ 3.18</td>
      <td>$ 3.18</td>
      <td>13</td>
      <td>$ 41.38</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>$ 2.88</td>
      <td>$ 3.08</td>
      <td>64</td>
      <td>$ 184.60</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>$ 2.12</td>
      <td>$ 2.12</td>
      <td>1</td>
      <td>$ 2.12</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age Demographics
#The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
#Purchase Count
#Average Purchase Price
#Total Purchase Value
#Normalized Totals (normalizing for the # of people in each age group)
```


```python
# Create the bins in which Data will be held
# Bins are 0 to 25, 25 to 50, 50 to 75, 75 to 100
bins = [0, 10, 14, 19, 24, 29, 34, 39, 100]

# Create the names for the four bins
group_names = ['<10', '10-14', '15-19', '20-24', '25-29','30-34', '35-39','40+']
```


```python
# Cut postTestScore and place the scores into bins
#pd.cut(df_pymoli["Age"], bins, labels=group_names)
```


```python
df_pymoli["Age group"] = pd.cut(df_pymoli["Age"], bins, labels=group_names)
df_pymoli.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age group</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20</td>
      <td>Male</td>
      <td>93</td>
      <td>Apocalyptic Battlescythe</td>
      <td>4.49</td>
      <td>Iloni35</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>12</td>
      <td>Dawne</td>
      <td>3.36</td>
      <td>Aidaira26</td>
      <td>20-24</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17</td>
      <td>Male</td>
      <td>5</td>
      <td>Putrid Fan</td>
      <td>2.63</td>
      <td>Irim47</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17</td>
      <td>Male</td>
      <td>123</td>
      <td>Twilight's Carver</td>
      <td>2.55</td>
      <td>Irith83</td>
      <td>15-19</td>
    </tr>
    <tr>
      <th>4</th>
      <td>22</td>
      <td>Male</td>
      <td>154</td>
      <td>Feral Katana</td>
      <td>4.11</td>
      <td>Philodil43</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Using groupby age group
grouped_age = df_pymoli.groupby('Age group')
grouped_age
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x114b86dd8>




```python
count_by_age = grouped_age["SN"].nunique()
count_by_age
```




    Age group
    <10       5
    10-14     3
    15-19    11
    20-24    34
    25-29     8
    30-34     6
    35-39     6
    40+       1
    Name: SN, dtype: int64




```python
##Percentage of players count by Gender(absolute values)
Perc_count2 = round(count_by_age / total_players, 4)*100
Perc_count2
```




    Age group
    <10       6.76
    10-14     4.05
    15-19    14.86
    20-24    45.95
    25-29    10.81
    30-34     8.11
    35-39     8.11
    40+       1.35
    Name: SN, dtype: float64




```python
df_pymoli5= pd.DataFrame({'Total count': count_by_age, "Percentage of Players": Perc_count2 })
df_pymoli5["Percentage of Players"]=df_pymoli5["Percentage of Players"].map("{:,.2f}".format)
df_pymoli5
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Percentage of Players</th>
      <th>Total count</th>
    </tr>
    <tr>
      <th>Age group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>6.76</td>
      <td>5</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4.05</td>
      <td>3</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>14.86</td>
      <td>11</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>45.95</td>
      <td>34</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>10.81</td>
      <td>8</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.11</td>
      <td>6</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>8.11</td>
      <td>6</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>1.35</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Age Demographics
#The below each broken into bins of 4 years (i.e. <10, 10-14, 15-19, etc.)
#Average Purchase Price
#Total Purchase Value
#Normalized Totals (normalizing for the # of people in each age group)
```


```python
#Purchase count
purchase_count2= grouped_age["SN"].count()
purchase_count2
```




    Age group
    <10       5
    10-14     3
    15-19    11
    20-24    36
    25-29     9
    30-34     7
    35-39     6
    40+       1
    Name: SN, dtype: int64




```python
#Average Purchase Price grouped by M, F and ND
Average_Price2 = round(grouped_age["Price"].mean(),2)
Average_Price2
```




    Age group
    <10      2.76
    10-14    2.99
    15-19    2.76
    20-24    3.02
    25-29    2.90
    30-34    1.98
    35-39    3.56
    40+      4.65
    Name: Price, dtype: float64




```python
#Total Purchase value grouped by M, F and ND
Total_Price2 = grouped_age["Price"].sum()
Total_Price2
```




    Age group
    <10       13.82
    10-14      8.96
    15-19     30.41
    20-24    108.89
    25-29     26.11
    30-34     13.89
    35-39     21.37
    40+        4.65
    Name: Price, dtype: float64




```python
#Normalized Purchase value grouped by M, F and ND
Normalized_Price2 = round(grouped_age["Price"].sum()/count_by_age,2)
Normalized_Price2
```




    Age group
    <10      2.76
    10-14    2.99
    15-19    2.76
    20-24    3.20
    25-29    3.26
    30-34    2.32
    35-39    3.56
    40+      4.65
    dtype: float64




```python
df_pymoli6= pd.DataFrame({'Purchase count': purchase_count2, "Average Purchase price": Average_Price2, "Total Purchase value": Total_Price2, "Normalized Totals":Normalized_Price2})
df_pymoli6["Average Purchase price"]=df_pymoli6["Average Purchase price"].map("$ {:,.2f}".format)
df_pymoli6["Total Purchase value"]=df_pymoli6["Total Purchase value"].map("$ {:,.2f}".format)
df_pymoli6["Normalized Totals"]=df_pymoli6["Normalized Totals"].map("$ {:,.2f}".format)
df_pymoli6
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase price</th>
      <th>Normalized Totals</th>
      <th>Purchase count</th>
      <th>Total Purchase value</th>
    </tr>
    <tr>
      <th>Age group</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>$ 2.76</td>
      <td>$ 2.76</td>
      <td>5</td>
      <td>$ 13.82</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>$ 2.99</td>
      <td>$ 2.99</td>
      <td>3</td>
      <td>$ 8.96</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>$ 2.76</td>
      <td>$ 2.76</td>
      <td>11</td>
      <td>$ 30.41</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>$ 3.02</td>
      <td>$ 3.20</td>
      <td>36</td>
      <td>$ 108.89</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>$ 2.90</td>
      <td>$ 3.26</td>
      <td>9</td>
      <td>$ 26.11</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>$ 1.98</td>
      <td>$ 2.32</td>
      <td>7</td>
      <td>$ 13.89</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>$ 3.56</td>
      <td>$ 3.56</td>
      <td>6</td>
      <td>$ 21.37</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>$ 4.65</td>
      <td>$ 4.65</td>
      <td>1</td>
      <td>$ 4.65</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Top Spenders
#Identify the the top 5 spenders in the game by total purchase value, then list (in a table):SN
#Purchase Count
#Average Purchase Price
#Total Purchase Value
```


```python
grouped_SN = df_pymoli.groupby('SN')
grouped_SN
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x114d02e10>




```python
#Purchase count
purchase_count3= grouped_SN["SN"].count()
purchase_count3.head()
```




    SN
    Aeri79           1
    Aerithllora36    1
    Aesririam61      1
    Aesurstilis64    1
    Aidaira26        2
    Name: SN, dtype: int64




```python
#Average Purchase Price grouped by M, F and ND
Average_Price3 = round(grouped_SN["Price"].mean(),2)
Average_Price3.head()
```




    SN
    Aeri79           4.15
    Aerithllora36    4.65
    Aesririam61      2.65
    Aesurstilis64    4.25
    Aidaira26        2.56
    Name: Price, dtype: float64




```python
Total_Price3 = grouped_SN["Price"].sum()
Total_Price3.head()
```




    SN
    Aeri79           4.15
    Aerithllora36    4.65
    Aesririam61      2.65
    Aesurstilis64    4.25
    Aidaira26        5.13
    Name: Price, dtype: float64




```python
#Total_Price3 = grouped_SN["Price"].sum()
#Total_Price3.sort_values(ascending=False).head(5)
```


```python
df_pymoli7= pd.DataFrame({'Purchase count': purchase_count3, "Average Purchase price": Average_Price3, "Total Purchase value": Total_Price3})
df_pymoli7["Average Purchase price"] = df_pymoli7["Average Purchase price"].map("$ {:,.2f}".format)
df_pymoli7["Total Purchase value"] = df_pymoli7["Total Purchase value"].map("$ {:,.2f}".format)
df_pymoli7.sort_values('Total Purchase value', ascending=False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Purchase price</th>
      <th>Purchase count</th>
      <th>Total Purchase value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Sundaky74</th>
      <td>$ 3.70</td>
      <td>2</td>
      <td>$ 7.41</td>
    </tr>
    <tr>
      <th>Aidaira26</th>
      <td>$ 2.56</td>
      <td>2</td>
      <td>$ 5.13</td>
    </tr>
    <tr>
      <th>Eusty71</th>
      <td>$ 4.81</td>
      <td>1</td>
      <td>$ 4.81</td>
    </tr>
    <tr>
      <th>Chanirra64</th>
      <td>$ 4.78</td>
      <td>1</td>
      <td>$ 4.78</td>
    </tr>
    <tr>
      <th>Alarap40</th>
      <td>$ 4.71</td>
      <td>1</td>
      <td>$ 4.71</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Popular Items
#Identify the 5 most popular items by purchase count, then list (in a table):
#Item ID
#Item Name
#Purchase Count
#Item Price
#Total Purchase Value
```


```python
grouped_Item_ID = df_pymoli.groupby (['Item ID','Item Name'])
grouped_Item_ID.count().head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Price</th>
      <th>SN</th>
      <th>Age group</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>Splinter</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <th>Putrid Fan</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Average Purchase Price grouped by M, F and ND
Item_price = grouped_Item_ID["Price"].mean()
```


```python
#Item name
item_name= grouped_Item_ID["Item Name"]
item_name.count().head()
```




    Item ID  Item Name         
    0        Splinter              1
    1        Crucifer              1
    2        Verdict               1
    4        Bloodlord's Fetish    1
    5        Putrid Fan            1
    Name: Item Name, dtype: int64




```python
#Purchase count
purchase_count4= grouped_Item_ID["SN"].count()
purchase_count4.head()
```




    Item ID  Item Name         
    0        Splinter              1
    1        Crucifer              1
    2        Verdict               1
    4        Bloodlord's Fetish    1
    5        Putrid Fan            1
    Name: SN, dtype: int64




```python
Total_Price4 = grouped_Item_ID["Price"].sum()
Total_Price4.head()
```




    Item ID  Item Name         
    0        Splinter              1.89
    1        Crucifer              3.67
    2        Verdict               2.65
    4        Bloodlord's Fetish    1.91
    5        Putrid Fan            2.63
    Name: Price, dtype: float64




```python
df_pymoli8= pd.DataFrame({"Item Price":Item_price,'Purchase count': purchase_count4, 'Total purchase value':Total_Price4})
df_pymoli8["Item Price"]=df_pymoli8["Item Price"].map("$ {:,.2f}".format)
df_pymoli8['Total purchase value']= df_pymoli8['Total purchase value'].map("{:,.2f}".format).apply(lambda x: "$"+str(x))
df_pymoli8.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Item Price</th>
      <th>Purchase count</th>
      <th>Total purchase value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <th>Splinter</th>
      <td>$ 1.89</td>
      <td>1</td>
      <td>$1.89</td>
    </tr>
    <tr>
      <th>1</th>
      <th>Crucifer</th>
      <td>$ 3.67</td>
      <td>1</td>
      <td>$3.67</td>
    </tr>
    <tr>
      <th>2</th>
      <th>Verdict</th>
      <td>$ 2.65</td>
      <td>1</td>
      <td>$2.65</td>
    </tr>
    <tr>
      <th>4</th>
      <th>Bloodlord's Fetish</th>
      <td>$ 1.91</td>
      <td>1</td>
      <td>$1.91</td>
    </tr>
    <tr>
      <th>5</th>
      <th>Putrid Fan</th>
      <td>$ 2.63</td>
      <td>1</td>
      <td>$2.63</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_pymoli8.sort_values("Purchase count",ascending=False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Item Price</th>
      <th>Purchase count</th>
      <th>Total purchase value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <td>$ 3.64</td>
      <td>3</td>
      <td>$10.92</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <td>$ 4.12</td>
      <td>2</td>
      <td>$8.24</td>
    </tr>
    <tr>
      <th>111</th>
      <th>Misery's End</th>
      <td>$ 1.79</td>
      <td>2</td>
      <td>$3.58</td>
    </tr>
    <tr>
      <th>64</th>
      <th>Fusion Pummel</th>
      <td>$ 2.42</td>
      <td>2</td>
      <td>$4.84</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <td>$ 4.11</td>
      <td>2</td>
      <td>$8.22</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Most Profitable Items
#Identify the 5 most profitable items by total purchase value, then list (in a table):
#Item ID
#Item Name
#Purchase Count
#Item Price
#Total Purchase Value
```


```python
df_pymoli8= pd.DataFrame({"Item Price":Item_price,'Purchase count': purchase_count4, 'Total purchase value':Total_Price4})
df_pymoli8["Item Price"]=df_pymoli8["Item Price"].map("$ {:,.2f}".format)
#df_pymoli8['Total purchase value']= df_pymoli8['Total purchase value'].map("{:,.2f}".format).apply(lambda x: "$"+str(x))
df_pymoli8.sort_values("Total purchase value", ascending= False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Item Price</th>
      <th>Purchase count</th>
      <th>Total purchase value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>94</th>
      <th>Mourning Blade</th>
      <td>$ 3.64</td>
      <td>3</td>
      <td>10.92</td>
    </tr>
    <tr>
      <th>117</th>
      <th>Heartstriker, Legacy of the Light</th>
      <td>$ 4.71</td>
      <td>2</td>
      <td>9.42</td>
    </tr>
    <tr>
      <th>93</th>
      <th>Apocalyptic Battlescythe</th>
      <td>$ 4.49</td>
      <td>2</td>
      <td>8.98</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <td>$ 4.12</td>
      <td>2</td>
      <td>8.24</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <td>$ 4.11</td>
      <td>2</td>
      <td>8.22</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_pymoli8= pd.DataFrame({"Item Price":Item_price,'Purchase count': purchase_count4, 'Total purchase value':Total_Price4})
df_pymoli8["Item Price"]=df_pymoli8["Item Price"].map("$ {:,.2f}".format)
df_pymoli8['Total purchase value']= df_pymoli8['Total purchase value'].map("{:,.2f}".format).apply(lambda x: "$"+str(x))
df_pymoli8.sort_values("Total purchase value", ascending= False).head(5)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Item Price</th>
      <th>Purchase count</th>
      <th>Total purchase value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>117</th>
      <th>Heartstriker, Legacy of the Light</th>
      <td>$ 4.71</td>
      <td>2</td>
      <td>$9.42</td>
    </tr>
    <tr>
      <th>93</th>
      <th>Apocalyptic Battlescythe</th>
      <td>$ 4.49</td>
      <td>2</td>
      <td>$8.98</td>
    </tr>
    <tr>
      <th>90</th>
      <th>Betrayer</th>
      <td>$ 4.12</td>
      <td>2</td>
      <td>$8.24</td>
    </tr>
    <tr>
      <th>154</th>
      <th>Feral Katana</th>
      <td>$ 4.11</td>
      <td>2</td>
      <td>$8.22</td>
    </tr>
    <tr>
      <th>180</th>
      <th>Stormcaller</th>
      <td>$ 2.77</td>
      <td>2</td>
      <td>$5.54</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Not corrected sorting of the Total purchase value using the dollar sign... Please help!
```
