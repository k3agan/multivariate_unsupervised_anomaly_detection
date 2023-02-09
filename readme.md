# Multivariate anomalies

Multivariate anomalies occur when the value sof various features, taken together seem anomalous even though the individual features d not take unuusual values. 

So in essence there might be outliers "hiding" in our dataset that might otherwise be left undetected with traditional univariate statistical methods. 

Isolation forests are able to isolate out anomalies very early on in the splitting process because the "random threshold" used for splitting has a large probability of lying in the empty space between the outlier and the data if the empty space is large enough. As a result, anomalies have shorte rpath lengths. So, the larger the empty space, the more likely it is for a randomly chosed split point to lie in that empty region. The resulting anomaly score is a calculated non-linear function of the "average path length' over all isolation trees. The path length is essentially the number of splits made by the isolation tree to isolate a point. 

The inputs to this algorithm (at least in sklearn) are :

n_estimators: number of trees
max_samples: number of data points fed into each tree during training
contamination: estimated fraction of anomalous datapoints (eg. 0.05 or 5%)
max_features: number of dimensions in the training data


What if we don't know the right contamination?

In this case we can either apply a univariate anomaly detection algorithm on the isolation forest decision function output or we can plot a histogram and manually select a threshold that "looks right". 

The problem with using "eyeballs" is the challenges of:
1.Scalability - isolation forests can use parallel processing during training and prediction, as all trees are trained independently of one another.
2. Interpretability - Individual trees in an isolation forest can be visualized to give the exact rule-chain to explain what made the model "think" it was an outlier. These rules can have wide ranging consequences for compliance/business. 
3. Flexibility - These models can capture outliers on higher dimensional distributions. 


SVM is another flexible model that can build non-linear boundaries to classify outliers accross high dimensional data. 