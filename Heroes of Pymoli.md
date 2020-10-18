```python
# Import Dependencies
import pandas as pd
```


```python
# File to Load
file_to_load = 'Resources/Pymoli.csv'
```


```python
# Read the file and store in a Pandas Data Frame
pymoli = pd.read_csv(file_to_load)
pymoli_df = pd.read_csv(file_to_load, encoding='utf-8')
pymoli_df.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Display the total number of players
player_count = len(pymoli_df['SN'].unique())
summary_df = pd.DataFrame({'Total Players': [player_count]})
summary_df
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
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchasing Analysis totals:
# Find number of unique items, average price, number of purchases, revenue
item_count = len(pymoli_df['Item Name'].unique())
avg_price = pymoli_df['Price'].mean()
purchase_tally = (pymoli_df['Purchase ID']).count()
revenue = (pymoli_df['Price']).sum()

# Display the summary data frame
summary2_df = pd.DataFrame({"Number of Unique Items": [item_count],
                           "Average Price": (avg_price),
                           "Number of Purchases": [purchase_tally],
                           "Revenue": [revenue]})
summary2_df["Average Price"] = summary2_df["Average Price"].map("${:,.2f}".format)
summary2_df["Revenue"] = summary2_df["Revenue"].map("${:,.2f}".format)
summary2_df
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
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>$3.05</td>
      <td>780</td>
      <td>$2,379.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Gender Demographics:
# Drop the duplicate SN from the list sorted by gender
combined_df = pymoli_df[['Gender', 'SN']].drop_duplicates()
combined_df
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
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Male</td>
      <td>Lisim78</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>Lisovynya38</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Male</td>
      <td>Ithergue48</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Male</td>
      <td>Chamassasya86</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Male</td>
      <td>Iskosia90</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>773</th>
      <td>Male</td>
      <td>Hala31</td>
    </tr>
    <tr>
      <th>774</th>
      <td>Male</td>
      <td>Jiskjask80</td>
    </tr>
    <tr>
      <th>775</th>
      <td>Female</td>
      <td>Aethedru70</td>
    </tr>
    <tr>
      <th>777</th>
      <td>Male</td>
      <td>Yathecal72</td>
    </tr>
    <tr>
      <th>778</th>
      <td>Male</td>
      <td>Sisur91</td>
    </tr>
  </tbody>
</table>
<p>576 rows × 2 columns</p>
</div>




```python
# Find the count of each gender category
count = combined_df['Gender'].value_counts()
```


```python
# Find the percent of each gender category
count_percent = combined_df['Gender'].value_counts(normalize=True).map("{:,.2%}".format)
```


```python
# Combine the count and percent onto one DataFrame
gender_df = pd.DataFrame({"Total Count": count, "Percentage of Players": count_percent})
gender_df
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
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Male</th>
      <td>484</td>
      <td>84.03%</td>
    </tr>
    <tr>
      <th>Female</th>
      <td>81</td>
      <td>14.06%</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>1.91%</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchasing analysis by Gender:
# First, sort by gender from the original DataFrame
gender_analysis = pymoli.groupby('Gender')

# Obtain purchase count, avg. purchase price, avg. purchase total per person by gender
purchase_count = gender_analysis['Purchase ID'].count().drop_duplicates()
avg_purchase_price = gender_analysis['Price'].mean()
total_purchase = gender_analysis['Price'].sum()
avg_price_ea = total_purchase/count

# Display the summary data frame
summary3_df = pd.DataFrame({"Purchase Count": purchase_count,
                           "Average Purchase Price": avg_purchase_price,
                           "Average Price Spent": avg_price_ea,
                           "Total Purchase per Gender": total_purchase})
# Correct your formatting!
summary3_df["Average Purchase Price"] = summary3_df["Average Purchase Price"].map("${:,.2f}".format)
summary3_df["Average Price Spent"] = summary3_df["Average Price Spent"].map("${:,.2f}".format)
summary3_df["Total Purchase per Gender"] = summary3_df["Total Purchase per Gender"].map("${:,.2f}".format)
summary3_df
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Average Price Spent</th>
      <th>Total Purchase per Gender</th>
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
      <td>113</td>
      <td>$3.20</td>
      <td>$4.47</td>
      <td>$361.94</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>652</td>
      <td>$3.02</td>
      <td>$4.07</td>
      <td>$1,967.64</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>15</td>
      <td>$3.35</td>
      <td>$4.56</td>
      <td>$50.19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Age Demographics:
# Establish bins for age and categorize the players using the age bins
bins = [0, 10, 14, 19, 24, 29, 34, 39, 200]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# Calc the numbers and percentages by age group
pymoli["Age Group"] = pd.cut(pymoli["Age"], bins, labels=group_names, include_lowest=True)

group_age = pymoli.groupby("Age Group")
total_age = group_age['SN'].nunique().drop_duplicates()
percent_age = total_age/player_count

# Create a summary data frame for the results
age_demo_df = pd.DataFrame({"Total Count": total_age, "Percentage of Players within Age Group": percent_age})

# Correct your formatting!
age_demo_df["Percentage of Players within Age Group"] = age_demo_df["Percentage of Players within Age Group"].map("{:,.2%}".format)
age_demo_df
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
      <th>Total Count</th>
      <th>Percentage of Players within Age Group</th>
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
      <td>24</td>
      <td>4.17%</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>15</td>
      <td>2.60%</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>107</td>
      <td>18.58%</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>258</td>
      <td>44.79%</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>77</td>
      <td>13.37%</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>52</td>
      <td>9.03%</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>31</td>
      <td>5.38%</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>12</td>
      <td>2.08%</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Purchasing Analysis by Age:
# Bin the purchase data df by age -- I used my previous binning
age_analysis = pymoli.groupby('Age Group')

