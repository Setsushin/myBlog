---
title: Obtain MAX/MIN values or indexes from any column/row
categories: 
- Technologies
tags:
- Python
- Pandas
---

This post introduces some common operations of obtaining MAX/MIN values or indexes from any column/row.
Yes, it's very basic. But reviewing is not bad, always.

previous:  
_import pandas_  
_df = pandas.dataframe(data)_  

Obtain the MAX/MIN value of one column:  
```
df[‘column_name’].max()
df[‘column_name’].min()
```

Obtain the MAX/MIN value indexes of one column:  
```
df[‘column_name’].idxmax()
df[‘column_name’].idxmin()
```

You need to use _loc/iloc_, if you want to deal from _"row"_:  
Obtain the MAX/MIN value of one row:  
```
df.loc[‘row_name’].max()
df.loc[‘row_name’].min()
```
or:  
```
df.iloc[row_index].max()
df.iloc[row_index].min()
```

Obtain the MAX/MIN value indexes of one row:  
```
df.loc[‘row_name’].idxmax()
df.loc[‘row_name’].idxmin()
```
or:  
```
df.iloc[row_index].idxmax()
df.iloc[row_index].idxmin()
```
