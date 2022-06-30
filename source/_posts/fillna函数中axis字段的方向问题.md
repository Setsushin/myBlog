---
title: fillna函数中axis字段的方向问题
categories: 
- Technologies
tags:
- Python
- Pandas
---

在使用Pandas时，如果想要填充某个dataframe中的缺失值NaN，可以使用fillna函数。  
fillna函数有两个常用字段：method和axis。  
如果用固定值填充，可以直接使用fillna(n)，其中n代表要使用的填充值。  
如果要使用method，有两种可用方法：bfill/backfill和ffill/pad。其中：  
bfill/backfill使用下一个有效值填充  
ffill/pad使用前一个有效值填充  

例子如下：  
使用pad方法填充reviews中的缺失值：  
```
reviews = pd.DataFrame([[np.nan, 2, np.nan, 0],
                   [3, 4, np.nan, 1],
                   [np.nan, np.nan, np.nan, 5],
                   [np.nan, 3, np.nan, 4]],
                  columns=list("ABCD"))
```

按照逻辑，填充值应该来自于同一列，所以axis应该为1，对吗？让我们试试看：  
```
reviews.fillna(method = 'pad', axis = 1)
```
 
完全不对！让我们把axis换成0再试一次。  
```
reviews.fillna(method = 'pad', axis = 0)
```
 
正确的axis是0。实际上，如果我们去掉axis字段使用默认值，我们也会得到axis=0的结果。  

所以，在fillna函数中：  
默认或axis = 0：沿纵向获取有效值填充  
axis = 1：沿横向获取有效值填充

这里的axis可能并不是“获取数值的方向”，而是“填充数值的推进方向”。  
比如axis=0时，数值填充是按列处理的，但在整体角度，推进方向是沿axis=0前进的。  
这可能有点反直觉，但我们最好还是记住这件它。  

