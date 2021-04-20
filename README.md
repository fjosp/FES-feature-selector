# FES-feature-selector

## Overview

This repository implements a framework for evaluating different feature selection methods. We provide a baseline **permutation importance** [2] method in our pipeline (using implementation from sklearn) as well as implementations of two more recent methods:  **Normalised Iterative Hard Thresholding** [1] and **Simultaneous Feature and Feature Group Selection through Hard Thresholding** [3]. The pipeline allows to perform evaluation on both synthetic and real data.

## Baseline method

### Permutation importance

Permutation importance is an approach to compute feature importances for anyblack-box estimator by measuring the decrease of a score when a feature is notavailable.  Permutation importance is calculated after a model has been fitted (i.e., the estimator is required to be a fitted estimator compatible with scorer).

This method contains the following steps:

* A baseline metric, defined by scoring, is evaluated on a data set defined by the X, where X can be the data set used to train the estimator or ahold-out set;
* A feature column from the validation set is permuted and the metric is evaluated again;
* The difference between the baseline metric and metric from permutating the feature column is the permutation importance. 



## Implemented methods

### Normalised Iterative Hard Thresholding

The algorithm searches for ![\Large \hat{x}^{n+1}](https://latex.codecogs.com/gif.latex?\dpi{120}&space;\hat{x}^{n&plus;1}) starting from ![\Large \hat{x}^0 = 0](https://latex.codecogs.com/gif.latex?\dpi{120}&space;\hat{x}^0&space;=&space;0) by applying the iterative procedure below where ![\Large H_K()](https://latex.codecogs.com/gif.latex?\dpi{120}&space;H_K()) is a non-linear operator that sets all but the top-k largest elements by their magnitude to zero and ![\Large \mu](https://latex.codecogs.com/gif.latex?\dpi{120}&space;\mu) is computed adaptively as described in [1].

![\Large \hat{x}^{n+1} = H_K(\hat{x}^n + \mu A^\top (y - A \hat{x}^n))](https://latex.codecogs.com/gif.latex?\dpi{150}&space;\hat{x}^{n&plus;1}&space;=&space;H_K(\hat{x}^n&space;&plus;&space;\mu&space;A^\top&space;(y&space;-&space;A&space;\hat{x}^n)))

Pros:
* Gives theoretical guarantees on convergence to a local minimum of the cost function
* Doesn't depend on the scaling of the design matrix ![\Large A](https://latex.codecogs.com/gif.latex?A)

Cons:
* Theoretical guarantees on convergence exist only if ![\Large A](https://latex.codecogs.com/gif.latex?A) that satisfies restricted isometry property 

### Simultaneous Feature and Feature Group Selection through Hard Thresholding

The algorithm employs the iterative procedure below where ![\Large f](https://latex.codecogs.com/gif.latex?f) is the objective loss function, ![\Large L](https://latex.codecogs.com/gif.latex?L) is found by line search and ![\Large SGHT()](https://latex.codecogs.com/gif.latex?SGHT()) stands for Sparse Group Hard Thresholding that is solved by dynamic programming as described in [3].

![\Large \hat{x}^{n+1} = SGHT(\hat{x}^n - \frac{1}{L} \nabla f(\hat{x}^n))](https://latex.codecogs.com/gif.latex?\dpi{150}&space;\hat{x}^{n&plus;1}&space;=&space;SGHT(\hat{x}^n&space;-&space;\frac{1}{L}&space;\nabla&space;f(\hat{x}^n)))

Pros:
* Line search on each iteration can be significantly sped up
* Gives theoretical guarantees on convergence to a local minimum of the cost function that is at least within ![\Large c||y-Ax^*||_2](https://latex.codecogs.com/gif.latex?c||y-Ax^*||_2) radius from globally optimal solution ![\Large x^*](https://latex.codecogs.com/gif.latex?x^*) for a certain constant ![\Large c](https://latex.codecogs.com/gif.latex?c)


Cons:
* Theoretical guarantees on convergence exist only if ![\Large A](https://latex.codecogs.com/gif.latex?A) that satisfies restricted isometry property

## Evaluation protocol

### Metrics

### Synthetic data

### Real data

## Team members roles

## References

[1]  T. Blumensath and M. E. Davies.  Normalized iterative hard thresholding:Guaranteed stability and performance.IEEE Journal of Selected Topics inSignal Processing, 4(2):298–309, 2010.

[2]  Leo Breiman.  Random forests.Machine Learning, 45(1):5–32, 2001.

[3]  Shuo Xiang, Tao Yang, and Jieping Ye.  Simultaneous feature and featuregroup selection through hard thresholding. InProceedings of the 20th ACMSIGKDD International Conference on Knowledge Discovery and Data Min-ing,  KDD  ’14,  page  532–541,  New  York,  NY,  USA,  2014.  Association  forComputing Machinery.
