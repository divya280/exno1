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
## BY 
## Name: V.DIVYASHREE
### REG.NO: 212223230051
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/6a354be4-f1ea-4c63-8c19-ca085399f578)

```
df.head(3)
df.tail(3)
```
![image](https://github.com/user-attachments/assets/89411b5e-ecdd-4a06-8364-daf43f3b8321)
```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/ebf374ad-0163-4167-b543-8277640cb9f0)
```
df.dropna(how='any').shape
```
![image](https://github.com/user-attachments/assets/87ac8c29-36aa-4503-bde9-63b5cc2a977b)
```
df.shape
```
![image](https://github.com/user-attachments/assets/724bb44e-104c-43cc-8946-9db755612cb9)
```
mn=df.TOTAL.mean()
mn
```
![image](https://github.com/user-attachments/assets/2e65d9d5-f0a9-4d4e-98f0-c6dde9a1701f)
```
df.TOTAL.fillna(mn,inplace=True)
df
```
![image](https://github.com/user-attachments/assets/f46dcc52-02d3-40f7-9776-37fdfd358b06)
```
df.drop_duplicates(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/b91e8e84-f187-4e9b-80ca-4d6c19c06405)
```
df.duplicated()
```
![image](https://github.com/user-attachments/assets/417ce399-d51c-4543-aea5-3d174ded32b2)

```
df['DOB']
```
![image](https://github.com/user-attachments/assets/8b446378-7271-43e4-a4b4-4c19e7cae53b)
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df['DOB'] = pd.to_datetime(df['DOB'], format='%Y-%m-%d',errors='coerce')
df['DOB']
```
![image](https://github.com/user-attachments/assets/74ab2aa4-672f-4703-a8da-610b6b56fcbc)
```
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/94f63fd8-0abb-4134-8958-a22fb1906cf6)
```
import pandas as pd
import seaborn as sns
import numpy as np
```
```
age = [1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af= pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/f6a5d357-f2c2-4901-9ffc-fc75ab17dc66)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/545d965b-e7e9-4e0c-85ff-d898b661145a)
```
sns.scatterplot(data=af)
```
![image](https://github.com/user-attachments/assets/7d8d6c86-c6c9-4016-8893-7dd409cd3ae6)
```
q1=af.quantile(0.25)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/dbc7ffe7-90b3-4182-8bb7-a1c0df7765bf)
```
Q1 = np.quantile(af, 0.25)
Q3 = np.quantile(af, 0.75)
IQR = Q3 - Q1
IQR
```
![image](https://github.com/user-attachments/assets/c7832dd8-081a-468f-a7f5-843d8211c62f)

```
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
```
```
lower_bound
```
![image](https://github.com/user-attachments/assets/166179de-f586-4f42-bc17-5642741b0e33)
```
upper_bound
```
![image](https://github.com/user-attachments/assets/4a7514ab-c547-4353-bb89-386bee9fb035)
```
outliers = [x for x in age if x < lower_bound or x > upper_bound]
```
```
print("Q1:",Q1)
print("Q3:",Q3)
print("IQR:",IQR)
print("Lower Bound:",lower_bound)
print("Upper Bound:",upper_bound)
print("Outliers:",outliers)
```
![image](https://github.com/user-attachments/assets/2e4ca8dd-985a-4eaf-8d3c-9e89c0b73e32)
```
af=af[((af >= lower_bound)&(af <= upper_bound))]
af
```
![image](https://github.com/user-attachments/assets/467302d7-c18b-4a0a-86c5-90443ebe7bd0)
```
af.dropna()
```
![image](https://github.com/user-attachments/assets/d91e3c6c-1e31-461b-b953-55977176d6f4)
```
sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/89eae0f4-6d5f-42cd-98aa-4f7a82913c65)
```
data = [1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean = np.mean(data)
std = np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)
```
![image](https://github.com/user-attachments/assets/abf17827-1fc9-4e45-bf54-b90beda5c8a9)

```
threshold = 3
outlier = []
for i in data:
  z_score = (i-mean)/std
  if np.abs(z_score) > threshold:
    outlier.append(i)
print('outlier in dataset is',outlier)
```
![image](https://github.com/user-attachments/assets/9ea52dc4-8173-435e-8a9b-345d8cdedebd)
```
import pandas as pd
import numpy as np
import seaborn as sns
import pandas as pd
from scipy import stats
```
```
z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
![image](https://github.com/user-attachments/assets/6612b79c-fc0f-4342-b5ca-31cf3e07f3b6)




# Result
          Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
