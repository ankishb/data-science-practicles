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
