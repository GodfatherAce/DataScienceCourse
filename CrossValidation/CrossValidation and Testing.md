Cross-Validation and Testing
==============================
In order to quantify the effects of bias and variance and construct the best possible estimator, we will split our training data into three parts: a training set, a cross-validation set, and a test set. As a general rule, the training set should be about 60% of the samples, and the cross-validation and test sets should be about 20% each.

The general idea is as follows. The model parameters (in our case, the coefficients of the polynomials) are learned using the training set as above. The error is evaluated on the cross-validation set, and the meta-parameters (in our case, the degree of the polynomial) are adjusted so that this cross-validation error is minimized. Finally, the labels are predicted for the test set. These labels are used to evaluate how well the algorithm can be expected to perform on unlabeled data.

Note Why do we need both a cross-validation set and a test set? Many machine learning practitioners use the same set of data as both a cross-validation set and a test set. This is not the best approach, for the same reasons we outlined above. Just as the parameters can be over-fit to the training data, the meta-parameters can be over-fit to the cross-validation data. For this reason, the minimal cross-validation error tends to under-estimate the error expected on a new set of data.
