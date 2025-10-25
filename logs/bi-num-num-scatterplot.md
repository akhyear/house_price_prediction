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

# GrLivArea_capped, TotalBsmtSF_capped- SalePrice
- Summary:
- Visual finding: IT HAS CONE DISTRIBUTION
- Possible cause: 
- Decision / Action: GONNA TRANSFORM Y

- Next-step code: 
```python
y_log = np.log1p(y_train)
y_log_flattern = y_log.flatten() if hasattr(y_log, 'flatten') else np.ravel(y_log)
# for training
y_pred_real = np.expm1(y_pred_log)
```

# 2ndFlrSF - SalePrice
- Summary: Second floor square feet. the 
- Visual finding: to many zeros but rest have linear correlation. Percentage of zeros in 2ndFlrSF: 56.25%
Zero count: 657 out of 1168.
- Decision / Action: I'm gonna make a binary indicator for whether house has 2nd floor. for houses WITH 2nd floor, I gonna transform.

- Next-step code: 
```python
# Create a binary indicator for whether house has 2nd floor
df['Has2ndFloor'] = (df['2ndFlrSF'] > 0).astype(int)

# For houses WITH 2nd floor, you might want to log transform
df['2ndFlrSF_log'] = df['2ndFlrSF'].apply(lambda x: np.log1p(x) if x > 0 else 0)
```
- Option 2: Keep original as-is . The 56% zeros is actually meaningful, most houses are single-story. Tree-based models (Random Forest, XGBoost, LightGBM) handle this naturally
