# Feature1 = OverallQual
- Summary: It has spike at specific integer that is 1 to 10. 1 means very poor and 10 means very exilent. so it is oridinal by nature
- Visual finding: average are lies between 4 to 8. have 2 peaks.
- Possible cause: It common for most house quality is avarege.
- Decision / Action: I'm gonna do oridinal encoding.

- Next-step code: 

```from sklearn.preprocessing import OrdinalEncoder

# Define order (integers already ordered, but encode explicitly)
data['GarageCars_ord'] = data['GarageCars'].astype('category')  # Ensures order

encoder = OrdinalEncoder(categories=[sorted(data['GarageCars'].unique())])  # Enforce order
data['GarageCars_encoded'] = encoder.fit_transform(data[['GarageCars']])```

- Logged on: 19 October, 2025

# Feature2 = GrLivArea
- Summury = It have nice not much but ok normal distrubution

# Feature3 = GarageCars
- Summury = It has spike at specific integer. 
- Visual Finding = the spike at 0 to 4. highest value in 2
- Decision = I gonna scatterplot it with saleprice and see if it linear or not. 
- Next-step code : 
``` plt.scatter(X_train['GarageCars'], y_train, alpha=0.6, edgecolors='k', linewidth=0.5)```

# Feature4,5,6 = TotalBsmtSF_capped , GarageArea,  1stFlrSF
- summury = it has ok norlam distibution

# Feature7 = FullBath
- Summary: It has spike at specific integer.
- Visual finding: Have value from 0 to 3. 90% at 1 and 2
- Possible cause: It's natural
- Decision / Action: gonna leave it as it be. It means I'm gonna treat as integer
- Next-step code: Nothing

# Feature8 = TotRmsAbvGrd
- Summary: it also has spike at specific integers
- Visual finding: value is from 2 to 14.
- Possible cause: 
- Decision / Action: first I need to handle outlier and do oridical encoding 
- Next-step code: 