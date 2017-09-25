## Excercises 2 ##

This directory hosts all the files related to the second homework.

I will add all the related details to this document. However, all the solutions would go into the following files directly:
* [exercises02-SDS385.tex](exercises02-SDS385.tex)
* [exercises02-solutions.pdf](exercises02-solutions.pdf)

**Note1:**  In this exercise, I am going to use the [wdbc.csv](https://github.com/anvaribs/SDS385/tree/master/data/wdbc.csv) dataset. I am also going to use some other datasets to test my implementation. I will add all those datasets to this repo. 

**Note2:** Please refer to the iPython notebook for the implementations: [Logistic_Regression_via_Stochastic_Gradient_Descent.ipynb](src/Logistic_Regression_via_Stochastic_Gradient_Descent.ipynb).




## Exercises 2: Online learning

[The goal in this exercise](exercises02-SDS385.pdf) to get some working code -- not necessarily fast or efficient code -- that fits a logistic-regression model by stochastic gradient descent (SGD).  The idea of SGD is to fit the model in such a way that we process only one observation at a time (or possibly a small handful of observations, called minibatches). This contrasts sharply with ordinary gradient descent or Newton's method, both of which are _batch methods_: they require that we process the entire data set as a batch in order to take a single step.  In future applications -- not quite yet -- SGD will even allow us to fit a model in such a way that we never have to load a full data set into your computer's working memory.  Instead we can just read it a chunk at a time off the hard drive.  This is very handy if you have more data than memory!

But as we'll see, getting stochastic-gradient descent right is tricky.  We'll learn the basics now, recognize the key issues, and save the more advanced stuff (for addressing those issues) for the next two sets of exercises.  

