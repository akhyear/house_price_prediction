# OverallQual - Saleprice
- Visual finding: it has liner relationship with target column, but it has stack of point from 1 to 10.
- Decision / Action: based on univariate analysis I'm sure I'm gonna use ordinal encoding
- Next-step code: 
```python 
from sklearn.preprocessing import OrdinalEncoder
# Define order (integers already ordered, but encode explicitly)
data['OverallQual_encoded'] = data['OverallQual'].astype('category')  # Ensures order
encoder = OrdinalEncoder(categories=[sorted(data['OverallQual'].unique())])  # Enforce order
data['OverallQual_encoded'] = encoder.fit_transform(data[['OverallQual']])
```