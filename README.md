# data-science-practicles

## Replace outlier with the median of that features
    mean, std = users[cols[0]].mean(), users[cols[0]].std()
    median = users[cols[0]].loc[(users[cols[0]] - mean).abs() < 3*std].median()
    users['testing'] = np.where((users[cols[0]] - mean).abs() > 3*std, median,users[cols[0]])
    plt.plot(users['testing'])
    
    
## Remove outliers
    # np.percentile(train[cols[0]],q=0.1)
    q1 = users[cols[0]].quantile(0.10)
    q3 = users[cols[0]].quantile(0.90)
    iqr = q3-q1
    # train[cols[0]][~(train[cols[0]] < (q1-1.5*iqr) | train[cols[0]] > (q1+1.5*iqr)).
    #                any(axis=1)].shape
    users = users[(users[cols[0]]< (q3+1.5*iqr))]
    users = users[(users[cols[0]]>(q1-1.5*iqr))]



## Merging array in the DataFrame
        # convert array in the list first.
        First make the list into a Series:
        se = pd.Series(mylist)
        
        Then add the values to the DataFrame:
        df['new_col'] = se.values


## One-Hot Encoding
        >>> a = np.array([1, 0, 3])
        >>> b = np.zeros((3, 4))
        >>> b[np.arange(3), a] = 1
        >>> b
        array([[ 0.,  1.,  0.,  0.],
               [ 1.,  0.,  0.,  0.],
               [ 0.,  0.,  0.,  1.]])
               
               
        users = np.zeros((4,3345))
        users[np.arange(4), temp[:,1].astype(int)[0]] = 1 
        users
