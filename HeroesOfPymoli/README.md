
# Heroes Of Pymoli Data Analysis

- OBSERVED TREND 1
- OBSERVED TREND 2
- OBSERVED TREND 3



```python
import pandas as pd
import numpy as np
```


```python
Heroes_original_df = pd.read_json('raw_data/purchase_data.json')
```


```python
Heroes_original_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 780 entries, 0 to 779
    Data columns (total 6 columns):
    Age          780 non-null int64
    Gender       780 non-null object
    Item ID      780 non-null int64
    Item Name    780 non-null object
    Price        780 non-null float64
    SN           780 non-null object
    dtypes: float64(1), int64(2), object(3)
    memory usage: 36.6+ KB
    


```python
Heroes_original_df.columns
```




    Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN'], dtype='object')




```python
Heroes_original_df.head()
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
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
Heroes_original_df['Gender'].value_counts()
```




    Male                     633
    Female                   136
    Other / Non-Disclosed     11
    Name: Gender, dtype: int64



## Total Number of Players


```python
# Total Number of Players
Total_no_of_players = pd.DataFrame([Heroes_original_df['SN'].nunique()],
                                   columns = ['Total Players'])
Total_no_of_players
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)


```python
Purchasing_analysis_total = pd.DataFrame([[Heroes_original_df['Item Name'].nunique(), Heroes_original_df['Price'].mean(),
                                     Heroes_original_df['Item Name'].count(),Heroes_original_df['Price'].sum()]],
                                   columns = ['No of Unique Items','Average Price','Number of Purchases','Total Revenue']
                                  )
Purchasing_analysis_total['Average Price'] = Purchasing_analysis_total['Average Price'].map("${:.2f}".format)
Purchasing_analysis_total['Total Revenue'] = Purchasing_analysis_total['Total Revenue'].map("${:.2f}".format)

Purchasing_analysis_total

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
      <th>No of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2286.33</td>
    </tr>
  </tbody>
</table>
</div>



### Gender Demographics


```python
Gender_Demographics = pd.DataFrame(Heroes_original_df.groupby('Gender').SN.nunique())
Gender_Demographics.columns = ['Total Count']
Gender_Demographics['Percentage of Players'] = round(Gender_Demographics['Total Count']/Heroes_original_df['SN'].nunique()*100)
Gender_Demographics = Gender_Demographics[['Percentage of Players','Total Count']]
Gender_Demographics.sort_values('Total Count', ascending = False)
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
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>81.0</td>
      <td>465</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>17.0</td>
      <td>100</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>1.0</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



### Purchasing Analysis (Gender)



```python
Purchasing_analysis_gender = pd.DataFrame(Heroes_original_df.groupby(['Gender']).SN.nunique())
Purchasing_analysis_gender.columns = ['Purchase Count']
Purchasing_analysis_gender['Average Purchase Price'] = Heroes_original_df.groupby(['Gender']).Price.mean()
Purchasing_analysis_gender['Total Purchase Price'] = Heroes_original_df.groupby(['Gender']).Price.sum()
Purchasing_analysis_gender['Normalized Totals'] = Purchasing_analysis_gender['Total Purchase Price'] / Purchasing_analysis_gender['Purchase Count']
Purchasing_analysis_gender['Average Purchase Price'] = Purchasing_analysis_gender['Average Purchase Price'].map("${:.2f}".format)
Purchasing_analysis_gender['Total Purchase Price'] = Purchasing_analysis_gender['Total Purchase Price'].map("${:.2f}".format)
Purchasing_analysis_gender['Normalized Totals'] = Purchasing_analysis_gender['Normalized Totals'].map("${:.2f}".format)
Purchasing_analysis_gender
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Price</th>
      <th>Normalized Totals</th>
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
      <td>100</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>$3.83</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>465</td>
      <td>$2.95</td>
      <td>$1867.68</td>
      <td>$4.02</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>8</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>$4.47</td>
    </tr>
  </tbody>
</table>
</div>



### Age Demographics


```python
ranges = [ (0,10),(10,15), (15, 20), (20, 25),(25,30),(30,35),(35,40) ]
Age_ranges = ['<10','10-14','15-19','20-24','25-29','30-34','35-39','40+']
Age_ranges_count = []
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'] < 10].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(10,15))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(15,20))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(20,25))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(25,30))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(30,35))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(35,40))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'] >= 40].SN.nunique())
Age_demographics = pd.DataFrame(list(zip(Age_ranges_count)),index=Age_ranges)
Age_demographics.index.name = 'Age Group'
Age_demographics.columns = ['Total Count']
Age_demographics['Percentage Of Players'] = round(((Age_demographics['Total Count'] / Heroes_original_df['SN'].nunique()) * 100),2)
Age_demographics = Age_demographics[['Percentage Of Players','Total Count']]
Age_demographics
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
      <th>Percentage Of Players</th>
      <th>Total Count</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>3.32</td>
      <td>19</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>4.01</td>
      <td>23</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>17.45</td>
      <td>100</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>45.20</td>
      <td>259</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>15.18</td>
      <td>87</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>8.20</td>
      <td>47</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>4.71</td>
      <td>27</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>1.92</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>



