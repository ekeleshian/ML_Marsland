# Ch 3 Summary

This chapter provides a comprehensive guide to a very important algorithm in Machine Learning, perceptron.  To me, perceptron can be seen both as a curse and a blessing.  A curse because it was doubted amongst many scientists about its applicability, and a blessing because it became the setting stone for multi layer neural networks, aka deep learning.  The last bit of the chapter introduces another machine learning method, linear regression, and shows how perceptron is not the only candidate for generating predictions with the Pima Natives dataset.

The main gist here is that machine learning algorithms have a particular work flow: decide, act, evaluate.  Within each component is a comprehensive and statistically grounded set of instructions to conduct.  For instance, under the decision stage involves the careful task of data preprocessing, like visualizing the data, normalizing values, etc. 

Some key notes:

* Perceptron's complexity is speed O(mn), m = sample size, n = output size
* The logical operator XOR isn't learned in perceptron model if the dimension is 2.  However, if you bump it up to the third dimension, perceptron works on XOR.  
* The above insight sheds light on the fact that any linearly separable dataset can be trained successfully with perceptron.  Another way of saying is that the algorithm converges after T iterations, T having a discrete lower bound.  
* What perceptron tries to do is to find a straight line between one case against the other cases.  
* It is always possible to separate out two classes with a linear function, provided that you project the data into the correct set of dimensions (which hints at what **kernel classifiers** in **SVMs**.)