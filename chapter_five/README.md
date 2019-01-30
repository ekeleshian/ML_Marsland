# Ch 5 Summary

  The main idea with Radial Basis Functions (RBFs) is that weights are updated based on how close they are to a particular centroid.  The motivation stems from the notion of a receptive field from neuroscience.  Think about your eye and its receptive field, the retina.  When your eye hits light, it goes through your eye, hits the retina, and rods will detect the light.  But which rods will detect the light -- are these rods distributed across the entire retina or are they localised in a region based on the location the light came from?   If you think about these rods as nodes, their firing strength as weights, and the retina as the neural network, you can imagine that there are two unique models that come about from this quesion:  MLP and RBF respectively.  In actuality, the eye's functionality is more aligned with the latter option, that the light detection depends on a particular localization of rods.  If you have good eye vision, the weights of those localised rods will be high, whereas the weights of far away rods would be approaching zero. This is the idea of RBF.  The 'radial' part comes from the fact that you measure the distance between the input and how far it is from a centroid.  The 'basis function' comes from the fact that these distances can then be mapped on a gaussian with dimension D (D is the number of the centroids in your neural network), forming a basis function. 


  You may ask what are these centroids? You can use k-means on your input space, performing unsupervised learning to determine the centroids.  How many centroids do you need?  That's a tricky part with RBF's: the number of centroids is a hyperparameter.  Ideally, you'd want to test out your model with different numbers of centroids, and then pick that number that lead to the highest results.    

  Mathamatically speaking, here's RBF: 
  Assume each (x,y) in the dataset D influences h(x) the hypothesis based on ||x-mu|| where h(x) = summation(w_k\*exp(-gamma\*||x-mu_k||^2)).  The parameters we can tune are the weights, gamma, and the centroids.  


  There is reason why h(x) is the gaussian -- this is because it renders smooth weight updates as opposed to abrupt weight updates. It has been proven mathematically that the Gaussian generates the smoothest interpolation, so therefore we choose the gaussian to map these distances.  The number of centroids will determine the dimensionality of your basis functions.


  Weight updates are super easy and quick. If you look at its equation: h(x) = summation(w_k\*exp(-gamma\*||x-mu_k||^2)) and rewrite it in matrix form, you get h(x) = Phi\*w  ~~ y, where Phi = exp(-gamma\*||x-mu_k||^2) and ~~ y is an approximation of the actual target y.  With this form, you see that Phi is an NxK matrix, w is Kx1, and y is Nx1.  If we treat the approximation as an equation such that h(x) = y, you see that there are K equations, and K unknowns.  What's really great about RBF's is that the matrix Phi is psuedo-invertible, and therefore you can find the weights by simply finding the psuedo inverse, i.e. w = (Phi_transpose\*Phi)^-1\*Phi_transpose\*y) where y is the actual target.  This makes weight updates much faster, as opposed to performing back propagation and chain rule.


  


