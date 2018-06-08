# An Introduction to Statistical Learning
James, Witten, Hastie, Tibshirani
Kathryn Hamilton - May 2018

## Table of Contents
[1 Introduction](#introduction)
[2 Statistical Learning](#statistical-learning)
&nbsp;&nbsp;&nbsp;&nbsp;[2.1 What is Statistical Learning?](#what-is-statistical-learning)
&nbsp;&nbsp;&nbsp;&nbsp;[2.2 Assessing Model Accuracy](#assessing-model-accuracy)
[3 Linear Regression](#linear-regression)
&nbsp;&nbsp;&nbsp;&nbsp;[3.1 Simple Linear Regression](#simple-linear-regression)
&nbsp;&nbsp;&nbsp;&nbsp;[3.2 Multiple Linear Regression](#multiple-linear-regression)
&nbsp;&nbsp;&nbsp;&nbsp;[3.3 Other Consideration in the Regression Model](#other-consideration-in-the-regression-model)
&nbsp;&nbsp;&nbsp;&nbsp;[3.4 The Marketing Plan](#the-marketing-plan)
&nbsp;&nbsp;&nbsp;&nbsp;[3.5 Comparison of Linear Regression with K-Nearest Neighbors](#comparison-of-linear-regression-with-k-nearest-neighbors)
[4 Classification](#classification)
&nbsp;&nbsp;&nbsp;&nbsp;[4.1 An Overview of Classification](#an-overview-of-classification)
&nbsp;&nbsp;&nbsp;&nbsp;[4.2 Why Not Linear Regression?](#why-not-linear-regression)
&nbsp;&nbsp;&nbsp;&nbsp;[4.3 Logistic Regression](#logistic-regression)
&nbsp;&nbsp;&nbsp;&nbsp;[4.4 Linear Discriminant Analysis](#linear-discriminant-analysis)
&nbsp;&nbsp;&nbsp;&nbsp;[4.5 A Comparison of Classification Methods](#a-comparison-of-classification-methods)
[5 Resampling Methods](#resampling-methods)
&nbsp;&nbsp;&nbsp;&nbsp;[5.1 Cross-Validation](#cross-validation)
&nbsp;&nbsp;&nbsp;&nbsp;[5.2 The Bootstrap](#the-bootstrap)
[6 Linear Model Selection and Regularization](#linear-model-selection-and-regularization)
&nbsp;&nbsp;&nbsp;&nbsp;[6.1 Subset Selection](#subset-selection)
&nbsp;&nbsp;&nbsp;&nbsp;[6.2 Shrinkage Methods](#shrinkage-methods)
&nbsp;&nbsp;&nbsp;&nbsp;[6.3 Dimension Reduction Methods](#dimension-reduction-methods)
&nbsp;&nbsp;&nbsp;&nbsp;[6.4 Considerations in High Dimensions](#considerations-in-high-dimensions)
[7 Moving Beyond Linearity](#moving-beyond-linearity)
&nbsp;&nbsp;&nbsp;&nbsp;[7.1 Polynomial Regression](#polynomial-regression)
&nbsp;&nbsp;&nbsp;&nbsp;[7.2 Step Functions](#step-functions)
&nbsp;&nbsp;&nbsp;&nbsp;[7.3 Basis Functions](#basis-functions)
&nbsp;&nbsp;&nbsp;&nbsp;[7.4 Regression Splines](#regression-splines)
&nbsp;&nbsp;&nbsp;&nbsp;[7.5 Smoothing Splines](#smoothing-splines)
&nbsp;&nbsp;&nbsp;&nbsp;[7.6 Local Regression](#local-regression)
&nbsp;&nbsp;&nbsp;&nbsp;[7.7 Generalized Additive Models](#generalized-additive-models)
[8 Tree-Based Methods](#tree-based-methods)
&nbsp;&nbsp;&nbsp;&nbsp;[8.1 The Basics of Decision Trees](#the-basics-of-decision-trees)
&nbsp;&nbsp;&nbsp;&nbsp;[8.2 Bagging, Random Forests, Boosting](#bagging-random-forests-boosting)
[9 Support Vector Machines](#support-vector-machines)
&nbsp;&nbsp;&nbsp;&nbsp;[9.1 Maximal Margin Classifier](#maximal-margin-classifier)
&nbsp;&nbsp;&nbsp;&nbsp;[9.2 Support Vector Classifiers](#support-vector-classifiers)
&nbsp;&nbsp;&nbsp;&nbsp;[9.3 Support Vector Machines](#support-vector-machines-1)
&nbsp;&nbsp;&nbsp;&nbsp;[9.4 SVMs with More than Two Classes](#svms-with-more-than-two-classes)
&nbsp;&nbsp;&nbsp;&nbsp;[9.5 Relationship to Logistic Regression](#relationship-to-logistic-regression)
[10 Unsupervised Learning](#unsupervised-learning)
&nbsp;&nbsp;&nbsp;&nbsp;[10.1 The Challenge of Unsupervised Learning](#the-challenge-of-unsupervised-learning)
&nbsp;&nbsp;&nbsp;&nbsp;[10.2 Principal Components Analysis](#principal-components-analysis)
&nbsp;&nbsp;&nbsp;&nbsp;[10.3 Clustering Methods](#clustering-methods)

## 1 Introduction 

Statistical learning is a set of tools for modeling and understanding complex datasets. These tools can be classified as **supervised** or **unsupervised**.

* **Supervised** learning predicts an output based on one or more inputs. Examples include linear regression and logistic regression.
* **Unsupervised** learning has inputs and no supervised output, but can still be used to learn relationships and structure. The primary example of this is cluster analysis.

[Back to Table of Contents](#table-of-contents)

## 2 Statistical Learning

[2.1 What is Statistical Learning?](#what-is-statistical-learning)
[2.2 Assessing Model Accuracy](#assessing-model-accuracy)
[Back to Table of Contents](#table-of-contents)

### 2.1 What is Statistical Learning?
#### The Learning Problem

For input variables $X_1, X_2, \dots , X_p$ and output response $Y$ we assume that there is some relationship $Y=f(X)+\epsilon$, where $\epsilon$ is a zero-mean random error term independent of $X$. 

*Statistical learning is a set of approaches to estimate $f$.* We call this estimate $\hat{f}$.

Variables in a statistical learning problem are either **quantitative** or **qualitative**. We tend to refer to problems with a quantitative response as **regression** problems while those involving a qualitative response are referred to as **classification** or **categorical** problems.

#### Accuracy

The accuracy of $\hat{f}$ depends on both **reducible error** and **irreducible error**. This book focuses on methods of reducing reducible error.

* **Reducible error** is introduced when $\hat{f}$ is not a perfect estimate for $f$ ($\hat{f} \neq f$)
* **Irreducible error** is the result of unmeasured variables that are useful in predicting $Y$ ($\epsilon \not\perp\!\!\!\perp Y$) and any other unmeasurable variation ($\epsilon \neq 0$).

#### Motivation

There are two motivations to estimate $f$: **prediction** and **inference**.

In situations where $X$ is readily available but $Y$ is not, we can **predict** $Y$ to be $\hat{Y} = \hat{f}(X)$. In general, $\hat{f}$ is not a perfect estimate for $f$ because it cannot predict the irreducible error $\epsilon$. Here we can treat $\hat{f}$ as a black box.

In other situations, we are interested in understanding the way that $Y$ is affected as $X$ changes. This is called **inference**. We still need to estimate $f$ but cannot treat $\hat{f}$ as a black box as we are interested in understanding the relationship between $X$ and $Y$ as opposed to predicting $Y$. We may want to know:  

* Which predictors are most strongly associated to the response?
* What is the relationship between the response and each predictors?
* Which relationships can be summarized using a linear equation? Which are more complicated?

*Many problems fall into both of these categories.* For example, consider an advertising firm that would like to know which form of media advertising generates the largest boost in sales (inference), and how much of an increase in sales would occur given an advertising increase in that specific media (prediction).

*The best method for estimating $f$ depends on the goal and what you are trying to achieve.*

#### Parametric and Non-Parametric Methods

Most statistical learning methods can be classified as either **parametric** or **non-parametric**.

**Parametric methods** first make an assumption about the form of $f$, which typical involves some parameters, and then uses training data to fit the model and thus provide estimate values for each parameter. Assuming a parametric form simplifies the problem of estimating $f$, but can be dangerous if the model chosen does not represent the data sufficiently well or is overly complicated.

**Non-parametric methods** do not make an explicit assumption about the form of $f$. They seek an estimate of $f$ by getting as close to the data as possible while limiting noise and overfitting. The advantage is that they can be fit accurately to a wide range of possible shapes, thus avoiding the possibility of poor fit. However, solving these types of problems are can be very difficult and the results are often not easy to interpret.

#### Trade off: Interpretability vs Flexibility

Various statistical methods have a trade off between **interpretability** and **flexibility**. Inference problems favor restrictive models with higher interpretability. Prediction problems favor more flexible models as they are more likely to be accurate (at the risk of overfitting) and thus provide better predictions. Some exemplary methods are as follows:

* **Subset Selection** and **Lasso** have high interpretability and have low flexibility.
* **Bagging**, **Boosting** and **Support Vector Machines** have high flexibility and low interpretability.
* **Least Squares**, **Generalized Additive Models** and **Trees** have moderate flexibility and moderate interpretability.

[Back to 2 Statistical Learning](#statistical-learning)
[Back to Table of Contents](#table-of-contents)

### 2.2 Assessing Model Accuracy

*There is no free lunch* in statistics: no one method dominates all others over all possible datasets. Hence, it is an important task to decide which method produces the best results for the particular dataset at hand.

To measure how well predictions match observed data we use the following error functions, where $y_i$ is the observed value and $\hat{f}(x_i)$ is the predicted value of the response:

* **Mean Squared Error** (MSE) for regression problems, $MSE=\frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{f}(x_i))^2$.
* **Error Rate** for classification problems, $\text{Error rate}=\frac{1}{n}\sum_{i=1}^{n} I_{(y_i)\neq \hat{f}(x_i)}$.

Models with smaller error predict more accurately that those with larger error.

These accuracy metrics are meant to be performed on *unseen data that has not been used to fit the model*, known as the test set. In practice, computing the test error can be very difficult as response data is not usually available. Sometimes the training error can approximate the test error. Otherwise, **cross-validation** or **partitioning** must be used to estimate the test error using the training data.

------

In order to minimize expected test error, the chosen statistical method *must simulatenously acheive* **low variance** *and* **low bias** where:

* **Variance** is the amount by which $\hat{f}$ would change if the model were fitted using a different training set.
* **Bias** is the error that is introduced by approximating a real-life problem with a simplified model.

------

Test error rate is minimized, on average, by a classifier that *assigns each observation to the most likely class*.

The **Bayes Classifier** for quantitative responses operates under this premise, by predicting the class of $x_0$ to be $j$ when $P(Y=j \, | \, X=x_0)$ is the greatest out of all possible classes.

The **Bayes error rate** is $1-E\left(\max_j P(Y=j \, | \, X)\right)$ which is analogous to the irreducible error.

**K-Nearest Neighbors** (KNN) follows the same theory for qualitative responses. However, conditional probability can only be estimated rather than calculated directly so this method is weaker than the Bayes Classifier. 

KNN identifies the K closest observations to $x_0$, called $N_0$. It then estimates the conditional probability for class $j$ as the ratio of neighbouring responses in that class, $P(Y=j \, | \, X=x_0) \approx \frac{1}{K}\sum_{i\in N_0}I_{(y_i=j)}$, and predicts the class of $x_0$ in the same manner as Bayes.

*The choice of $K$ is very important.* As $K$ grows the model becomes less flexible. The optimal $K$ value is often neither small nor large, but somewhere in the middle.

[Back to 2 Statistical Learning](#statistical-learning)
[Back to Table of Contents](#table-of-contents)

## 3 Linear Regression 
[3.1 Simple Linear Regression](#simple-linear-regression)
[3.2 Multiple Linear Regression](#multiple-linear-regression)
[3.3 Other Consideration in the Regression Model](#other-consideration-in-the-regression-model)
[3.4 The Marketing Plan](#the-marketing-plan)
[3.5 Comparison of Linear Regression with K-Nearest Neighbors](#comparison-of-linear-regression-with-k-nearest-neighbors)
[Back to Table of Contents](#table-of-contents)

### 3.1 Simple Linear Regression

We assume a linear relationship between a quantitative response Y and a single predictor variable X: $Y \approx \beta_0+\beta_1X$.

When we regress $Y$ on $X$ we obtain estimates ($\hat{\beta_0}$, \, $\hat{\beta_1}$) for ($\beta_0$, \, $\beta_1$) such that the model fits as close as possible to the available data, $Y = \hat{Y} + \epsilon = \hat{\beta_0}+\hat{\beta_0}X + \epsilon$.

The most common was to do this is by least squares regression, which minimizes the residual sum of squares (RSS). This gives:

$$
\begin{aligned}
\hat{\beta_1} &= \text{slope} = \frac{\sum_i=1^n (x_i-\bar{x})(y_i-\bar{y})}{\sum_i=1^n (x_i-\bar{x})^2} \\
\hat{\beta_0} &= \text{intercept} = \bar{y}-\hat{\beta_1}\bar{x} \\
RSS &= \sum_i 1^n e_i^2 = \sum_i 1^n (y_i-\hat{y_i})^2 = \sum_i 1^n (y_i-\hat{\beta_0}-\hat{\beta_1} x_i)^2 \\
\end{aligned}
$$

The true relationships is expressed as $Y = \beta_0 + \beta_1 X + \epsilon$.

An **unbiased** estimator does not systematically over- or under-setimate the true parameter. For example, averaging a parameter over many samples or datasets is (hopefully) unbiased, whereas relying on the value calculated from a single sample is (likely) biased.

We can measure **bias** with **standard error**, $\text{Var}(\hat{\mu})=\text{SE}(\hat{\mu})^2=\frac{\sigma^2}{n}$.

[Back to 3 Linear Regression](#linear-regression)
[Back to Table of Contents](#table-of-contents)

### 3.2 Multiple Linear Regression

Text

[Back to 3 Linear Regression](#linear-regression)
[Back to Table of Contents](#table-of-contents)

### 3.3 Other Consideration in the Regression Model

Text

[Back to 3 Linear Regression](#linear-regression)
[Back to Table of Contents](#table-of-contents)

### 3.4 The Marketing Plan

Text

[Back to 3 Linear Regression](#linear-regression)
[Back to Table of Contents](#table-of-contents)

### 3.5 Comparison of Linear Regression with K-Nearest Neighbors

Text

[Back to 3 Linear Regression](#linear-regression)
[Back to Table of Contents](#table-of-contents)

## 4 Classification 

[4.1 An Overview of Classification](#an-overview-of-classification)
[4.2 Why Not Linear Regression?](#why-not-linear-regression)
[4.3 Logistic Regression](#logistic-regression)
[4.4 Linear Discriminant Analysis](#linear-discriminant-analysis)
[4.5 A Comparison of Classification Methods](#a-comparison-of-classification-methods)
[Back to Table of Contents](#table-of-contents)

### 4.1 An Overview of Classification

Text

[Back to 4 Classification](#classification)
[Back to Table of Contents](#table-of-contents)

### 4.2 Why Not Linear Regression?

Text

[Back to 4 Classification](#classification)
[Back to Table of Contents](#table-of-contents)

### 4.3 Logistic Regression

Text

[Back to 4 Classification](#classification)
[Back to Table of Contents](#table-of-contents)

### 4.4 Linear Discriminant Analysis

Text

[Back to 4 Classification](#classification)
[Back to Table of Contents](#table-of-contents)

### 4.5 A Comparison of Classification Methods

Text

[Back to 4 Classification](#classification)
[Back to Table of Contents](#table-of-contents)

## 5 Resampling Methods 

[5.1 Cross-Validation](#cross-validation)
[5.2 The Bootstrap](#the-bootstrap)
[Back to Table of Contents](#table-of-contents)

### 5.1 Cross-Validation

Text

[Back to 5 Resampling Methods](#resampling-methods)
[Back to Table of Contents](#table-of-contents)

### 5.2 The Bootstrap

Text

[Back to 5 Resampling Methods](#resampling-methods)
[Back to Table of Contents](#table-of-contents)

## 6 Linear Model Selection and Regularization

[6.1 Subset Selection](#subset-selection)
[6.2 Shrinkage Methods](#shrinkage-methods)
[6.3 Dimension Reduction Methods](#dimension-reduction-methods)
[6.4 Considerations in High Dimensions](#considerations-in-high-dimensions)
[Back to Table of Contents](#table-of-contents)

### 6.1 Subset Selection

Text

[Back to 6 Linear Model Selection and Regularization](#linear-model-selection-and-regularization)
[Back to Table of Contents](#table-of-contents)

### 6.2 Shrinkage Methods

Text

[Back to 6 Linear Model Selection and Regularization](#linear-model-selection-and-regularization)
[Back to Table of Contents](#table-of-contents)

### 6.3 Dimension Reduction Methods

Text

[Back to 6 Linear Model Selection and Regularization](#linear-model-selection-and-regularization)
[Back to Table of Contents](#table-of-contents)

### 6.4 Considerations in High Dimensions

Text

[Back to 6 Linear Model Selection and Regularization](#linear-model-selection-and-regularization)
[Back to Table of Contents](#table-of-contents)

## 7 Moving Beyond Linearity

[7.1 Polynomial Regression](#polynomial-regression)
[7.2 Step Functions](#step-functions)
[7.3 Basis Functions](#basis-functions)
[7.4 Regression Splines](#regression-splines)
[7.5 Smoothing Splines](#smoothing-splines)
[7.6 Local Regression](#local-regression)
[7.7 Generalized Additive Models](#generalized-additive-models)
[Back to Table of Contents](#table-of-contents)

### 7.1 Polynomial Regression

Text

[Back to 7 Moving Beyond Linearity](#moving-beyond-linearity)
[Back to Table of Contents](#table-of-contents)

### 7.2 Step Functions

Text

[Back to 7 Moving Beyond Linearity](#moving-beyond-linearity)
[Back to Table of Contents](#table-of-contents)

### 7.3 Basis Functions

Text

[Back to 7 Moving Beyond Linearity](#moving-beyond-linearity)
[Back to Table of Contents](#table-of-contents)

### 7.4 Regression Splines

Text

[Back to 7 Moving Beyond Linearity](#moving-beyond-linearity)
[Back to Table of Contents](#table-of-contents)

### 7.5 Smoothing Splines

Text

[Back to 7 Moving Beyond Linearity](#moving-beyond-linearity)
[Back to Table of Contents](#table-of-contents)

### 7.6 Local Regression

Text

[Back to 7 Moving Beyond Linearity](#moving-beyond-linearity)
[Back to Table of Contents](#table-of-contents)

### 7.7 Generalized Additive Models 

Text

[Back to 7 Moving Beyond Linearity](#moving-beyond-linearity)
[Back to Table of Contents](#table-of-contents)

## 8 Tree-Based Methods

[8.1 The Basics of Decision Trees](#the-basics-of-decision-trees)
[8.2 Bagging, Random Forests, Boosting](#bagging-random-forests-boosting)
[Back to Table of Contents](#table-of-contents)

### 8.1 The Basics of Decision Trees

Text

[Back to 8 Tree-Based Methods](#tree-based-methods)
[Back to Table of Contents](#table-of-contents)

### 8.2 Bagging, Random Forests, Boosting

Text

[Back to 8 Tree-Based Methods](#tree-based-methods)
[Back to Table of Contents](#table-of-contents)

## 9 Support Vector Machines 

[9.1 Maximal Margin Classifier](#maximal-margin-classifier)
[9.2 Support Vector Classifiers](#support-vector-classifiers)
[9.3 Support Vector Machines](#support-vector-machines-1)
[9.4 SVMs with More than Two Classes](#svms-with-more-than-two-classes)
[9.5 Relationship to Logistic Regression](#relationship-to-logistic-regression)
[Back to Table of Contents](#table-of-contents)

### 9.1 Maximal Margin Classifier

Text

[Back to 9 Support Vector Machines](#support-vector-machines)
[Back to Table of Contents](#table-of-contents)

### 9.2 Support Vector Classifiers

Text

[Back to 9 Support Vector Machines](#support-vector-machines)
[Back to Table of Contents](#table-of-contents)

### 9.3 Support Vector Machines

Text

[Back to 9 Support Vector Machines](#support-vector-machines)
[Back to Table of Contents](#table-of-contents)

### 9.4 SVMs with More than Two Classes

Text

[Back to 9 Support Vector Machines](#support-vector-machines)
[Back to Table of Contents](#table-of-contents)

### 9.5 Relationship to Logistic Regression

Text

[Back to 9 Support Vector Machines](#support-vector-machines)
[Back to Table of Contents](#table-of-contents)

## 10 Unsupervised Learning 

[10.1 The Challenge of Unsupervised Learning](#the-challenge-of-unsupervised-learning)
[10.2 Principal Components Analysis](#principal-components-analysis)
[10.3 Clustering Methods](#clustering-methods)

### 10.1 The Challenge of Unsupervised Learning

Text

[Back to 10 Unsupervised Learning](#unsupervised-learning)
[Back to Table of Contents](#table-of-contents)

### 10.2 Principal Components Analysis

Text

[Back to 10 Unsupervised Learning](#unsupervised-learning)
[Back to Table of Contents](#table-of-contents)

### 10.3 Clustering Methods

Text

[Back to 10 Unsupervised Learning](#unsupervised-learning)
[Back to Table of Contents](#table-of-contents)
