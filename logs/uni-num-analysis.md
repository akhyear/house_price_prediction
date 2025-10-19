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

- Logged on: 19 October, 2025

# Feature 2 = GrLivArea
- Summury = It have nice not much but ok normal distrubution

# Feature 3 = GarageCars
- Summury = It has spike at specific integer. 
- Visual Finding = the spike at 0 to 4. highest value in 2
- Decision = I gonna scatterplot it with saleprice and see if it linear or not. 
- Next-step code : 
```python 
plt.scatter(X_train['GarageCars'], y_train, alpha=0.6, edgecolors='k', linewidth=0.5)
 ```

# Feature 4,5,6 = TotalBsmtSF_capped , GarageArea,  1stFlrSF
- summury = it has ok norlam distibution

# Feature 7 = FullBath
- Summary: It has spike at specific integer.
- Visual finding: Have value from 0 to 3. 90% at 1 and 2
- Possible cause: It's natural
- Decision / Action: gonna leave it as it be. It means I'm gonna treat as integer
- Next-step code: Nothing

# Feature 8 = TotRmsAbvGrd
- Summary: it also has spike at specific integers
- Visual finding: value is from 2 to 14.
- Possible cause: 
- Decision / Action: first I need to handle outlier and do oridical encoding 
- Next-step code: 

# Feature 9 = YearBuilt
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