
第一部分：Series
^^^^^^^^^^^^^^^^^^^^^^^^^^

Pandas是一个强大的分析结构化数据的工具集；它的使用基础是
Numpy（提供高性能的矩阵运算）；用于数据挖掘和数据分析。

Series:
它是一种类似于一维数组的对象，是由一组数据(各种NumPy数据
类型)以及一组与之相关的数据标签(即索引)组成。仅由一组数据
也可产生简单的Series对象。

在pandas的相应代码中，需要numpy和pandas的拓展包功能，所以一般都需要在开头加上::

    import numpy as np
    import pandas as pd

1.1 Series 的主要特点
--------------------------

特点1
    Series是一种key-value型数据结构，每个元素由#key(多个显式index)
    和#value(每个显式index对应的值value)。
特点2
    Series存在两种index。



1.2 Series 的定义方法
--------------------------

利用pd.Series()函数来实现定义，见如下示例::

    import pandas as pd
    mySeries1 = pd.Series(data = [11,12,13,14],
        index = ['a','b','c','d'])
   
    mySeries1


*index与 value的个数应一致，否则会报错。*
*当 index是字符串时，应用双引号或者单引号括起来* 



1.3 Series 的操作方法
--------------------------

(1)查看显式index部分::

    mySeries1.index

(2)查看values部分::

    mySeries1.values

*此处 values拼写是复数*

(3)通过显式index查看元素，支持切片::

    mySeries1['b']
    #单双引号均可

    #切片1方法
    mySeries1[['a','b','c']]

    #切片2方法
    mySeries1['a':'d']

(4)通过隐式index读取元素::

    #切片
    mySeries1[1:4:2]

(5)支持显式index的in操作::

    'c' in mySeries1
    #若存在，返回值为True，否则为False

(6)更新显式index的方法：.reindex()::

    #1
    import pandas as pd
    mySeries2 = pd.Series([21,22,23,24,25,26,27], index = ['a','b'
                ,'c','d','e','f','g']
    mySeries3 = mySeries2.reindex(index = ['b','c','a','d','e','g'
                ,'f'])
    #在reindex过程中，mySeries2本身并未改变


    #2
    #如果更新后的index不存在，会自动增加key，对应的value为NaN缺失值
    mySeries4 = mySeries2.reindex(index = ['new1','c','a','new2'
            'e','g','new3'])
    #mySeries4输出结果
    #IN:  
         mySeries4
    #OUT:
         new1   NaN
         c      23.0
         a      21.0
         new2   NaN
         e      25.0
         g      27.0
         news3  NaN
         dtype: float64
         
*reindex()不改变Series对象本身的显式index*