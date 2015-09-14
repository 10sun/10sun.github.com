---
layout : post
category : LearningNote
tags : [MachineLearning, Basis]
---
{% include JB/setup %}

**Chapter 1. Introduction**

- *Definition*:
    + *Machine Learning*: A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E. - *Tom Mitchell*.
    + *Supervised Learning*: given a dataset and knowing what the correct output should look like, supervised learning tries to find the relationship between the input and output.
        * It is categorized into "*regression*" and "*classification*" problems.
    + *Unsupervised Learning*: Unsupervised learning derives structure from data where we don't necessarily know the effect of the variables, approaching problems with little or no idea what our results should look like.
    
**Chapter 2. Linear Regression with One Variable**

- *Definition*:
    + *Univariable linear regression*: linear regression with one variable is also known as "univariable linear regression". It is used to predict a signle output value from a single input value.
    + *Cost function*: it measures the accuracy of our hypothesis function. 

<!--more-->

- *Notes*:
    + Hypothesis function:
        $$ h_{\theta}(x) = \theta_0 + \theta_1 x$$
        By giving input '\\(x\\)' to \\(h_{\theta}(x)\\), we can get an output 'y' as the predict value.

    + Cost function: It takes an average of all the results of hypothesis with inputs from x's compared to the actual output y's. 
        $$ J(\theta_0,\theta_1) = \frac{1}{2m} \sum_{i = 1}^{m}(h_{\theta}(x^{(i)}) - y^{(i)})^2 $$
    + Gradient Descent: A way to automatically improve the hypothesis function. The way to do is taking the *derivative* of the cost function. The slope of the tangent is the derivative at that point and it will give us a direction to move towards. We make steps down that derivative by the parameter \\(\alpha\\), called the *learning rate*. The gradient descent equation is:</br>
        **repeat until convergence:**
        \\( \theta_j := \theta_j - \alpha \frac{\partial }{\partial \theta_{j}} J(\theta_0, \theta_1)\\)
        for  \\(j = 0\\) and \\(j = 1\\).
        Intuitively, this could be thought of as:
        **repeat until convergence:**
        \\( \theta_j := \theta_j - \alpha\\) [Slope of tangent, aka derivative]
    + Gradient Descent for Linear Regression: Replacing the \\(J(\theta_0, \theta_1)\\) with the actual cost function, we could get the gradient descent rule for linear regression:</br>
        **repeat until convergence:**
        {</br>
           $$ \theta_0 := \theta_0 - \alpha \frac{1}{m}\sum_{i=1}^m(h_{\theta}(x^{(i)}) - y^{(i)})$$
        </br>
           $$ \theta_1 := \theta_1 - \alpha \frac{1}{m}\sum_{i=1}^m((h_{\theta}(x^{(i)}) - y^{(i)})x^{(i)})$$
        } </br>
        where m is the size of the training set, \\(\theta_0\\) as a constant that will be changing simultaneously with \\(\theta_1\\) and \\(x^{(i)}\\), \\(y^{(i)}\\) are values of the given training set (data).

**Chapter 6. Logistic Regression**

- Notes:
    + Logistic regression cost function:
        $$Cost(h_{\theta}(x), y) = \begin{cases}
 & -log(h_{\theta}(x)), y = 1
 & -log(1 - h_{\theta}(x)), y = 0 
\end{cases}$$
