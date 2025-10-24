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

# GrLivArea_capped - SalePrice
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