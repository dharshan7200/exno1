# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
import numpy as np
import seaborn as sns
import os 
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/386699f2-5ead-452a-988f-9dc702780233)
```
df.isnull().sum()
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/b1e58f0d-028a-4d81-a5a4-4c9d124be6ff)
```
df.isnull().any()
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/1e44112b-62f1-45d9-ae5d-e219ce3e3366)
```
df.dropna()
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/086d0bfb-e543-4a6d-8a3c-26190da1b3d1)
```
df.fillna(0)
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/8880436a-437e-482e-9a1d-9003245f07fa)
```
df.fillna(method = 'ffill')
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/65bd6f16-25fd-4909-9545-6a6d43c7005f)

```
df.fillna(method = 'bfill')
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/f1460e19-efbe-47b2-b76f-2707efaed2cd)
```
df_dropped = df.dropna()
df_dropped
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/e65154f6-d942-4308-b9dc-94083969771f)
```
df.fillna({'GENDER':'FEMALE','NAME':'PRIYU','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/592588ca-a0f9-4acd-8059-cac8d444a3e4)

## IQR(Inter Quartile Range)
```
import pandas as pd
ir=pd.read_csv('iris.csv')
ir
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/f6aacc7a-fdc7-4bee-8a80-fa4ad12344a5)
```
ir.describe()
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/55ac293d-8a30-435a-9d0c-91f246817f33)
```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/7ae0fb52-f9c4-4a76-b6a2-55f7c931ce6e)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
![image](https://github.com/dharshan7200/exno1/assets/138850116/743ab1d5-b07b-4851-ae77-b134525afc42)


rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
![image](https://github.com/dharshan7200/exno1/assets/138850116/d288949a-e36a-4020-8c6a-1c630a1b9d1f)

delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
![image](https://github.com/dharshan7200/exno1/assets/138850116/00c49cfc-74d6-4a55-989a-d3d1c60528e6)

sns.boxplot(x='sepal_width',data=delid)
![image](https://github.com/dharshan7200/exno1/assets/138850116/8dc2e07f-4e1b-4b59-9b68-8d1a1cad8bf7)

## Z score

import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
![image](https://github.com/dharshan7200/exno1/assets/138850116/96ca1de3-a4ca-4633-b9c6-82ad79008375)

df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
![image](https://github.com/dharshan7200/exno1/assets/138850116/08f4c7b4-2a81-43b4-98fa-87aefc1dc2a1)

low = q1 - 1.5*iqr
low
![image](https://github.com/dharshan7200/exno1/assets/138850116/0582bd6e-71cb-49ca-8e86-2e1eda81256b)

high = q3 + 1.5*iqr
high
![image](https://github.com/dharshan7200/exno1/assets/138850116/c7d4e890-6d59-4c6e-a615-8a965f562ea5)

df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
![image](https://github.com/dharshan7200/exno1/assets/138850116/5021f352-2840-4e17-bdaa-a89c4e000382)

z = np.abs(stats.zscore(df['height']))
z
![image](https://github.com/dharshan7200/exno1/assets/138850116/0fdfc9e5-799b-4673-bb6c-b3e94f105c26)

df1 = df[z<3]
df1
![image](https://github.com/dharshan7200/exno1/assets/138850116/cc0a56f3-7f6f-415b-b000-3f63d30f83f6)

```
## Result:

Hence the data was cleaned , outliers were detected and removed.

