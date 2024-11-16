# AppDSExno-03

**AIM:**

To Implement Recommendation Systems using the suitable data sets.

**ALGORITHM:**

STEP 1: Load the necessary Datasets.

STEP 2: Include the necessary python library.

STEP 3: Use Fuzzy library for handling text data.

STEP 4: Perform Data Preprocessing Steps.

STEP 5: Standardize column names for merging.

STEP 6: Apply fuzzy matching to find similar text data between datasets.

STEP 7: Perform Data transformation between datasets.

STEP 8: Define a recommendation score using the features of the datasets.

STEP 9: Sort the data by recommendation score.

STEP 10: Export the results to a CSV file.


**CODING & OUTPUT**
```c
import pandas as pd
import numpy as np
pip install pandas numpy scikit-learn fuzzywuzzy python-Levenshtein
```
![371784163-1b5039b0-b2eb-4665-99ca-f38164996056](https://github.com/user-attachments/assets/95733b19-8d48-4ed2-abf4-99f1cef2947f)

```c
from fuzzywuzzy import process
from sklearn.preprocessing import MinMaxScaler
df = pd.read_csv('/content/emobile.csv')
df.head()

```

![371784204-5f686c6b-770a-4509-abdc-60b53ec8bdc8](https://github.com/user-attachments/assets/f42cf94a-a520-40eb-8ea1-49996a0af4ea)

```c
dx = pd.read_csv('/content/maxmobile.csv')
dx.head()
```

![371784229-7f554645-1f70-4221-8a61-2d98f6b490a6](https://github.com/user-attachments/assets/571a0cb8-bc9e-46d2-8957-223bd960799f)

```c
df.drop_duplicates(inplace=True)
dx.drop_duplicates(inplace=True)
df.columns = ['Product_id','Product_Name','Rating','Review_Count']
def match_products(name,choices,limit=1):
  results = process.extract(name,choice,limit=limit)
  return results[0][0] if results else None
print(dx.columns)
print(df.columns)

```

![371784287-ec65abf3-25e9-4deb-ba6b-888177db40b6](https://github.com/user-attachments/assets/c2a49d35-d608-4611-b498-917d7e53b16c)

```c
dx.columns = dx.columns.str.strip()
print(dx.head())
df.drop_duplicates(inplace=True)
dx.drop_duplicates(inplace=True)
df.columns = ['Product_id','Product_Name','Rating','Review_Count']
dx.columns = ['Product_id','Product_Name','Rating','Review_Count']

```

![371784399-66ee8244-a28f-4cb1-863b-f4e1f499b507](https://github.com/user-attachments/assets/b123685b-a62d-46bb-b410-8a5f8459f95b)

```c
def match_products(name,choices,limit=1):
  results = process.extract(name,choices,limit=limit)
  return results[0][0] if results else None
dx['Matched_Product'] = dx['Product_Name'].apply(lambda x: match_products(x,df['Product_Name'].tolist()))
merged_df = pd.merge(df, dx, left_on='Product_Name', right_on='Matched_Product', how='inner', suffixes=('_ds1', '_ds2'))
merged_df

```
![371784492-a011d33b-bda1-47a6-8dd0-b6e8db1f2890](https://github.com/user-attachments/assets/a82d5ab1-c68b-4a92-af09-9055505462da)

```c
merged_df.columns
x=merged_df['Review_Count_ds1'] + merged_df['Review_Count_ds2']
x=merged_df['Rating_ds1'] + merged_df['Rating_ds2']
merged_df['Combined_Rating'] = (merged_df['Rating_ds1'] * merged_df['Rating_ds1']+merged_df['Rating_ds2'] * merged_df['Rating_ds2'])/x
merged_df['Recommendatio_Score'] = 0.7* merged_df['Combined_Rating'] + 0.3 * merged_df['Rating_ds1']
merged_df.head()

```


![371784598-63f347e2-2454-4bf8-8359-3377fd1f9b0a](https://github.com/user-attachments/assets/59e67ad6-177b-4247-9916-826a5491f956)

```c
best_products = merged_df.sort_values(by='Recommendatio_Score', ascending=False)
print(best_products[['Matched_Product', 'Combined_Rating', 'Recommendatio_Score']].head(10))
print(best_products.columns)
best_products.columns = best_products.columns.str.strip()  # Remove any leading or trailing spaces
best_products[['Matched_Product', 'Combined_Rating', 'Recommendatio_Score']].to_csv('best_recommended_products.csv', index=False)

```


![371784643-930d4181-b86d-443d-8077-e52a91d0da00](https://github.com/user-attachments/assets/b4059416-cc79-4a19-b089-25b4fbb2e861)

```c

rp=pd.read_csv('/content/best_recommended_products.csv')
rp.head()

```


![371784677-4e8de5c0-00a5-4ab7-9363-8f7a990d2def](https://github.com/user-attachments/assets/a3c69f99-093a-4005-a606-44d8abe88d53)



**RESULT**
Thus, Recommendation Systems using the suitable data sets is implemented successfully.