# Run basic calcs to obtain puchase count, avg. pur price, avg. pur total per person, etc
purchase_count = age_analysis['Purchase ID'].count().drop_duplicates()
avg_purchase_price = age_analysis['Price'].mean()
total_purchase = age_analysis['Price'].sum()
avg_price_ea = total_purchase/purchase_count

# Create a summary data frame
summary4_df = pd.DataFrame({"Purchase Count": purchase_count,
                           "Average Purchase Price": avg_purchase_price,
                           "Average Price Spent": avg_price_ea,
                           "Total Purchase per Age": total_purchase})

# Correct your formatting!
summary4_df["Average Purchase Price"] = summary4_df["Average Purchase Price"].map("${:,.2f}".format)
summary4_df["Average Price Spent"] = summary4_df["Average Price Spent"].map("${:,.2f}".format)
summary4_df["Total Purchase per Age"] = summary4_df["Total Purchase per Age"].map("${:,.2f}".format)
summary4_df
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
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Average Price Spent</th>
      <th>Total Purchase per Age</th>
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
      <td>32</td>
      <td>$3.40</td>
      <td>$3.40</td>
      <td>$108.96</td>
    </tr>
    <tr>
      <th>10-14</th>
      <td>19</td>
      <td>$2.68</td>
      <td>$2.68</td>
      <td>$50.95</td>
    </tr>
    <tr>
      <th>15-19</th>
      <td>136</td>
      <td>$3.04</td>
      <td>$3.04</td>
      <td>$412.89</td>
    </tr>
    <tr>
      <th>20-24</th>
      <td>365</td>
      <td>$3.05</td>
      <td>$3.05</td>
      <td>$1,114.06</td>
    </tr>
    <tr>
      <th>25-29</th>
      <td>101</td>
      <td>$2.90</td>
      <td>$2.90</td>
      <td>$293.00</td>
    </tr>
    <tr>
      <th>30-34</th>
      <td>73</td>
      <td>$2.93</td>
      <td>$2.93</td>
      <td>$214.00</td>
    </tr>
    <tr>
      <th>35-39</th>
      <td>41</td>
      <td>$3.60</td>
      <td>$3.60</td>
      <td>$147.67</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>13</td>
      <td>$2.94</td>
      <td>$2.94</td>
      <td>$38.24</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Top 5 Spenders:
# Group by the SN
spend_analysis = pymoli.groupby('SN')

# Run calcs to obtain purchase count, avg purchase price, total purchase value by SN
purchase_count = spend_analysis['Purchase ID'].count()
avg_purchase_price = spend_analysis['Price'].mean()
total_purchase = spend_analysis['Price'].sum()

# Create a summary data frame
summary5_df = pd.DataFrame({"Purchase Count": purchase_count,
                           "Average Purchase Price": avg_purchase_price,
                           "Total Purchase Value": total_purchase})

# Correct your formatting!
summary5_df = summary5_df.sort_values(["Total Purchase Value"], ascending=False).head()
summary5_df["Average Purchase Price"] = summary5_df["Average Purchase Price"].map("${:,.2f}".format)
summary5_df["Total Purchase Value"] = summary5_df["Total Purchase Value"].map("${:,.2f}".format)
summary5_df
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
      <th>Lisosia93</th>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <th>Idastidru52</th>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <th>Chamjask73</th>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <th>Iral74</th>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <th>Iskadarya95</th>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Most Popular items:
# Group by Item Name and Item ID
popular_analysis = pymoli.groupby(['Item ID', 'Item Name'])

# Run calculations for purchase count, item price, and total purchase value
purchase_count = popular_analysis['Purchase ID'].count()
purchase_price = popular_analysis['Price'].mean()
total_purchase = popular_analysis['Price'].sum()

# Create a summary data frame
summary6_df = pd.DataFrame({"Purchase Count": purchase_count,
                           "Item Price": purchase_price,
                           "Total Purchase Value": total_purchase})

# Correct your formatting!
summary6_df = summary6_df.sort_values(["Purchase Count"], ascending=False).head()
summary6_df["Total Purchase Value"] = summary6_df["Total Purchase Value"].map("${:,.2f}".format)
summary6_df["Item Price"] = summary6_df["Item Price"].map("${:,.2f}".format)
summary6_df
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
      <th>92</th>
      <th>Final Critic</th>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>132</th>
      <th>Persuasion</th>
      <td>9</td>
      <td>$3.22</td>
      <td>$28.99</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Extraction, Quickblade Of Trembling Hands</th>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Most profitable
# Again, group by Item Name and Item ID
profit_analysis = pymoli.groupby(['Item ID', 'Item Name'])

# Run calculations for purchase count, item price, and total purchase value
purchase_count = profit_analysis['Purchase ID'].count()
purchase_price = profit_analysis['Price'].mean()
total_purchase = profit_analysis['Price'].sum()

# Create a summary data frame
summary7_df = pd.DataFrame({"Purchase Count": purchase_count,
                           "Item Price": purchase_price,
                           "Total Purchase Value": total_purchase})

# Correct your formatting!
summary7_df = summary7_df.sort_values(["Total Purchase Value"], ascending=False).head()
summary7_df["Total Purchase Value"] = summary7_df["Total Purchase Value"].map("${:,.2f}".format)
summary7_df["Item Price"] = summary7_df["Item Price"].map("${:,.2f}".format)
summary7_df
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
      <th>92</th>
      <th>Final Critic</th>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <th>178</th>
      <th>Oathbreaker, Last Hope of the Breaking Storm</th>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <th>82</th>
      <th>Nirvana</th>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <th>145</th>
      <th>Fiery Glass Crusader</th>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Singed Scalpel</th>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>


