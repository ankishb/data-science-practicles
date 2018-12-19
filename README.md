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
        
        
        
        
## convert data-type



        The input to to_numeric() is a Series or a single column of a DataFrame.

        >>> s = pd.Series(["8", 6, "7.5", 3, "0.9"]) # mixed string and numeric values
        >>> s
        0      8
        1      6
        2    7.5
        3      3
        4    0.9
        dtype: object

        >>> pd.to_numeric(s) # convert everything to float values
        0    8.0
        1    6.0
        2    7.5
        3    3.0
        4    0.9
        dtype: float64

        As you can see, a new Series is returned. Remember to assign this output to a variable or column name to continue using it:

        # convert Series
        my_series = pd.to_numeric(my_series)

        # convert column "a" of a DataFrame
        df["a"] = pd.to_numeric(df["a"])

        You can also use it to convert multiple columns of a DataFrame via the apply() method:

        # convert all columns of DataFrame
        df = df.apply(pd.to_numeric) # convert all columns of DataFrame

        # convert just columns "a" and "b"
        df[["a", "b"]] = df[["a", "b"]].apply(pd.to_numeric)




        # convert all DataFrame columns to the int64 dtype
        df = df.astype(int)

        # convert column "a" to int64 dtype and "b" to complex type
        df = df.astype({"a": int, "b": complex})

        # convert Series to float16 type
        s = s.astype(np.float16)

        # convert Series to Python strings
        s = s.astype(str)




train.astype({"Credit_History":object}).dtypes

train.groupby(cols[4])['Loan_Status'].count()






cols = ['ApplicantIncome', 'CoapplicantIncome', 'LoanAmount']

for col in cols:
    mean, std = train[col].mean(), train[col].std()
    median = train[col].loc[(train[col] - mean).abs() < 2*std].median()
    # fill null values with median
    train[col+'_feature'] = train[col].fillna(median)
    test[col+'_feature'] = test[col].fillna(median)
    # replace outlier with median
    train[col+'_feature'] = np.where((train[col + '_feature'] - mean).abs() > 2*std, median,train[col+'_feature'])
    test[col+'_feature'] = np.where((test[col+'_feature'] - mean).abs() > 2*std, median,test[col+'_feature'])



cols = ['ApplicantIncome_feature', 'CoapplicantIncome_feature', 'LoanAmount_feature']
W = 16
H = 10
fig, m_axs = plt.subplots(3,7, figsize = (W,H))
# m_axs = m_axs.flatten().T
for i in range(3):
    m_axs[i,0].plot(train[cols[i]])
#     m_axs[i,1].plot(train[cols[i]])
#     sns.boxplot(train[cols[i]],  orient='h' , ax=m_axs[i,1])
    sns.distplot(train[cols[i]], ax=m_axs[i,1])
#     sns.histplot(np.log(temp[cols[i]]), ax=m_axs[i,2])
    m_axs[i,2].hist(train[cols[i]])
    m_axs[i,3].plot(test[cols[i]])
    m_axs[i,4].hist(test[cols[i]])
    m_axs[i,5].plot(np.log(1e-9+train[cols[i]]))
    waste = np.log(1e-9+train[cols[i]])
#     print(waste.shape)
    m_axs[i,6].hist(waste)

