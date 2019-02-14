# Ch 6 Summary

## Dimensionality Reduction

The practice of reducing dimensions in your feature space is one way instance of making your data more intepretable and hence can be used to answer all or some of the following questions: 

1) Are some features redundant, insofar as they're not correlated with the output and are just noise?

2) If we applied some transformation to the data, like changing the coordinate system, can we derive new features from the old ones?  If so, how can we identify those features that are useful?

3) Can we allow fewer features being used to group together similar datapoints and hence perform clustering?


The chapter covers a few methods which are coded up and demonstrated in this chapter's notebook. I will summarize two of the algorithms. 

## LDA

* The insight from LDA is the claim that covariance can tell us something about the **scatter** of the dataset.  Particularly, there are two types of scatters to compute in order to use its alogirthm:  **scatter within** and **scatter between**.  **scatter within** tells you the spread of the datapoints that share the same class, and **scatter between** tells you the spread of the datapoints between each classes.  Ideally, you'd want S_w to be small, because that would represent datapoints that are tightly clustered together in each class.  Furthemore, you'd want S_b to be large, because that would represent clusters of data that are nicely separated out.  So, the goal of the algorithm is the maximize the ratio S_b/S_w, and then project that onto a smaller dimensional space.  

*  Merely maximizing over this ratio doesn't guarantee an appropriate projection, though.  Therefore, we have to add on a parameter, w, where you multiply w\*w.T on both S_w and S_b, use the quotient rule to differentiate the ratio w.r.t w, set it equal to zero to get S_w\*w  = (w.T\*S_w\*w)/(w.T\*S_b\*w).  Finding this optimal value is not easy and requires finidng the eigenvectors of S_b/S_w.  The corresponding eigenvalues that are genereated will tell you how much of an impact each feature has on the data.  You may safely ignore those eigenvalues that are close to zero, therefore reducing the dimensionality. 


## PCA 
* Unlike LDA, PCA doesn't need to know the labels.  The goal with PCA is to find the principal components of your data.  A principal component is the direction with the largest variation in the data.  The idea is that you choose the direction with the largest variation, place an axis in that direction, and then look at the variation that remains and choose another axis that is orthogonal to the first one and covers as muchof teh remaining variation as possible.  It then reiterates this until it has run out of possible axes.   

* So the algorithm works as follows: 
    * Write your datapoints as row vectors
    * put these vectors in a matrix **X**
    * Center the data by subtracting off the mean of each column putting into matrix **B**
    * compute the covariance matrix C = (1/N)**B**.T**B**, where N is the number of datapoints
    * Compute the eigenvalues and eigenvectors of C, so **V**^-1**C****V** = **D** where **V** holds the eigenvectors of **C** and **D** is the *MxM* diagonal eigenvalue matrix
    * Sort the columsn of **D** inroder order of decreasing eigenvalues, and apply the same order on the eigenvectors of **V**
    * reject those with eigenvalues less than some eta, leaving L dimensions in the data. 