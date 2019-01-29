#Ch 4 Summary

Percetron is great, but can only work for linearly separable problems.  Most interesting problems aren't linearly separable, though.  One way to work with the complexity of the data is by adding more layers of nodes to the network.  This is the main idea for Multi-Layer Perceptron (or MLP). 


Just like Perceptrons, MLP is the process of working out what the outputs are for the given inputs and current weights, and then updating the weights according to the error, which is a function of the difference between the outputs and the targets.   Just like perceptrons, you have an activation function defined for each layer that determines the behavior of a neuron.  Just like perceptrons, there are bias terms added to each layer.  


Not like perceptrons, MLP goes through a process of back propagation in order to minimize loss.  The weights get updated by traversing backwards into the network, performing gradients.  To figure out which weights affected the error, you take the gradient of the loss function (which is typically sum of squares) with respect to each weight. This gradient tells you the direction it increases (if positive) or decreases the most.  Since the goal is to minimize the loss function, we follow the direction of the gradient with some step size. 


With back propagation, there are further distinctions that arise comparing MLP with perceptron.  Unlike perceptrons, MLP's activation function should contain certain properties in order for gradient descent to work.  First, the activation function should be continuous, so that it's actually differentiable.  If it's not differentiable at all points in the domain space of the activation function, then back propagation won't work.  Second, which is a general requirement that all optimal models should have, is that the loss function should have nice differentiable properties to alleviate some of the hefty computational work.  Afterall, if there are many layers in the network, back propagation can become a very expensive, and hence 'not production ready'.  MLP can have other constraints to consider, but it depends on the type of loss function and gradient descent you choose when training the model. 


What continually boggles my mind still is the powerful affect certain simple mathematical properties have, particularly those that were learned in high school.  I think back propagation is so cool because its main job is totally dependent on the chain rule.  When traversing backwards into the neural network, you start updating weights from the last layer.  The last layer only knows about its input, its weights, and its outputs.  It doesn't know anything about prior weights.  Similarily, the first layer doesn't know anything about the targets, it just knows its input, its weights, and its outputs. But when you're trying to optimize for the whole system, you want a holistic approach, where you want the first layer to know the entire series of cause-and-effects that led to its weight being the value that it is.  This is where chain rule comes into play.


Chain rule in pseudo math terms can be explained like this: 

Suppose you have a neural network with the given architecture:  first layer (L1), hidden layer (L2), output layer (Y).  Since gradient descent happens when you traverse the network backwards, you will first need to update the weights from L2. Say you had to update its first weight, call it W1L2.  How much should you change W1L2? This depends on how W1L2 affected the network as a whole.  Since W1L2 only affected the network at its last stage, the chain rule will allow the computation of its gradient to take into account this one-step affect.  You continue to update the weights of L2 in this manner.  But what happens to the weights of L1?  Suppose you're at W1L1.  How did W1L1 affect the network as a whole?  It affected it in two stages, first by affecting the weights of L2, and then implicitly affecting the esimated targets.  Therefore, to compute the gradient of W1L1, the chain rule will account for explicit affects (affects right after leaving the node) and implicit affects (trailing affects that occur after leaving the node). 


## Other Useful Facts about MLP
* Choosing the initial weights requires some thought, as the neural network as a whole can be affected based on these weights.  Afterall, weights affect activation functions, and activation functions affect end results.  For instance, if you choose to initialize all of your weights to 1, then all corresponding activation functions will fire up, which can lead to skewed results.  It's important to randomize and normalize your weights, and to do so after each epoch so that the network doesn't end up memorizing weird nuanced things that aren't related to the general problem.
* Setting up your weight updates in mini batches can give the model a chance to leave local minimum
* Adding a momentum factor to your weight update equation can also give the model a chance to find global minimum.  For instance, you can add on a fixed term that represents how previous weight changes contribute to the current weight change. 
*  The network should make large-scale changes to weights in the beginning, when weights are random.  If it's making large weight changes later, you know something is wrong with your model.  One way to improve this is by integrating the second order derivatives of the error w.r.t. weights, as opposed to merely accounting for the first oder derivatives.
* amount of parameters in your network can explode if you have many hidden layers.  For each hidden layer, there are (L+1)\*M + (M+1)\*N weights, were L is number of inputs, M is the number of nodes in the hidden layer, and N is the number of nodes in the output layer.  All of these weights must be adjusted and reparameterized, and ideally you should have training data that is 10 times more than your parameter space.  You can imagine how computationaly expensive it can be to do neural network training. 
* Mathematical phenomenon known as Universal Approximation Theorem states that a neural network with one hidden layer suffices, as long as there are no constraints on how many nodes there can be assigned to that layer.  Promising theorem, as finding the right number of hidden layers with the right number of nodes can be super hard.  This theorem allows you to only focus on finding the right number of nodes.  
*  Finding the proper time to stop the training is also a super important concept.  If you train your network for too long, the learning will essentially become memorizing, which will hence not be generalizable. In fact, this is a classical case of *overfitting*.  That's why you should always have a validation set to use to evaluate your model to see how generalizable it is and its degree of overfitting. 
* an alternative to the sum-of-squares loss function is cross-entropy.  Cross-entropy works for classification problems and complements nicely with the softmax activation function in terms of finding its derivative. 








