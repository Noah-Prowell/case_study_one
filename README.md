# United States and United Kingdom Population Data from 1960-2016

## Goal:
To explore various changes in US and UK population data over the years 1960-2016.


## Our Raw Data



After reading in the raw data from Health Nutrition and Population Statistics, it was immediately apparent that we would have to do some transformation to get it into a workable form. As you can see, the rows were an index of numbers from 1 to ~90,000, and the columns are country names, years 1960-2016, and indicators.



![Image](https://imgur.com/kmSFYlx.png)

![Image](https://imgur.com/JSbVIxv.png)



The indicators (things like population size, death rate, etc.) was the data we actually cared about, so we needed to find a way to transform the dataframe to better represent that.

--- 

To do this, decided to focus in on the US and UK specifically, allowing us to sqeeze our indicators down to unique values with no duplicates. Then we made the indicators our columns, and ended up with a dataframe that makes much more sense. 

```
#UK dataframe
df_UK = df[df['Country Name'] == 'United Kingdom']
columns = df_UK.iloc[:,3]
df_UK = df_UK[[column for column in df_UK.columns if column not in ['Country Name', 'Country Code','Indicator Name','Indicator Code', 'Unnamed: 60']]].transpose()
df_UK.index = df_UK.index.astype(int)
df_UK.columns = columns
df_UK.index.name = 'Year'
```

 
![Image](https://imgur.com/HWzINGo.png)
 

Now, we had reduced our dataframe from a 90,000x60 dataframe, to two 345x60 dataframes; **MUCH** more manageable.

--- 

## Exploring our data

Exploring our data showed us that there were quite a lot indicators with little or no data. In order to find ones indicators that had good, workable data, we needed to be able to lookup our indicator codes by name. Here is the function we wrote to do that:

```
def get_indicator_code(ind_name=''):
    if len(ind_name) == 0:
        return set(df_US.loc["Indicator Name"])
    else:
        return df_US.columns[(df_US == ind_name).loc['Indicator Name']][0] 
```

So, after grabbing columns that had data we could work with, we made the following graphs!


**US v. UK Healthcare Expenditure**

![Image](https://i.imgur.com/XDmLiMD.png)

**US v. UK population growth**

![Image](https://i.imgur.com/k8rTEbW.png)

**US v. UK Death Rate**

![Image](https://i.imgur.com/UTs4r1C.png)

**US v. UK Birth Rate**

![Image](https://i.imgur.com/KQ8SqkT.png)

**Urban population as a % of population for the UK**

![Image](https://i.imgur.com/7ATIEOq.png)
