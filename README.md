
# Video Gambling Data and Pandas 🧐
<img src="https://media.tegna-media.com/assets/WQAD/images/01c4abef-ca79-4b9b-b3f7-2ad2e856b34b/01c4abef-ca79-4b9b-b3f7-2ad2e856b34b_750x422.jpg" width="460"/>

### *Video gambling, in Illinois, was legalized in 2012.*

>Since then, it has become a boon for local bars, restaurants, and communities with declining tax revenue, but comes with public health concerns of gambling addition.
Because of this Video Gambling is a frequent issue voted on by municipal governments in Illinois. 

>Video Gambling is closely monitored by the [Illinois Gaming Board](https://www.igb.illinois.gov/) and has been the subject of much reporting by local news agencies.

**Let's use our skills with Pandas to investigate this topic.**


```python

# Run this cell unchanged

# if you get a long error msg:
# - restart the kernal 
# (click the circular arrow icon right below the tab for the notebook)
# - make a new cell above this one and import pandas as pd there

import pandas as pd
from IPython.display import display, Markdown

def markdown(text):
    display(Markdown(text))
    
#used for tests
from test_background import pkl_dump, test_dict, run_test
import numpy as np
```

**Our data is located** within the ```data``` folder of this repo.

It is titled ```2019-il-vgambling.csv```

<u>In the cell below:</u> 
1. Set the ```path``` variable to the path ```./data/2019-il-vgambling.csv```. 
    - (reverse the slashes if you're on Windows)
2. Run the cell to import our dataset.


```python
path = './data/2019-il-vgambling.csv'
data = pd.read_csv(path)

data.head()
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
      <th>Municipality</th>
      <th>Establishment Count</th>
      <th>Terminal Count</th>
      <th>Amount Played</th>
      <th>Amount Won</th>
      <th>Nti Tax</th>
      <th>State Share</th>
      <th>Municipality Share</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Oregon</td>
      <td>13</td>
      <td>58</td>
      <td>30182428.57</td>
      <td>27583763.32</td>
      <td>818444.23</td>
      <td>688505.69</td>
      <td>129938.54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Oakwood Hills</td>
      <td>1</td>
      <td>4</td>
      <td>216669.74</td>
      <td>199790.23</td>
      <td>5281.38</td>
      <td>4433.69</td>
      <td>847.69</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Merrionette Park</td>
      <td>4</td>
      <td>17</td>
      <td>26567816.26</td>
      <td>24324921.75</td>
      <td>706616.85</td>
      <td>594470.85</td>
      <td>112146.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ashkum</td>
      <td>2</td>
      <td>8</td>
      <td>2289711.66</td>
      <td>2113123.06</td>
      <td>55674.55</td>
      <td>46845.11</td>
      <td>8829.44</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Grandview</td>
      <td>5</td>
      <td>25</td>
      <td>13713301.51</td>
      <td>12475853.83</td>
      <td>390048.01</td>
      <td>328175.50</td>
      <td>61872.51</td>
    </tr>
  </tbody>
</table>
</div>



**Ok,** let's print out the first 5 rows using the ```.head()``` method.


```python
data.head()
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
      <th>Municipality</th>
      <th>Establishment Count</th>
      <th>Terminal Count</th>
      <th>Amount Played</th>
      <th>Amount Won</th>
      <th>Nti Tax</th>
      <th>State Share</th>
      <th>Municipality Share</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Oregon</td>
      <td>13</td>
      <td>58</td>
      <td>30182428.57</td>
      <td>27583763.32</td>
      <td>818444.23</td>
      <td>688505.69</td>
      <td>129938.54</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Oakwood Hills</td>
      <td>1</td>
      <td>4</td>
      <td>216669.74</td>
      <td>199790.23</td>
      <td>5281.38</td>
      <td>4433.69</td>
      <td>847.69</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Merrionette Park</td>
      <td>4</td>
      <td>17</td>
      <td>26567816.26</td>
      <td>24324921.75</td>
      <td>706616.85</td>
      <td>594470.85</td>
      <td>112146.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ashkum</td>
      <td>2</td>
      <td>8</td>
      <td>2289711.66</td>
      <td>2113123.06</td>
      <td>55674.55</td>
      <td>46845.11</td>
      <td>8829.44</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Grandview</td>
      <td>5</td>
      <td>25</td>
      <td>13713301.51</td>
      <td>12475853.83</td>
      <td>390048.01</td>
      <td>328175.50</td>
      <td>61872.51</td>
    </tr>
  </tbody>
</table>
</div>



<center><u><h3>Column Descriptions</h3><u></center>


| Column Name         	| Description                                                                                                                                                               	|
|:---------------------	|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
| Municipality        	| The community's name                                                                                                                                                      	|
| Establishment Count 	| Number of businesses with video gambling licenses                                                                                                                         	|
| Terminal Count      	| Number of video gambling machines in the community.                                                                                                                       	|
| Amount Played       	| Total amount spent on video gambling by players.                                                                                                                          	|
| Amount Won          	| Total amount won by players                                                                                                                                               	|
| Nti Tax             	| The Net Terminal Income Tax Rate <br>is 30% of the Net Terminal Income. <br>The funds are divided between<br>the State of Illinois and local <br>governmental organizations. 	|
| State Share         	| Total revenue received by the State Government                                                                                                                            	|
| Municipality Share  	| Total revenue received by the Municipality                                                                                                                                	|

**When examining data at the municipal level,** it is common to <i><u>scale</u></i> our data according to the municipality's population. 
>This is often referred to as scaling our data *per capita*. 

To do this let's import some population data for Illinois Municipalities.

In the cell below: 
1. Set the ```path``` variable to the path for the ```population.csv``` file within the ```data``` folder.
2. Run the cell to import our population data.


```python
path = './data/population.csv'
pop = pd.read_csv(path)

pop.head()
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
      <th>Municipality</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Champaign</td>
      <td>86,791</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Carbondale</td>
      <td>25,846</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Prairie Grove</td>
      <td>1,826</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Macomb</td>
      <td>18,118</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Brimfield</td>
      <td>965</td>
    </tr>
  </tbody>
</table>
</div>



**Cool Cool**, let's print out the first 5 rows using the ```.head()``` method.


```python
pop.head()
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
      <th>Municipality</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Champaign</td>
      <td>86,791</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Carbondale</td>
      <td>25,846</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Prairie Grove</td>
      <td>1,826</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Macomb</td>
      <td>18,118</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Brimfield</td>
      <td>965</td>
    </tr>
  </tbody>
</table>
</div>



Let's remove the ```Unnamed: 0``` column.


```python

pop.drop('Unnamed: 0', axis = 1, inplace = True)
pop.head()
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
      <th>Municipality</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Champaign</td>
      <td>86,791</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Carbondale</td>
      <td>25,846</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Prairie Grove</td>
      <td>1,826</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Macomb</td>
      <td>18,118</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Brimfield</td>
      <td>965</td>
    </tr>
  </tbody>
</table>
</div>



We need to merge our two datasets. 

**When merging** datasets, it's important to check the length of our datasets before and after merging to make sure we are not losing too much data.

<u>In the cell below:</u>
1. Set the variable ```length_before_merge``` to the length of our ```df``` dataframe using python's built in ```len``` function


```python
length_before_merge = len(data)



# Run Code below without change
string = '''<u>Length before merge:</u> **{}**'''.format(length_before_merge)
markdown(string)
```


<u>Length before merge:</u> **835**


*Merge Time*


<u>In the cell below:</u>
1. [Merge](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html) the two dataframes on the ```Municipality``` column.
    - Save the merged dataframe as the variable ```df```


```python
df = pd.merge(data, pop, on = 'Municipality')
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
      <th>Municipality</th>
      <th>Establishment Count</th>
      <th>Terminal Count</th>
      <th>Amount Played</th>
      <th>Amount Won</th>
      <th>Nti Tax</th>
      <th>State Share</th>
      <th>Municipality Share</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Oregon</td>
      <td>13</td>
      <td>58</td>
      <td>30182428.57</td>
      <td>27583763.32</td>
      <td>818444.23</td>
      <td>688505.69</td>
      <td>129938.54</td>
      <td>3,683</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Oakwood Hills</td>
      <td>1</td>
      <td>4</td>
      <td>216669.74</td>
      <td>199790.23</td>
      <td>5281.38</td>
      <td>4433.69</td>
      <td>847.69</td>
      <td>2,245</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Merrionette Park</td>
      <td>4</td>
      <td>17</td>
      <td>26567816.26</td>
      <td>24324921.75</td>
      <td>706616.85</td>
      <td>594470.85</td>
      <td>112146.00</td>
      <td>2,163</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ashkum</td>
      <td>2</td>
      <td>8</td>
      <td>2289711.66</td>
      <td>2113123.06</td>
      <td>55674.55</td>
      <td>46845.11</td>
      <td>8829.44</td>
      <td>800</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Grandview</td>
      <td>5</td>
      <td>25</td>
      <td>13713301.51</td>
      <td>12475853.83</td>
      <td>390048.01</td>
      <td>328175.50</td>
      <td>61872.51</td>
      <td>1,453</td>
    </tr>
  </tbody>
</table>
</div>



Now we need to check the length of our dataframe to make sure we didn't lose data! 

<u>In the cell below:</u>
1. Set the ```length_after_merge``` variable to the length of ```df```.


```python
length_after_merge = len(df)

# Run Code below without change
string = '''<u>Length after merge:</u> **{}**'''.format(length_after_merge)
markdown(string)
```


<u>Length after merge:</u> **835**


In the cell below, set the Municipality column as the index using the ```.set_index()``` method.


```python
df.set_index('Municipality', drop=True, inplace = True)
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
      <th>Establishment Count</th>
      <th>Terminal Count</th>
      <th>Amount Played</th>
      <th>Amount Won</th>
      <th>Nti Tax</th>
      <th>State Share</th>
      <th>Municipality Share</th>
      <th>Population</th>
    </tr>
    <tr>
      <th>Municipality</th>
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
      <th>Oregon</th>
      <td>13</td>
      <td>58</td>
      <td>30182428.57</td>
      <td>27583763.32</td>
      <td>818444.23</td>
      <td>688505.69</td>
      <td>129938.54</td>
      <td>3,683</td>
    </tr>
    <tr>
      <th>Oakwood Hills</th>
      <td>1</td>
      <td>4</td>
      <td>216669.74</td>
      <td>199790.23</td>
      <td>5281.38</td>
      <td>4433.69</td>
      <td>847.69</td>
      <td>2,245</td>
    </tr>
    <tr>
      <th>Merrionette Park</th>
      <td>4</td>
      <td>17</td>
      <td>26567816.26</td>
      <td>24324921.75</td>
      <td>706616.85</td>
      <td>594470.85</td>
      <td>112146.00</td>
      <td>2,163</td>
    </tr>
    <tr>
      <th>Ashkum</th>
      <td>2</td>
      <td>8</td>
      <td>2289711.66</td>
      <td>2113123.06</td>
      <td>55674.55</td>
      <td>46845.11</td>
      <td>8829.44</td>
      <td>800</td>
    </tr>
    <tr>
      <th>Grandview</th>
      <td>5</td>
      <td>25</td>
      <td>13713301.51</td>
      <td>12475853.83</td>
      <td>390048.01</td>
      <td>328175.50</td>
      <td>61872.51</td>
      <td>1,453</td>
    </tr>
  </tbody>
</table>
</div>



Let's sort our index alphabetically using [this](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_index.html) method.


```python
df.sort_index(inplace = True)
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
      <th>Establishment Count</th>
      <th>Terminal Count</th>
      <th>Amount Played</th>
      <th>Amount Won</th>
      <th>Nti Tax</th>
      <th>State Share</th>
      <th>Municipality Share</th>
      <th>Population</th>
    </tr>
    <tr>
      <th>Municipality</th>
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
      <th>Abingdon</th>
      <td>4</td>
      <td>16</td>
      <td>6492446.76</td>
      <td>5968296.97</td>
      <td>165040.02</td>
      <td>138832.38</td>
      <td>26207.64</td>
      <td>3,452</td>
    </tr>
    <tr>
      <th>Addieville</th>
      <td>1</td>
      <td>5</td>
      <td>939917.34</td>
      <td>860520.60</td>
      <td>25020.09</td>
      <td>21050.20</td>
      <td>3969.89</td>
      <td>344</td>
    </tr>
    <tr>
      <th>Addison</th>
      <td>23</td>
      <td>111</td>
      <td>88623932.26</td>
      <td>80762581.15</td>
      <td>2476573.63</td>
      <td>2083474.53</td>
      <td>393099.10</td>
      <td>37,089</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>2</td>
      <td>7</td>
      <td>2030709.60</td>
      <td>1855397.39</td>
      <td>55473.53</td>
      <td>46707.84</td>
      <td>8765.69</td>
      <td>979</td>
    </tr>
    <tr>
      <th>Albers</th>
      <td>1</td>
      <td>4</td>
      <td>1546280.29</td>
      <td>1419896.70</td>
      <td>39710.50</td>
      <td>33391.29</td>
      <td>6319.21</td>
      <td>1,184</td>
    </tr>
  </tbody>
</table>
</div>



To make things easier on ourselves, let's reformat our column names.

<u>In the cell below:</u>
1. Replace spaces with underscores for each column name
2. Lower each column name
>Bonus points if you do this via list comphrension 😃


```python
df.columns = [x.lower().replace(' ', '_') for x in df.columns]
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
      <th>establishment_count</th>
      <th>terminal_count</th>
      <th>amount_played</th>
      <th>amount_won</th>
      <th>nti_tax</th>
      <th>state_share</th>
      <th>municipality_share</th>
      <th>population</th>
    </tr>
    <tr>
      <th>Municipality</th>
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
      <th>Abingdon</th>
      <td>4</td>
      <td>16</td>
      <td>6492446.76</td>
      <td>5968296.97</td>
      <td>165040.02</td>
      <td>138832.38</td>
      <td>26207.64</td>
      <td>3,452</td>
    </tr>
    <tr>
      <th>Addieville</th>
      <td>1</td>
      <td>5</td>
      <td>939917.34</td>
      <td>860520.60</td>
      <td>25020.09</td>
      <td>21050.20</td>
      <td>3969.89</td>
      <td>344</td>
    </tr>
    <tr>
      <th>Addison</th>
      <td>23</td>
      <td>111</td>
      <td>88623932.26</td>
      <td>80762581.15</td>
      <td>2476573.63</td>
      <td>2083474.53</td>
      <td>393099.10</td>
      <td>37,089</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>2</td>
      <td>7</td>
      <td>2030709.60</td>
      <td>1855397.39</td>
      <td>55473.53</td>
      <td>46707.84</td>
      <td>8765.69</td>
      <td>979</td>
    </tr>
    <tr>
      <th>Albers</th>
      <td>1</td>
      <td>4</td>
      <td>1546280.29</td>
      <td>1419896.70</td>
      <td>39710.50</td>
      <td>33391.29</td>
      <td>6319.21</td>
      <td>1,184</td>
    </tr>
  </tbody>
</table>
</div>



<center><i><h1>So much cleaning</h1></i></center>


![](https://media.giphy.com/media/3o7WIE14z2d66BJWJa/giphy.gif)

--------

Ok Ok, we're almost done formatting our data.

<u>In the cell below:</u> 
1. Print out the datatypes for each of our columns using the ```.info()``` method.



```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Index: 835 entries, Abingdon to Zion
    Data columns (total 8 columns):
    establishment_count    835 non-null int64
    terminal_count         835 non-null int64
    amount_played          835 non-null float64
    amount_won             835 non-null float64
    nti_tax                835 non-null float64
    state_share            835 non-null float64
    municipality_share     835 non-null float64
    population             835 non-null object
    dtypes: float64(5), int64(2), object(1)
    memory usage: 58.7+ KB


Our ```population``` column contains commas which is causing the computer to interpret the column as a string.

<u>In the cell below:</u>
1. Remove the commas from the column using the ```.apply``` method
>**If your confused:** Find the answer relating to ```.apply()``` in this [Stack Overflow](https://stackoverflow.com/questions/56947333/how-to-remove-commas-from-all-the-column-in-pandas-at-once/56947424#56947424?newreg=3c19aff3bd5146a19f7787afedc243a2) thread.
2. Convert the column datatype to integer

    - Bonus points if you can do steps 1 & 2 with 1️⃣ line of code! 😻


```python
df.population = df.population.apply(lambda x: int(x.replace(',', '')))
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
      <th>establishment_count</th>
      <th>terminal_count</th>
      <th>amount_played</th>
      <th>amount_won</th>
      <th>nti_tax</th>
      <th>state_share</th>
      <th>municipality_share</th>
      <th>population</th>
    </tr>
    <tr>
      <th>Municipality</th>
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
      <th>Abingdon</th>
      <td>4</td>
      <td>16</td>
      <td>6492446.76</td>
      <td>5968296.97</td>
      <td>165040.02</td>
      <td>138832.38</td>
      <td>26207.64</td>
      <td>3452</td>
    </tr>
    <tr>
      <th>Addieville</th>
      <td>1</td>
      <td>5</td>
      <td>939917.34</td>
      <td>860520.60</td>
      <td>25020.09</td>
      <td>21050.20</td>
      <td>3969.89</td>
      <td>344</td>
    </tr>
    <tr>
      <th>Addison</th>
      <td>23</td>
      <td>111</td>
      <td>88623932.26</td>
      <td>80762581.15</td>
      <td>2476573.63</td>
      <td>2083474.53</td>
      <td>393099.10</td>
      <td>37089</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>2</td>
      <td>7</td>
      <td>2030709.60</td>
      <td>1855397.39</td>
      <td>55473.53</td>
      <td>46707.84</td>
      <td>8765.69</td>
      <td>979</td>
    </tr>
    <tr>
      <th>Albers</th>
      <td>1</td>
      <td>4</td>
      <td>1546280.29</td>
      <td>1419896.70</td>
      <td>39710.50</td>
      <td>33391.29</td>
      <td>6319.21</td>
      <td>1184</td>
    </tr>
  </tbody>
</table>
</div>



# Cleaning Complete!

<img src="https://media.giphy.com/media/hEZIaecxpR78I/giphy.gif" width=400/>

#### Ok Ok! 

Let's create a column that shows the number of gambling terminals per capita!

<u>In the cell below:</u>
1. Create a new column called ```terminals_percapita``` by dividing ```terminal_count``` by ```population```


```python
df['terminals_percapita'] = df.terminal_count/df.population
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
      <th>establishment_count</th>
      <th>terminal_count</th>
      <th>amount_played</th>
      <th>amount_won</th>
      <th>nti_tax</th>
      <th>state_share</th>
      <th>municipality_share</th>
      <th>population</th>
      <th>terminals_percapita</th>
    </tr>
    <tr>
      <th>Municipality</th>
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
      <th>Abingdon</th>
      <td>4</td>
      <td>16</td>
      <td>6492446.76</td>
      <td>5968296.97</td>
      <td>165040.02</td>
      <td>138832.38</td>
      <td>26207.64</td>
      <td>3452</td>
      <td>0.004635</td>
    </tr>
    <tr>
      <th>Addieville</th>
      <td>1</td>
      <td>5</td>
      <td>939917.34</td>
      <td>860520.60</td>
      <td>25020.09</td>
      <td>21050.20</td>
      <td>3969.89</td>
      <td>344</td>
      <td>0.014535</td>
    </tr>
    <tr>
      <th>Addison</th>
      <td>23</td>
      <td>111</td>
      <td>88623932.26</td>
      <td>80762581.15</td>
      <td>2476573.63</td>
      <td>2083474.53</td>
      <td>393099.10</td>
      <td>37089</td>
      <td>0.002993</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>2</td>
      <td>7</td>
      <td>2030709.60</td>
      <td>1855397.39</td>
      <td>55473.53</td>
      <td>46707.84</td>
      <td>8765.69</td>
      <td>979</td>
      <td>0.007150</td>
    </tr>
    <tr>
      <th>Albers</th>
      <td>1</td>
      <td>4</td>
      <td>1546280.29</td>
      <td>1419896.70</td>
      <td>39710.50</td>
      <td>33391.29</td>
      <td>6319.21</td>
      <td>1184</td>
      <td>0.003378</td>
    </tr>
  </tbody>
</table>
</div>



Now let's identify which communities have the highest number of gambling devices per capita. 


<u>In the cell(s) below:</u>
1. [Sort](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html) the dataframe according to the ```terminals_percapita``` column.
2. Identify the 10 communities with the highest number of gambling machines per capita.
3. Save those 10 community names in a list called ```highest_machines_percapita```


```python

highest_machines_percapita = \
    df.sort_values \
    (by='terminals_percapita', 
     ascending=False)\
    .head(10)\
    .index

highest_machines_percapita = list(highest_machines_percapita)
highest_machines_percapita

#used for testing
pkl_dump([(
    highest_machines_percapita,
    'highest_machines_percapita'
)])
```

    can"t dump, highest_machines_percapita already exists


Run the cell below to see if you identified the correct Municipalities!


```python

run_test(highest_machines_percapita, 'highest_machines_percapita')
```




    'Hey, you did it.  Good job.'



**Next,** let's figure out how much money players lost for each municipality.

<u>In the cell below:</u>
1. Create a new column called ```amount_lost``` that is the difference between the ```amount_played``` and ```amount_won``` columns


```python
df['amount_lost'] = df.amount_played - df.amount_won
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
      <th>establishment_count</th>
      <th>terminal_count</th>
      <th>amount_played</th>
      <th>amount_won</th>
      <th>nti_tax</th>
      <th>state_share</th>
      <th>municipality_share</th>
      <th>population</th>
      <th>terminals_percapita</th>
      <th>amount_lost</th>
    </tr>
    <tr>
      <th>Municipality</th>
      <th></th>
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
      <th>Abingdon</th>
      <td>4</td>
      <td>16</td>
      <td>6492446.76</td>
      <td>5968296.97</td>
      <td>165040.02</td>
      <td>138832.38</td>
      <td>26207.64</td>
      <td>3452</td>
      <td>0.004635</td>
      <td>524149.79</td>
    </tr>
    <tr>
      <th>Addieville</th>
      <td>1</td>
      <td>5</td>
      <td>939917.34</td>
      <td>860520.60</td>
      <td>25020.09</td>
      <td>21050.20</td>
      <td>3969.89</td>
      <td>344</td>
      <td>0.014535</td>
      <td>79396.74</td>
    </tr>
    <tr>
      <th>Addison</th>
      <td>23</td>
      <td>111</td>
      <td>88623932.26</td>
      <td>80762581.15</td>
      <td>2476573.63</td>
      <td>2083474.53</td>
      <td>393099.10</td>
      <td>37089</td>
      <td>0.002993</td>
      <td>7861351.11</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>2</td>
      <td>7</td>
      <td>2030709.60</td>
      <td>1855397.39</td>
      <td>55473.53</td>
      <td>46707.84</td>
      <td>8765.69</td>
      <td>979</td>
      <td>0.007150</td>
      <td>175312.21</td>
    </tr>
    <tr>
      <th>Albers</th>
      <td>1</td>
      <td>4</td>
      <td>1546280.29</td>
      <td>1419896.70</td>
      <td>39710.50</td>
      <td>33391.29</td>
      <td>6319.21</td>
      <td>1184</td>
      <td>0.003378</td>
      <td>126383.59</td>
    </tr>
  </tbody>
</table>
</div>



<u>In the cell below:</u>
1. Save the mean of the ```amount_loss``` column as the variable ```average_loss```.
2. Using numpy, round the ```average_loss``` variable to 2 decimal points.
    - Save the rounded number as the variable ```average_loss_rounded```


```python

average_loss = df.amount_lost.mean()
average_loss_rounded = np.round(average_loss, decimals=2)
```

Let's zoom in on this new loss data. 

<u>In the cell below:</u>
1. Create a new column called ```loss_percapita``` that is the division of the ```amount_lost``` and ```population```


```python
df['loss_percapita'] = df.amount_lost / df.population
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
      <th>establishment_count</th>
      <th>terminal_count</th>
      <th>amount_played</th>
      <th>amount_won</th>
      <th>nti_tax</th>
      <th>state_share</th>
      <th>municipality_share</th>
      <th>population</th>
      <th>terminals_percapita</th>
      <th>amount_lost</th>
      <th>loss_percapita</th>
    </tr>
    <tr>
      <th>Municipality</th>
      <th></th>
      <th></th>
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
      <th>Abingdon</th>
      <td>4</td>
      <td>16</td>
      <td>6492446.76</td>
      <td>5968296.97</td>
      <td>165040.02</td>
      <td>138832.38</td>
      <td>26207.64</td>
      <td>3452</td>
      <td>0.004635</td>
      <td>524149.79</td>
      <td>151.839452</td>
    </tr>
    <tr>
      <th>Addieville</th>
      <td>1</td>
      <td>5</td>
      <td>939917.34</td>
      <td>860520.60</td>
      <td>25020.09</td>
      <td>21050.20</td>
      <td>3969.89</td>
      <td>344</td>
      <td>0.014535</td>
      <td>79396.74</td>
      <td>230.804477</td>
    </tr>
    <tr>
      <th>Addison</th>
      <td>23</td>
      <td>111</td>
      <td>88623932.26</td>
      <td>80762581.15</td>
      <td>2476573.63</td>
      <td>2083474.53</td>
      <td>393099.10</td>
      <td>37089</td>
      <td>0.002993</td>
      <td>7861351.11</td>
      <td>211.959101</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>2</td>
      <td>7</td>
      <td>2030709.60</td>
      <td>1855397.39</td>
      <td>55473.53</td>
      <td>46707.84</td>
      <td>8765.69</td>
      <td>979</td>
      <td>0.007150</td>
      <td>175312.21</td>
      <td>179.072737</td>
    </tr>
    <tr>
      <th>Albers</th>
      <td>1</td>
      <td>4</td>
      <td>1546280.29</td>
      <td>1419896.70</td>
      <td>39710.50</td>
      <td>33391.29</td>
      <td>6319.21</td>
      <td>1184</td>
      <td>0.003378</td>
      <td>126383.59</td>
      <td>106.742897</td>
    </tr>
  </tbody>
</table>
</div>



<u>In the cell below</u>
1. Sort the dataframe by ```loss_percapita``` and save the 10 communities with the highest loss per capita to a list called ```highest_loss_percapita```


```python
highest_loss_percapita = list(
    df
    .sort_values(
        by='loss_percapita', 
        ascending = False
    )
    .head(10)
    .index
)

highest_loss_percapita

#used for tests
pkl_dump([(
    highest_loss_percapita,
    'highest_loss_percapita'
)])
```

    can"t dump, highest_loss_percapita already exists


Run the cell below to see if you idenitified the correct municipalities!


```python
run_test(highest_loss_percapita, 'highest_loss_percapita')
```

<u>In the cell below:</u>
1. Filter our dataframe to contain municipalities with a ```loss_percapita``` of 406 or greater. 
    - Save this filtered dataframe as ```high_loss_percapita```
2. Filter our dataframe to contain municipalities with a ```loss_percapita``` of 155 or less.
    - Save this filtered dataframe as ```low_loss_percapita```
3. Identify the mean population for the municipalities with a high per capita loss
    - Using numpy, round this data point to 2 decimals
    - Save this data point as the variable ```high_loss_average_population```

4. Identify the mean population for the municipalities with a low per capita loss.
    - Using numpy round this data point to 2 decimals
    - Save this data point as the variable ```low_loss_average_population```  


```python
high_loss_percapita = df[df.loss_percapita >= 406]
low_loss_percapita = df[df.loss_percapita <= 155]
high_loss_average_population = (
    np.round(
        high_loss_percapita
        .population
        .mean()
        , 2
    )
)

low_loss_average_population = (
    np.round(
        low_loss_percapita
        .population
        .mean()
        , 2)
)

low_loss_average_population

#used for tests
pkl_dump([
    (high_loss_average_population,
    'high_loss_average_population'
    ),
    (low_loss_average_population,
    'low_loss_average_population'
    )
])
```

    can"t dump, high_loss_average_population already exists


Run the cell below to see if you identified the correct averages!


```python
high_result = run_test(high_loss_average_population, 'high_loss_average_population')
low_result = run_test(low_loss_average_population, 'low_loss_average_population')

print(f'high loss test result: {high_result}')
print
print(f'low loss test result: {low_result}')
```

    high loss test result: Hey, you did it.  Good job.
    low loss test result: Hey, you did it.  Good job.

