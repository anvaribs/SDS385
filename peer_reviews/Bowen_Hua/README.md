# Peer Review: [Bowen Hua](https://github.com/bowenhua/SDS_385)

In this short code review, I am going through your codes for [assignment 5 - sparsity](https://github.com/bowenhua/SDS_385/blob/master/5_sparsity/lasso_CV.ipynb) and [assignment 6 - proximal gradient descient](https://github.com/bowenhua/SDS_385/blob/master/6_proximal_gradient/Proximal%20gradient%20method.ipynb) and try to comment on your overall approach, coding style and some short micro-comments about how you can improve your coding.

### General Comments on Overall Approach:

Generally, your code is very clean and readible. At the same time, you have tried to make it as concise as possible and it is most of the time a very good characteristic of a good programmer. It is great that you switched to ipython notebook after our discussion at the beginning of semester. Jupyter notebook, in my opinion, is a great tool for learning how to be a good data scientist. The way that you have combined text, code and plots make it a great combination for yourself in the first place (to come back to your code later and understand what is going on) and also for anyone else who wants to refer to your code and learn something from it or develop some code on top of it. Overally, you did a great job in these two exercises that I am reviewing. The fact that you have identified the big problem that you want to solve, and know how to break it down to bite-size problems that you know how to solve is great. That is a great skill that makes you a great programmer and data scientist later in your career.

### coding style:

As I meantioned earlier, I am so happy that our conversation at the beginning of semester lead to you using jupyter notebook in solving SDS assignment. Jupyter notebook is a great tool for both learning and developing. You code is very clear, and easy to follow. This is a great attribute if you want to go back later to your code and maybe to build something on top of it. 

It is great that you tried to break the code into smaller pieces that you know how to tackle. I really like the fact that you have tried to code some utility function at the beginning and use them later in your main solution. It makes the code very modular. For example:

```
def calc_grad(X,y,beta):
    grad = np.dot(np.dot(X.T, X), beta) - np.dot(X.T, y)
    return (2 / np.shape(X)[0]) * grad
}
```

and 

```
def calc_obj(X,y,beta,lam):
    """Objective function normalized""" 
    return (1 / np.shape(X)[0]) * (np.linalg.norm(y - np.dot(X, beta)))**2 + lam * np.sum(np.abs(beta))
```

One thing that I strongly suggest you do in these cases, is to write unit test for each function that you write. Even if you don't know what you should test about your function, you can always write unit test that for example assert that the dimension of the output is correct. Or maybe in this case, you can manually calculate the objective function for a simple input and write a unit test to make sure that your utility function is generating the result that you are expecting. 

One other thing that you can try is to use somebody else implementation of the same function or a slow, not optimized implementation of the same function to generate some output and use those for your test units.

The other thing is, wherever that is possible you have used an external library such as numpy, scipy, matplotlib and sklearn and did not reinvent the wheel which is a great coding habit. Great job overall. 


### Readibility of the code:
A lot of inline comments and also combining text and code makes your code very readible and comprehinsible. That fact that you have combined all the relevent pieces of code and function s into the same notebook cell makes your code very easy to follow and understand.


### some final micro-comments: 
The only thing that I can comment again is, testing, and testing and testing. In my humble opinion, there is always a way to test a piece of code. try to write as many unit tests as you can. At the end, for this small programming excercises, you probably would be able to find an open-source implementation of the same thing. Use those to test the overall result of you code, whether it is in the form of a loss vs iteration plot or anything else. That would give a confident to develop on top the that code and build something bigger using your already developed small pieces. Again, overall, you did a great job Bowen. Keep up the great work.

