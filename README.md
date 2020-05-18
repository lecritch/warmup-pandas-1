
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
path = None
data = pd.read_csv(path)
```

**Ok,** let's print out the first 5 rows using the ```.head()``` method.


```python
# Your code here
```

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
path = None
pop = pd.read_csv(path)
```

**Cool Cool**, let's print out the first 5 rows using the ```.head()``` method.


```python
# Your Code here
```

Let's remove the ```Unnamed: 0``` column.


```python
pop.drop('Unnamed: 0', axis = 1, inplace = True)
```

We need to merge our two datasets. 

**When merging** datasets, it's important to check the length of our datasets before and after merging to make sure we are not losing too much data.

<u>In the cell below:</u>
1. Set the variable ```length_before_merge``` to the length of our ```data``` dataframe using python's built in ```len``` function


```python
# Your code here
length_before_merge = None


# Run Code below without change
string = '''<u>Length before merge:</u> **{}**'''.format(length_before_merge)
markdown(string)
```


<u>Length before merge:</u> **None**


*Merge Time*


<u>In the cell below:</u>
1. [Merge](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.merge.html) the two dataframes on the ```Municipality``` column.
    - Save the merged dataframe as the variable ```df```


```python
# Your code here

```

Now we need to check the length of our dataframe to make sure we didn't lose data! 

<u>In the cell below:</u>
1. Set the ```length_after_merge``` variable to the length of ```df```.


```python
# Your code here
length_after_merge = None


# Run Code below without change
string = '''<u>Length after merge:</u> **{}**'''.format(length_after_merge,)
markdown(string)
```


<u>Length after merge:</u> **None**


In the cell below, set the Municipality column as the index using the ```.set_index()``` method.


```python
# Your code here

```

Let's sort our index alphabetically using [this](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_index.html) method.


```python
# Your code here
```

To make things easier on ourselves, let's reformat our column names.

<u>In the cell below:</u>
1. Replace spaces with underscores for each column name
2. Lower each column name
>Bonus points if you do this via list comphrension 😃


```python
# Your code here

```

<center><i><h1>So much cleaning</h1></i></center>


![](https://media.giphy.com/media/3o7WIE14z2d66BJWJa/giphy.gif)

--------

Ok Ok, we're almost done formatting our data.

<u>In the cell below:</u> 
1. Print out the datatypes for each of our columns using the ```.info()``` method.



```python
# Your code here

```

Our ```population``` column contains commas which is causing the computer to interpret the column as a string.

<u>In the cell below:</u>
1. Remove the commas from the column using the ```.apply``` method
>**If your confused:** Find the answer relating to ```.apply()``` in this [Stack Overflow](https://stackoverflow.com/questions/56947333/how-to-remove-commas-from-all-the-column-in-pandas-at-once/56947424#56947424?newreg=3c19aff3bd5146a19f7787afedc243a2) thread.
2. Convert the column datatype to integer

    - Bonus points if you can do steps 1 & 2 with 1️⃣ line of code! 😻


```python
# Your code here

```

# Cleaning Complete!

<img src="https://media.giphy.com/media/hEZIaecxpR78I/giphy.gif" width=400/>

#### Ok Ok! 

Let's create a column that shows the number of gambling terminals per capita!

<u>In the cell below:</u>
1. Create a new column called ```terminals_percapita``` by dividing ```terminal_count``` by ```population```


```python
# Your code here

```

Now let's identify which communities have the highest number of gambling devices per capita. 


<u>In the cell(s) below:</u>
1. [Sort](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.sort_values.html) the dataframe according to the ```terminals_percapita``` column.
2. Identify the 10 communities with the highest number of gambling machines per capita.
3. Save those 10 community names in a list called ```highest_machines_percapita```


```python
# Your code here

```

Run the cell below to see if you identified the correct Municipalities!


```python
run_test(highest_machines_percapita, 'highest_machines_percapita')
```




    'Hey, you did it.  Good job.'



**Next,** let's figure out how much money players lost for each municipality.

<u>In the cell below:</u>
1. Create a new column called ```amount_lost``` that is the difference between the ```amount_played``` and ```amount_won``` columns


```python
# Your code here

```

<u>In the cell below:</u>
1. Save the mean of the ```amount_loss``` column as the variable ```average_loss```.
2. Using numpy, round the ```average_loss``` variable to 2 decimal points.
    - Save the rounded number as the variable ```average_loss_rounded```


```python
# Your code here

average_loss = None
average_loss_rounded = None
```

Let's zoom in on this new loss data. 

<u>In the cell below:</u>
1. Create a new column called ```loss_percapita``` that is the division of the ```amount_lost``` and ```population```


```python
# Your code here
```

<u>In the cell below</u>
1. Sort the dataframe by ```loss_percapita``` and save the 10 communities with the highest loss per capita to a list called ```highest_loss_percapita```


```python
# Your code here
highest_loss_percapita = None
```

Run the cell below to see if you idenitified the correct municipalities!


```python
run_test(highest_loss_percapita, 'highest_loss_percapita')
```




    'Hey, you did it.  Good job.'



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
# Your code here

```

Run the cell below to see if you identified the correct averages!


```python
high_result = run_test(high_loss_average_population, 'high_loss_average_population')
low_result = run_test(low_loss_average_population, 'low_loss_average_population')

print(f'high loss test result: {high_result}')
print
print(f'low loss test result: {low_result}')
```


```python

```