### Purchasing Analysis (Age)


```python
Age_ranges_mean = []
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'] < 10].Price.mean())
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(10,15))].Price.mean())
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(15,20))].Price.mean())
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(20,25))].Price.mean())
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(25,30))].Price.mean())
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(30,35))].Price.mean())
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(35,40))].Price.mean())
Age_ranges_mean.append(Heroes_original_df.loc[Heroes_original_df['Age'] >= 40].Price.mean())

Age_ranges_sum = []
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'] < 10].Price.sum())
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(10,15))].Price.sum())
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(15,20))].Price.sum())
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(20,25))].Price.sum())
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(25,30))].Price.sum())
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(30,35))].Price.sum())
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(35,40))].Price.sum())
Age_ranges_sum.append(Heroes_original_df.loc[Heroes_original_df['Age'] >= 40].Price.sum())

Age_ranges_count = []
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'] < 10].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(10,15))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(15,20))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(20,25))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(25,30))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(30,35))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(35,40))].SN.nunique())
Age_ranges_count.append(Heroes_original_df.loc[Heroes_original_df['Age'] >= 40].SN.nunique())

User_count = []
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'] < 10].SN.count())
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(10,15))].SN.count())
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(15,20))].SN.count())
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(20,25))].SN.count())
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(25,30))].SN.count())
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(30,35))].SN.count())
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'].isin(range(35,40))].SN.count())
User_count.append(Heroes_original_df.loc[Heroes_original_df['Age'] >= 40].SN.count())

Purchasing_analysis = pd.DataFrame({'Age Group': Age_ranges,
                    'Purchase Count': Age_ranges_count,
                    'Average Purchase Price': Age_ranges_mean,
                    'Total Purchase Value': Age_ranges_sum,
                    'User Count': User_count }).set_index('Age Group')

Purchasing_analysis['Normalized Totals'] = Purchasing_analysis['Total Purchase Value'] / Purchasing_analysis['Purchase Count']
Purchasing_analysis = Purchasing_analysis[['Purchase Count', 'Average Purchase Price', 'Total Purchase Value', 'Normalized Totals']]
Purchasing_analysis['Average Purchase Price'] = Purchasing_analysis['Average Purchase Price'].map('${:,.2f}'.format) 
Purchasing_analysis['Total Purchase Value'] = Purchasing_analysis['Total Purchase Value'].map('${:,.2f}'.format) 
Purchasing_analysis['Normalized Totals'] = Purchasing_analysis['Normalized Totals'].map('${:,.2f}'.format) 
Purchasing_analysis

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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Age Group</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>19</td>
      <td>$2.98</td>
      <td>$83.46</td>
      <td>$4.39</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>23</td>
      <td>$2.77</td>
      <td>$96.95</td>
      <td>$4.22</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>100</td>
      <td>$2.91</td>
      <td>$386.42</td>
      <td>$3.86</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>259</td>
      <td>$2.91</td>
      <td>$978.77</td>
      <td>$3.78</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>87</td>
      <td>$2.96</td>
      <td>$370.33</td>
      <td>$4.26</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>47</td>
      <td>$3.08</td>
      <td>$197.25</td>
      <td>$4.20</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>27</td>
      <td>$2.84</td>
      <td>$119.40</td>
      <td>$4.42</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>11</td>
      <td>$3.16</td>
      <td>$53.75</td>
      <td>$4.89</td>
    </tr>
  </tbody>
</table>
</div>



### Top Spenders


```python
Top_spenders = pd.DataFrame({'Total Purchase Value': Heroes_original_df.groupby('SN').Price.sum(),
                    'Average Purchase Price': Heroes_original_df.groupby('SN').Price.mean(),
                    'Purchase Count': Heroes_original_df.groupby('SN').Price.count()})
