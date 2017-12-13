# Matrix Factorization Methods and their applications
For the purpose of the final project for the course “SDS385: Statistical Models for big data”, I am going to investigate problem of factorizing a matrix into the product of two smaller matrices (i.e., Matrix Factorization). Then I will move on to the non-negative matrix factorization, which differs from the ordinary matrix factorization by restricting all values of the data and model to be greater than zero. This allows for “parts-based learning” from data, of which topic modeling is a prime example. I will try to implement and present two standard NMF algorithms for this problem. 

After that, I will cover the fundamental matrix factorization technique called principle component analysis (PCA), a very useful dimensionality reduction approach. I will also present and implement some extension to the regular PCA such as probabilistic PCA for image denoising and inpainting and also kernel PCA for nonlinear dimensionality reduction.



## Introduction

Matrix factorization problem is an unsupervised learning problem. I will start by motivating the matrix factorization problem by first talking about collaborative filtering problem. The motivation for this type of model, is the object recommendation problem. Of course, there is no need to talk about the importance of the problem of matching consumers to products and many companies are interested to do well in this subject. 

We can often make these connections using user feedback about subsets of products. for example:

- Netflix asks its users to rate the movies that they watch 
- Amazon asks users to rate products and write some reviews about them.
- Yelp asks users to rate businesses, write reviews about them, and also upload pictures
- Youtube asks users to like/dislike a video and write comments about them

Recommendation systems often use this information to help recommend new things to customers that they may like. This is actually a very big complicated problem and there are many different strategies to solve this problem. One general subset of approaches is called **content filtering.** 

The way content filtering performs is it uses known information about the products and users to make profiles for each of them and at the end it matches those profiles to each other.  This approach is actually not using any of the users behavioral information and also it requires a lot of information that sometimes are difficult and expensive to collect.

A fundamentally different approach to solve the problem of object recommendation is **collaborative filtering (CF).** What CF does is, it use previous user’s inputs/behavior to make future recommendation, ignoring any sort of a priori user or object specific information. 

For an example for collaborative filtering, we can look at neighborhood-based approaches. In this kind of methods, CF:


1. Defines some sort of similarity score between each user and other users based on solely how much their overlapping ratings agree, then
2. based on these scores, let others “vote” on what each user would probably like.

Notice that there is no background information used by this method and exactly the same sort of method can be used for any recommendation system. Note also that content filtering approaches and collaborative filtering approaches are not mutually exclusive. Content filtering information can also be built into a CF system to improve it’s performance.

in location-based CF approaches, the algorithm tries to get an $$R^d$$ embedding for users and objects. The way that we learn these embedding is through **Matrix Factorization.**



## Matrix Factorization

To see how we can use matrix factorization to do object recommendation in a collaborative filtering setting, first let’s see how the data structure should look like. We assume that we have a matrix of ratings and by assuming that we have $$N_1$$ users and $$N_2$$ objects we setup our rating **matrix M** as below:

![Data Structure for the rating matrix M](https://d2mxuefqeaa7sj.cloudfront.net/s_B623DF4E3920788CF9583F4A05F5A41695A80A2EAF6D3C32053CFEE8F6F48876_1513196113550_Screenshot+2017-12-13+14.14.45.png)



Notice that in this kind of data structure for the rating matrix, the matrix will have many missing values. The goal of the Matrix Factorization algorithm here is to learn a low-rank factorization of this rating matrix using only the data that we have observed and ignoring all the data that we don’t have and then fill in all of these missing values. Finally we can use those predictions, and recommend highly rated objects among the predictions.




Our goal here is to factorize Matrix M. One approach to this is **Singular Value Decomposition.**

**Singular Value Decompisition**
Every matrix M can be written as M = $$USV^T$$, where $$U^TU = I$$, $$V^TV = I$$ and S is diagonal with $$S_{ii} \geq 0$$.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_B623DF4E3920788CF9583F4A05F5A41695A80A2EAF6D3C32053CFEE8F6F48876_1513198352056_Screenshot+2017-12-13+14.52.18.png)


We assume r = rank(M). When r is small, M has fewer “degrees of freedom”. A low-rank matrix factorization can restrict the degrees of freedom of how many different types of things we can model in matrix M. We are going to exploit this idea of low-rank matrix factorization in the collaborative filtering with matrix factorization.


We want to define a model for learning a low-rank factorization of M. It should:

1. Account for the fact that most values in M are missing.
2. It should be low-rank, where d << $$min\{{N_1, N_2}$$}
3. Learn a location $$u_i \in R^d$$ for user i and $$v_j \in R^d$$ for object j
![](https://d2mxuefqeaa7sj.cloudfront.net/s_B623DF4E3920788CF9583F4A05F5A41695A80A2EAF6D3C32053CFEE8F6F48876_1513200163379_Screenshot+2017-12-13+15.22.35.png)


To discuss more the idea of low-rank matrix and why we want to learn it, we can say that since there are a lot of missing data, by enforcing all the objects and users features to live in this low-rank d-dimensional space, we are in some sense enforcing there to be correlations between similar objects and similar users.

In the missing data problem, one particularly good model for learning low-rank factorization is called **Probabilistic Matrix Factorization.** Following, I am going into more details of this model.


## Probabilistic Matrix Factorization

Some pieces of notation to start with:


- Let the set $$\Omega$$ contain the pairs (i , j) that are observed: $$\Omega = \{(i,j): M_{ij}\  is\  measured.\}$$
- Let $$\Omega_{ui}$$ be the index set of objects rated by user i.
- Let $$\Omega_{vj}$$ be index set of users who rated object j.

Probabilistic Matrix Factorization assumes a **generative** model for the data. So for example, by assuming the normal prior for our model variables we would have:

For $$N_1$$ users and $$N_2$$ objects, generate

- **User locations:**           $$u_i \sim    N(0, \gamma^{-1}I)$$,      i = 1, …, $$N_1$$
- **Object locations:**       $$v_j \sim    N(0, \gamma^{-1}I)$$,      j = 1, …, $$N_2$$


Given these locations the distribution on the data is

                                          $$M_{ij} \sim N(u_i^Tv_j, \sigma^2)$$, for each $$(i,j) \in \Omega$$.
                                          
Note that since $$M_{ij}$$ is a rating, the Gaussian assumption is clearly wrong. However, the Gaussian is a convenient assumption. The algorithm is going to be easy to implement, and the model works well. 

                                     













# Refrences:
- A review of principal components analysis in [Introduction to Statistical Learning](http://www-bcf.usc.edu/~gareth/ISL/), Section 10.2.
- The paper ["A penalized matrix decomposition, with applications to sparse principal components and canonical correlation analysis"](https://faculty.washington.edu/dwitten/Papers/pmd.pdf), by Witten, Tibshirani, and Hastie.
- Optional: [more background](https://www.cs.cmu.edu/~venkatg/teaching/CStheory-infoage/book-chapter-4.pdf) on the singular value decomposition.
- Koren, Y., Robert B., and Volinsky, C.. “Matrix factorization techniques for recommender systems.” Computer 42.8 (2009): 30-37.



