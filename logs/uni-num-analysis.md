# Feature = OverallQual
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