Top_spenders = Top_spenders[['Purchase Count','Average Purchase Price','Total Purchase Value']]
Top_spenders = Top_spenders.sort_values('Total Purchase Value', ascending=False).head()
Top_spenders['Average Purchase Price'] = Top_spenders['Average Purchase Price'].map('${:,.2f}'.format) 
Top_spenders['Total Purchase Value'] = Top_spenders['Total Purchase Value'].map('${:,.2f}'.format) 
Top_spenders
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
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
      <th>Undirrala66</th>
      <td>5</td>
      <td>$3.41</td>
      <td>$17.06</td>
    </tr>
    <tr>
      <th>Saedue76</th>
      <td>4</td>
      <td>$3.39</td>
      <td>$13.56</td>
    </tr>
    <tr>
      <th>Mindimnya67</th>
      <td>4</td>
      <td>$3.18</td>
      <td>$12.74</td>
    </tr>
    <tr>
      <th>Haellysu29</th>
      <td>3</td>
      <td>$4.24</td>
      <td>$12.73</td>
    </tr>
    <tr>
      <th>Eoda93</th>
      <td>3</td>
      <td>$3.86</td>
      <td>$11.58</td>
    </tr>
  </tbody>
</table>
</div>



### Most Popular items¶


```python
Most_popular_items = pd.DataFrame({'Purchase Count': Heroes_original_df.groupby(['Item ID','Item Name']).Price.count(),
                    'Item Price': Heroes_original_df.groupby(['Item ID','Item Name']).Price.mean(),
                    'Total Purchase Value': Heroes_original_df.groupby(['Item ID','Item Name']).Price.sum()})
Most_popular_items = Most_popular_items[['Purchase Count','Item Price','Total Purchase Value']]
Most_profitable_items = Most_popular_items
Most_popular_items = Most_popular_items.sort_values(['Purchase Count','Total Purchase Value'], ascending=False).head()
Most_popular_items['Item Price'] = Most_popular_items['Item Price'].map('${:,.2f}'.format) 
Most_popular_items['Total Purchase Value'] = Most_popular_items['Total Purchase Value'].map('${:,.2f}'.format) 
Most_popular_items
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
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
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
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>



### Most Profitable items


```python
Most_profitable_items = Most_profitable_items.sort_values(['Total Purchase Value','Purchase Count','Item Price'], ascending=False).head()
Most_profitable_items['Item Price'] = Most_profitable_items['Item Price'].map('${:,.2f}'.format) 
Most_profitable_items['Total Purchase Value'] = Most_profitable_items['Total Purchase Value'].map('${:,.2f}'.format) 
Most_profitable_items
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
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
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
      <th>34</th>
      <th>Retribution Axe</th>
      <td>9</td>
      <td>$4.14</td>
      <td>$37.26</td>
    </tr>
    <tr>
      <th>115</th>
      <th>Spectral Diamond Doomblade</th>
      <td>7</td>
      <td>$4.25</td>
      <td>$29.75</td>
    </tr>
    <tr>
      <th>32</th>
      <th>Orenmir</th>
      <td>6</td>
      <td>$4.95</td>
      <td>$29.70</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>6</td>
      <td>$4.87</td>
      <td>$29.22</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Splitter, Foe Of Subtlety</th>
      <td>8</td>
      <td>$3.61</td>
      <td>$28.88</td>
    </tr>
  </tbody>
</table>
</div>


