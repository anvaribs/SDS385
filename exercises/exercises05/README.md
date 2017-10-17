# exercises 5
This directory hosts all the files related to the fifth homework.
I will add all the related details to this document. Howver, all the solutions would go into the following files directly:

* [exercises05-SDS385.tex](exercises05-SDS385.tex)
* [exercises05-solutions.pdf](exercises05-solutions.pdf)


**Note1:**  In this exercise, I am going to use the [wdbc.csv](https://github.com/anvaribs/SDS385/tree/master/data/wdbc.csv) dataset. I am also going to use some other datasets to test my implementation. I will add all those datasets to this repo. 

**Note2:** Please refer to the iPython notebook for the implementations: [stochastic_gradient_descent.ipynb](src/stochastic_gradient_descent.ipynb).

## Exercises 5: Sparsity

[Link here.](exercises05-SDS385.pdf)

In many problems, we wish to impose _sparsity_ on the parameters of a statistical model -- that is, the assumption that some parameters are zero. In this set of exercises, we will learn a few basic ideas that are important for thinking about sparse statistical models at scale.

Please finish reading Chapter 3.4 of [The Elements of Statistical Learning](http://statweb.stanford.edu/~tibs/ElemStatLearn/), although feel free to skip the part about "Least angle regression."  The key things to take away from this reading are:  
- the lasso  
- the idea of the lasso solution path (Figure 3.10)  
- the degrees of freedom for the lasso (page 77)

Note that we will work the lasso objective in "Lagrangian form" (Equation 3.52).  If you want a short overview of how the software you'll be using on this set of exercises actually fits the lasso, see Chapter 3.8.6 (Pathwise Coordinate Optimization), or the paper below for more detail.  But as you'll see, it's super fast.

### Extended reading

The following papers treat some of the issues that arise in lasso regression in much greater detail.  They are optional, but provide nice background.

- [The original paper on the lasso](http://statweb.stanford.edu/~tibs/lasso/lasso.pdf) 
- [Paper on pathwise coordinate optimization](http://arxiv.org/pdf/0708.1485.pdf)  
- ["Degrees of freedom" of the lasso fit](https://projecteuclid.org/euclid.aos/1194461726)  
- [Estimating the residual variance from the lasso fit](https://arxiv.org/abs/1311.5274).  Note that in the exercises we use their Equation 2 in our definition of CP.  
- [Estimating prediction error](https://people.eecs.berkeley.edu/~jordan/sail/readings/archive/efron_Cp.pdf).  

