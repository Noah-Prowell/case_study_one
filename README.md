# Teenage Pregnancy, Unmet Needs for Contraceptives, and Changes in School Careers

Goal: 


## Our Raw Data



After reading in the raw data from Health Nutrition and Population Statistics, it was immediately apparent that we would have to do some transformation to get it into a workable form. As you can see, the rows were an index of numbers from 1 to ~90,000, and the columns are country names, years 1960-2016, and indicators.


![Image](https://imgur.com/kmSFYlx.png)

![Image](https://imgur.com/JSbVIxv.png)


The indicators (things like population size, death rate, etc.) was the data we actually cared about, so we needed to find a way to transform the dataframe to better represent that.


```
df = pd.read_csv('../data/data.csv')
df_US = df[df['Country Name'] == 'United States'] #make US only Dataframe
df_US = df_US.transpose()

df_US.columns = df_US.iloc[3] #make the colums the values for row 4 (indicator code) 
df_US.drop(df_US.index[3], inplace=True) #drop the indicator code row since its now the column name
```

To do this, decided to focus in on the US and UK specifically, allowing us to sqeeze our indicators down to unique values with no duplicates. Then we made the indicators our columns, and ended up with a dataframe that makes much more sense. 


![Image](https://imgur.com/HWzINGo.png)


Now, we had reduced our dataframe from a 90,000x60 dataframe, to two 345x60 dataframes. MUCH more manageable.

## Exploring our data

Exploring our data showed us that there were quite a lot indicators with little or no data. So, we ended up just grabbing columns that had good, worable data:

**Urban population as a % of population for the UK**

![Image](https://i.imgur.com/xYGvo1o.png)

**US v. UK population growth**

![Image](https://i.imgur.com/zoAuH7j.png)

**US v. UK Death Rate**

![Image](https://i.imgur.com/M0DnwAH.png)

**US v. UK Birth Rate**

![Image](https://i.imgur.com/KQ8SqkT.png)
