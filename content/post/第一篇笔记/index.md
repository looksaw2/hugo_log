+++
date = '2025-02-09T21:57:28+08:00'
draft = true
title = 'Python办公自动化'
+++

# Python办公自动化
Python是一门很强大的语言，而且在办公自动化的领域，相比与VBA而言，Python办公自动化有无与伦比的优势。下面来看看Python的强大的自动化能力。

### Python环境的搭建
由于在写本文时采用的操作系统是Ubuntu，所以本节略过。

### Python的基本知识
最基本的知识语法方面的可以去看其他的博主，这里主要讲一讲一些主要的库的使用。
1. Numpy
   Python上最好的数学库，并且速度相比与Python自己的方法而言，速度快很多。缺点是必须存储的是同类型的数据，例如：

   ```python
   MyList = [1 , "helloWorld", 3.14]
   ```


   就是不可行的，它的基本用法如下


   ```python
   import numpy as np
   a1 = np.array([1,2,3])
   ```

   其还支持从中取出对应的行和列的元素

   ```python
   import numpy as numpy
   a1 = np.array([[1,2,3],[4,5,6],[7,8,9]])
   a2 = a1[0,:]
   ```
   可以发现a1 = [1,2,3] , [4,5,6] ,[7,8,9] 而a2 = [1,2,3]说明其可以取出对应的行和列，很方便。

2. pandas
   从pandas可以读取excel导出的.xlsx文件，首先可以新建一个excel文件，其表格形式如下
   | id | name | age | sex|
   | -- | --   |  --  | -- |
   | 01 | 小明  |  15  | 男  |
   | 02 | 小红  | 18   | 女  |
   | 03 | 张三 |  65   | 男  |

   然后可以通过python进行读取:

   ```python
   import numpy as np
   import pandas as pd
   import os
   pathNow = os.getcwd() 
   xlsxFile = os.path.join(pathNow , "test1.xlsx")
   myExcel = pd.read_excel(xlsxFile,engine='openpyxl')
   print(myExcel)
   ```   
   可以发现这个过程主要可以分成三部
   + 导入必要的库
   + 得到.xlsx文件的路径(os.getcwd()得到当前路径，再利用os.path.join()拼接)
   + 读取对应的.xlsx文件

   并且，更强大的是python可以自己创建一个pandas中的数据表格而不需要从Excel中导出，如下:

   ```python
   myData = [
        ["小明",15,"男"],
        ["小红",18,"女"],
        ["张三",65,"男"]
    ]
    myDF = pd.DataFrame(
        data=myData,
        columns=["name","age","sex"],
        index=[0,1,3]
    )
   ```
   显然，输出myDF可以得到对应的表格，更进一步的，在得到了对应的表格之后，便要开始得到修改这些数据了，例如想得到表格中的name 和 sex可以这样做。
   ```python
    myDF2 = myDF.loc[:,["name","sex"]]
   ```
   可以发现myDF2的表格如下:
   | id | name | sex |
   | --- | ---  | -- |
   | 1  | 小明  | 男  |
   | 2 | 小红   | 女  |
   |3  | 张三   | 男  |

   更进一步的，如果我想得到所有性别为男的人，则可以这样写
   ```python
   tf = myDF["sex"] == "男"
   myDF2 = myDF[tf]
   ```
   这样就筛选出了所有性别为男的。下面可以去创建一个更大的表，具体如下:
   | id | name | age | sex | country | score | phoneNumber |
   | -- | --   |---  |--  |  ---    | ---   | -----       |
   | 1  | 小明  | 15  | 男 |  中国    |  80.1 | 13782169132 |
   | 2  | 小红  | 18  | 女 | 美国     | 93.2  | 13754321234 |
   | 3  | 张三  | 65  | 男 | 中国     | 58.8   | 18765439887 |
   | 4 |  李四  | 34  | 男 | 中国     | 52.8   | 18775555555 |

   想筛选出来性别为男并且得分低于60的人，在python上可以这样做:
   ```python
   #df1为xlsx读取到的数据
   tf = (df1["sex"] == "男") & (df1["score"] <= 60.0);
   df2 = df1[tf]
   ```
   可以得到如下的图表
   | id | name | age | sex | country | score | phoneNumber |
   | -- | --   |---  |--  |  ---    | ---   | -----       |
   | 3  | 张三  | 65  | 男 | 中国     | 58.8   | 18765439887 |
   | 4 |  李四  | 34  | 男 | 中国     | 52.8   | 18775555555 |

   需要修改可以为(例如将张三，李四的分数修改为100)
   ```python
    tf = (df1["name"] == "张三") | (df1["name"] == "李四")
    df1.loc[tf,"score"] = 100
   ```
   可以得到:
   | id | name | age | sex | country | score | phoneNumber |
   | -- | --   |---  |--  |  ---    | ---   | -----       |
   | 1  | 小明  | 15  | 男 |  中国    |  80.1 | 13782169132 |
   | 2  | 小红  | 18  | 女 | 美国     | 93.2  | 13754321234 |
   | 3  | 张三  | 65  | 男 | 中国     | 100   | 18765439887 |
   | 4 |  李四  | 34  | 男 | 中国     | 100   | 18775555555 |

### 正则表达式
   ToDo




