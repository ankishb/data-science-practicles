## XGBOOST

for xgboost here is my steps, usually i can reach almost good parameters in a few steps,

initialize parameters such: eta = 0.1, depth= 10, subsample=1.0, minchildweight = 5, colsamplebytree = 0.2 (depends on feature size), set proper objective for the problem (reg:linear, reg:logistic or count:poisson for regression, binary:logistic or rank:pairwise for classification)

split %20 for validation, and prepare a watchlist for train and test set, set num_round too high such as 1000000 so you can see the valid prediction for any round value, if at some point test prediction error rises you can terminate the program running,

i) play to tune depth parameter, generally depth parameter is invariant to other parameters, i start from 10 after watching best error rate for initial parameters then i can compare the result for different parameters, change it 8, if error is higher then you can try 12 next time, if for 12 error is lower than 10 , so you can try 15 next time, if error is lower for 8 you would try 5 and so on.

ii) after finding best depth parameter, i tune for subsample parameter, i started from 1.0 then change it to 0.8 if error is higher then try 0.9 if still error is higher then i use 1.0, and so on.

iii) in this step i tune for min child_weight, same approach above,

iv) then i tune for colSamplebytree

v) now i descrease the eta to 0.05, and leave program running then get the optimum num_round (where error rate start to increase in watchlist progress),

after these step you can get roughly good parameters (i dont claim best ones), then you can play around these parameters.






"minimum sum of instance weight(hessian) needed in a child. If the tree partition step results in a leaf node with the sum of instance weight less than min_child_weight, then the building process will give up further partitioning.

Intuitively, this is the minimum number of samples that a node can represent in order to be split further. If there are fewer than min_child_weight samples at that node, the node becomes a leaf and is no longer split. This can help reduce the model complexity and prevent overfitting.



















