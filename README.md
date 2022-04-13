# pandas shenanigans

### Dataframe Manipulation
#### single column
##### apply/lambda
```python
df['col1'].apply(lambda x : x.strip().capitalize())
```
##### mapping - more efficient for applying methods to a single column (series vs. entire row)
```python
df['colA'] = df['colA'].map(lambda x: x + 1)
```
#### multiple columns 
##### same function
```python
df[['colA', 'colD']] = df[['colA', 'colD']].apply(lambda x: x + 1)
```
##### different functions
```python
def col_func(x):
    x['col1'] = 1
    x['col2'] = x['col2'] + 'x
    return x

df.apply(col_func, axis=1)   
```


##### iterating
```python
for index, row in df.iterrows():
    print(row['col1'], row['col2'])
    
 for ind in df.index:
     print(df['name'][ind], df['age'][ind])
```

##### conditional new column
```python
## ternary if statement
df['Price'] = [1500 if x =='Music' else 800 for x in df['Event']]



```


##### filtering 
```python 
# Boundary filtering
dataframe[dataframe['Percentage'] > 80]

# In a list
options = ['Math', 'Commerce', 'Shaurya']
rslt_df = dataframe[~dataframe['Stream'].isin(options)]

# Both conditions
rslt_df = dataframe[(dataframe['Age'] == 21) & dataframe['Stream'].isin(options)]
```
##### drop
```python
df = df.dropna(how = 'all')
df.drop(df[df['Age'] < 25].index, inplace = True)
```

##### Column Naming
```python
# Change all the column names
df.columns =['Col_1', 'Col_2']

# Change all the row indexes
df.index = ['Row_1', 'Row_2', 'Row_3', 'Row_4']

# Change some of the columns 
df = df.rename(columns = {"Col_1":"Mod_col"})

## add x to every column name
df = df.rename(columns=lambda x: x+'x')
```
##### Text?
```python
df1 = df['Position'].str.contains("PG")
```



### create dataframe
- list
- dict
- list of dicts
``` python 
pd.DataFrame(lst, columns = ["col1", "col2"])
pd.DataFrame(dict)
pd.DataFrame(lst_of_dicts)
```
##### list
```python
lst = [['Geek', 25], ['is', 30],
       ['for', 26], ['Geeksforgeeks', 22]]
       
pd.DataFrame(lst, columns = ["word", "number"])
```
##### dict
```python
dict = {'col1':['val1', 'val2', 'val3'],
        'col2':[0, 1, 3]}
pd.DataFrame(dict)
```
##### list of dicts

```python
lst_of_dicts = [{'Geeks': 'dataframe', 'For': 'using', 'geeks': 'list'},
        {'Geeks':10, 'For': 20, 'geeks': 30}]
pd.DataFrame(lst_of_dicts)      
```
##### series

```python
author = ['Jitender', 'Purnima', 'Arpit', 'Jyoti']
article = [210, 211, 114, 178]

auth_series = pd.Series(author)
article_series = pd.Series(article)

frame = { 'Author': auth_series, 'Article': article_series }

result = pd.DataFrame(frame)
``` 


### Combinging Data

##### mapping new data
```python
new_data = { "col1":"val1",
             "col2":"val2",
             "col5":"val5",
             "col3":"val3",
             "col4":"val4"
              }

# combine this new data with existing DataFrame
df["new_col"] = df["old_col_to_match"].map(new_data)
```
##### replacing new data
```python
new_data = { "col1":"val1",
             "col2":"val2",
             "col5":"val5",
             "col3":"val3",
             "col4":"val4"
              }

df = df.replace({"old_col_to_match":new_data})
```



