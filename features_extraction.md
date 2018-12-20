use the apply() method, which applies a function along a specific axis (meaning, either rows or columns) of a DataFrame

The lambda function includes the axis parameter at the end, in order to specify whether Pandas should apply the function to rows (axis = 1) or columns (axis = 0).


# axis=1 indicates applu the function on entrire column

# Timing apply on the Haversine function
df['distance'] = df.apply(lambda row: haversine(40.671, -73.985, row['latitude'], row['longitude']), axis=1)



## change value of one column using 'loc'
adjusted_ratings.loc[adjusted_ratings['rating_adjusted'] == 0, 'rating_adjusted'] = 1e-8
