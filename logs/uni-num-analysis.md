# Feature 1 = OverallQual
- Summary: It has spike at specific integer that is 1 to 10. 1 means very poor and 10 means very exilent. so it is oridinal by nature
- Visual finding: average are lies between 4 to 8. have 2 peaks.
- Possible cause: It common for most house quality is avarege.
- Decision / Action: I'm gonna do oridinal encoding.

- Next-step code: 

```python 
from sklearn.preprocessing import OrdinalEncoder

# Define order (integers already ordered, but encode explicitly)
data['GarageCars_ord'] = data['GarageCars'].astype('category')  # Ensures order

encoder = OrdinalEncoder(categories=[sorted(data['GarageCars'].unique())])  # Enforce order
data['GarageCars_encoded'] = encoder.fit_transform(data[['GarageCars']])
```

# Feature 2 = GrLivArea_capped
- Summury = It have nice not much but ok normal distrubution

# Feature 3, 4, 8= TotalBsmtSF_capped , GarageArea_capped, 
- summury = it has ok norlam distibution

# Feature 5 = YearBuilt 
- Summary: Original construction date. from 1880 to 2000.
- Visual finding: It is right skew data.
- Possible cause: Early years (1880–1920) show very low counts (near zero to ~20), indicating few older structures in the dataset—possibly due to urban development patterns, data collection biases (e.g., focusing on modern housing markets), or historical events like fires/wars destroying older builds.
- Decision / Action: gonna find out is it truly skewe. if yes then I'm gonna use log-transformation. 

- Next-step code:
```python 
df['YearBuilt_log'] = np.log(df['YearBuilt'] + 1)  # +1 for safety, though not needed

# Step 2: Verify the transformation
print("Original stats:")
print(df['YearBuilt'].describe())
print("\nLog-transformed stats:")
print(df['YearBuilt_log'].describe())

# Step 3: Visualize before/after (optional)
fig, axes = plt.subplots(1, 2, figsize=(12, 5))

# Original histogram
sns.histplot(df['YearBuilt'], kde=True, ax=axes[0])
axes[0].set_title('Original Distribution')

# Log-transformed histogram
sns.histplot(df['YearBuilt_log'], kde=True, ax=axes[1])
axes[1].set_title('Log-Transformed Distribution')

plt.tight_layout()
plt.show()  # Or plt.savefig('transformation.png') to save '''
```



# Feature6 = 2ndFlrSF
- Summary: Second floor square feet
- Visual finding: most of the value is Zero
- Possible cause: maybe those house have not second floor
- Decision / Action: I'm gonna do some reaserch with price and see if it is worth to keep. if yes then I gonna add bool to this 
  
- Next-step code: 
```python
  X_train['2ndFlrSF_Binary'] = (X_train['2ndFlrSF'] > 0).astype(int)
  ```

# Feature 7 = BsmtFinType1
- Summary: Type 1 finished square feet
- Visual finding: high spike at zero and I think it is left skewed
- Possible cause: many houses might have not basement
- Decision / Action: I'm gonna check weather it is skewed or not if yes then gonna aplly log_transformation. also gonna do bivariate analysis
- Next-step code: same as feature 5

# Feature 9 = LotArea
- Summary: Lot size in square feet
- Visual Finding: Normal distribution at right side but it have log tail at left.
- Possible cause : 
- Next-step code:
  ```Python
  X_train["LotArea_capped"].skew()
  X_train['LotArea_log'] = np.log1p(X_train['LotArea_capped'])
  sns.histplot(data=X_train, x = 'LotArea_log', kde = True)
  X_train["LotArea_log"].skew()