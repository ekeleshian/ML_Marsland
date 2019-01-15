# Ch 2 Summary

Chapter two's purpose is such:  What are some basic properties about data before and after training? 

## Terminology 
There is a lot of terminology in this chapter.  I figure it's best to apply them all in an example.

*Use Case 1*: Data on MOOCs is given to you. Each row represents a MOOC user, and each column is some info on the user.  The columns are: number of minutes user is on website, number of unique classes completed, number of unique classes currently enrolled, last time user logged in, list of class names, number of times user posted comments on website, list of grades from completed classes.

Suppose I want to predict whether a user will continue using the MOOC or not.  In this case, the **target** is a yes or no question based on the column *number of unique classes currently enrolled*. For example, if user X is not enrolled in any classes currently, then user X's target would be 0.  Since this target value had to be deduced from the data, we would have to insert this column of 1's and 0's by simply coding it up with an if else condition.  The **inputs** would be all columns that are relevant to the target; since every column relates to user retention, every column will be part of the input.  The **weights** would be the values deduced after training, which represent the degree of impact that feature has on the output.  The **outputs** would be the results after training, in this case, a 0 or 1 for each sample.  The goal for generating predictions is to minimize the **error**, or the discrepancy between the outputs and targets. 

The **feature space** or **weight space** is the set of all inputs in the model.  The **number of dimensions** or **dimensionality** is the number of inputs, so in our case it's at least 7. This number is sometimes not explicitly determined, hence I say *at least*.  For our case, since not all our data is quanititative, we'd have to convert the ones that aren't, and this will inevitably increase the feature space.  For instance, 'list of class names' would have to get **one-hot-encoded** which means that for every unique class in this dataset, there will be a new column that would represent whether or not a student is enrolled in that class.  You can imagine now that the feature space can be expanded up to the number of classes Udacity has to offer.  This can be extremely problematic. 

**The curse of dimensionality** is a valid concern for this use case, as we have two qualitative features that could be expanded and one-hot-encoded.  The curse of dimensionality is a mathematical phenomenon that states that as dimensions increase, the data points that are embedded in this feature space would be so sparse that it would be much more difficult to determine the decision boundary. In fact, the rate of increase in the dimension space grows exponentially, so you would exponentially more data in order to fill the sparseness.

To train your data, you would have to choose a statistics algorithm on a subset of your dataset.  Typically you take 60% of your data as your **training set**, 20% as your **validation set** and the other 20% as your **test set**.  The training set is the data that you use to train your algorithm.  The validation set keeps track on how well your model is doing.  YOU NEVER TRAIN ON THE TEST SET.  The test set is the data that you evaluate at the end, i.e. the final results.  You can think of the validation set as sort of a pseudo test set, as you use to it to assess and tweak your algorithm.  

If this dataset is small, you can use **k-fold cross-validation**.  This practice is such that you partition your dataset into K subsets, one subset is used as a validation set, while the algorithm is trained on the rest of the data.  Then, you repeat this process by choosing another one of those K subsets as a validation set, while training the rest of the data.  Then you choose the model that produces the lowest validation error to test and use.  

When you evaluate your model, there are various accuracy metrics to analyze.  First you have the **confusion matrix** that takes tally on target and output results.  In our case, this matrix would consist of two rows and two columns, rows depicting the target values (user actually continues MOOC, user actually doesn't continue MOOC) and columns depicting the output results (user theoretically continues MOOC, user doesn't theoretically continues MOOC). The goal is to converge the theoretical results with the actual results as much as possible, which would result in maximizing the diagonal values of this matrix. 

The confusion matrix measures the **accuracy** of your model.  In math terms, it's simply # of times target = output divided by all predictions.  Accuracy, though, is not the only metric to use when assessing the performance of the results.  **Recall** for instance measures the degree of how well the model does in finding all positive results. In our instance, this would be the ratio of # of times the model correctly labelled instances when a user continues with a MOOC and # of all instances when a user actually continues with a MOOC. On the other hand, the **precision** measures the tendency of the model labeling the positive result.  In our case, the positive result would be when a user continues with a MOOC. Therefore, precision would be the number of times the model correctly labelled this positive result divided by the total number of instances the model labelled the positive result.  

**Precision** is a metric that measures the positive result relative to all theoretical positive occurences.  **Recall** is a metric that measures the positive result relative to all actual positive occurrences. 

The total number of theoretical positive occurences = True Positives + False Positives (i.e. correctly labelling an output as positive plus incorrectly labelling an output as positive). 

The total number of actual positive ocurrences = True Positives + False Negatives (i.e. correctly labelling an output as positive plus incorrectly labelling an output as negative).

**Recall** and **precision** kind of work inversely.  If your model tends to label more positives than negatives, then precision will be high since FP will be high.  But if FP is high, then FN will most likely decrease.  The two metrics can often be tied together with the F1 measure = 2\*(precision\*recall)/(precision+recall).


The **ROC** curve and **AUC** jointly help you determine whether your algorithm is strong in making correct predictions.  The goal is to get the AUC as close to 1 as possible.  The idea is that you want to increase your true positive rate (i.e. recall) while decreasing the false positive rate.  

## Probabilities

Turning data into probabilities helps make predictions easier.  The goal, in general, is to find the *posterior probability*, i.e. P(C|X), given the fact that there is prior knowledge about your classes and features, i.e. you know what P(C) is and P(X|C).  **Bayes Rule** helps you find the posterior probability by the following formula:  P(C|X) = P(X|C)P(C)/P(X).  You then assign each observation to one of the classes by picking the class C where its posterior probability is the highest amongst all C's posterior probabilities. This method of determining a class based on the highest liklihood is called the MAP (maximum a posteriori) method. The **Naive Bayes Classifier**  is exactly the MAP classification.  This classifier works really well assuming that all features are conditionally independent of each other, i.e. P(**X**|C) = P(X1| C)\*P(X2| C)\*...\*P(Xn| C).  


## Variance and Covariance

**Variance** is simply the spread of your data in relation to the mean.  **Covariance** measures how two variables vary together.  If two variables are *independent*, then their covariance is 0.  If there is some correlation between two variables, then their covariance is either close to -1 or close to 1.  **Mahalanobis distance** measures the distance between a point to its mean in relation to the variance.  

## Probability Distributions

The spread of your data typically follows a bell curve, AKA **Gaussian distribution**.  This distribution is deduced from the **Central Limit Theorem** which states that lots of small random numbers will add up to something Gaussian. 


## Bias-Variance Trade-Off:
A model can be bad for two different reasons:  either it's not accurate and doesn't match the data well (bias problem) or it's not very precise and there's a lot of variation (variance). When the data overfits, it has really high variance and low bias.  Bias measures how far off in general predictions are from the correct values. Variance is how much predictions vary with each other.
Mathematically explained:  E[(y* - h(**x**\*))^2] = noise^2 + variance + bias^2.

