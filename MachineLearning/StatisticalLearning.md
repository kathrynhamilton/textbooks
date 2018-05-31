# An Introduction to Statistical Learning

James, Witten, Hastie, Tibshirani

Kathryn Hamilton - March 2018

## <a name="toc"></a>Table of Contents

[1 Introduction](#ch1)<br>
[2 Statistical Learning](#ch2)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[2.1 What is Statistical Learning?](#2.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[2.2 Assessing Model Accuracy](#2.2)<br>
[3 Linear Regression](#ch3)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[3.1 Simple Linear Regression](#3.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[3.2 Multiple Linear Regression](#3.2)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[3.3 Other Consideration in the Regression Model](#3.3)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[3.4 The Marketing Plan](#3.4)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[3.5 Comparison of Linear Regression with K-Nearest Neighbors](#3.5)<br>
[4 Classification](#ch4)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[4.1 An Overview of Classification](#4.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[4.2 Why Not Linear Regression?](#4.2)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[4.3 Logistic Regression](#4.3)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[4.4 Linear Discriminant Analysis](#4.4)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[4.5 A Comparison of Classification Methods](#4.5)<br>
[5 Resampling Methods](#ch5)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[5.1 Cross-Validation](#5.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[5.2 The Bootstrap](#5.2)<br>
[6 Linear Model Selection and Regularization](#ch6)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[6.1 Subset Selection](#6.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[6.2 Shrinkage Methods](#6.2)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[6.3 Dimension Reduction Methods](#6.3)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[6.4 Considerations in High Dimensions](#6.4)<br>
[7 Moving Beyond Linearity](#ch7)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[7.1 Polynomial Regression](#7.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[7.2 Step Functions](#7.2)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[7.3 Basis Functions](#7.3)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[7.4 Regression Splines](#7.4)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[7.5 Smoothing Splines](#7.5)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[7.6 Local Regression](#7.6)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[7.7 Generalized Additive Models](#7.7)<br>
[8 Tree-Based Methods](#ch8)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[8.1 The Basics of Decision Trees](#8.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[8.2 Bagging, Random Forests, Boosting](#8.2)<br>
[9 Support Vector Machines](#ch9)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[9.1 Maximal Margin Classifier](#9.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[9.2 Support Vector Classifiers](#9.2)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[9.3 Support Vector Machines](#9.3)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[9.4 SVMs with More than Two Classes](9.4)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[9.5 Relationship to Logistic Regression](9.5)<br>
[10 Unsupervised Learning](#ch10)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[10.1 The Challenge of Unsupervised Learning](#10.1)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[10.2 Principal Components Analysis](#10.2)<br>
&nbsp;&nbsp;&nbsp;&nbsp;[10.3 Clustering Methods](#10.3)

## <a name="ch1"></a>1 Introduction 

Statistical learning is a set of tools for modeling and understanding complex datasets. These tools can be classified as **supervised** or **unsupervised**.

* **Supervised** learning predicts an output based on one or more inputs. Examples include linear regression and logistic regression.

* **Unsupervised** learning has inputs and no supervised output, but can still be used to learn relationships and structure. The primary example of this is cluster analysis.

------

Three example datasets are used throughout this book:

* `Wage` - Income information for males in the central Atlantic region of the United States from 2003 to 2009. The goal is to predict income based on education, age, and year (Regression).
* `Smarket` - Daily return information of the S&P stock index from 2001 to 2005. The goal is to predict whether the market will increase or decrease on a given day (Classification).
* `NCI60` - Gene expression data for 64 cancer cell lines. The goal is to determine whether there are groups or clusters among the cell lines based on their expression measurements (Clustering).

There are **R** libraries and the above datasets available on the book's [website](http:/www.StatLearning.com) to work through the book's examples and labs.

[Back to Table of Contents](#toc)

## <a name="ch2"></a>2 Statistical Learning

[2.1 What is Statistical Learning?](#2.1)<br>
[2.2 Assessing Model Accuracy](#2.2)<br>
[Back to Table of Contents](#toc)

### <a name="2.1"></a>2.1 What is Statistical Learning?

For input variables $X_1, X_2, \dots , X_p$ and output response $Y$ we assume that there is some relationship $Y=f(X)+\epsilon$, where $\epsilon$ is a zero-mean random error term independent of $X$. *Statistical learning is a set of approaches to estimate $f$.* We call this estimate $\hat{f}$.

The accuracy of $\hat{f}$ depends on both **reducible error** and **irreducible error**. This book focuses on methods of reducing reducible error.

* **Reducible error** is introduced when $\hat{f}$ is not a perfect estimate for $f$.  
* **Irreducible error** is the result of unmeasured variables that are useful in predicting $Y$ and any other unmeasurable variation.

------

There are two motivations to estimate $f$: **prediction** and **inference**.

In situations where $X$ is readily available but $Y$ is not, we can **predict** $Y$ using an estimate of $f$: $\hat{Y} = \hat(f)(X)$. In general, $\hat{f}$ is not a perfect estimate for $f$ because it cannot predict the irreducible error $\epsilon$. Here we can treat $\hat{f}$ as a black box.

In other situations, we are interested in understanding the way that $Y$ is affected as $X$ changes. This is called **inference**. We still need to estimate $f$ but cannot treat $\hat{f}$ as a black box as we are interested in understanding the relationship between $X$ and $Y$ as opposed to predicting $Y$. We may want to know:  

* Which predictors are most strongly associated to the response?
* What is the relationship between the response and each predictors?
* Which relationships can be summarized using a linear equation? Which are more complicated?

*Many problems fall into both of these categories.* For example, consider an advertising firm that would like to know which form of media advertising generates the largest boost in sales (inference), and how much of an increase in sales would occur given an advertising increase in that specific media (prediction).

*The best method for estimating $f$ depends on the goal and what you are trying to achieve.*

------

Most statistical learning methods can be classified as either **parametric** or **non-parametric**.

**Parametric methods** first make an assumption about the form of $f$, which typical involves some parameters, and then uses training data to fit the model and thus provide estimate values for each parameter. Assuming a parametric form simplifies the problem of estimating $f$, but can be dangerous if the model chosen does not represent the data sufficiently well or is overly complicated.

**Non-parametric methods** do not make an explicit assumption about the form of $f$. They seek an estimate of $f$ by getting as close to the data as possible while limiting noise and overfitting. The advantage is that they can be fit accuractely to a wide range of possible shapes, thus avoiding the possibility of poor fit. However, solving these types of problems are can be very difficult and the results are often not easy to interpret.

------

Various statistical methods have a trade off between **interpretability** and **flexibility**. Inference problems favor restrictive models with higher interpretability. Prediction problems favor more flexible models as they are more likely to be accurate (at the risk of overfitting) and thus provide better predictions. Some exemplary methods are as follows:

* **Subset Selection** and **Lasso** have high interpretability and have low flexibility.
* **Bagging**, **Boosting** and **Support Vector Machines** have high flexibility and low interpretability.
* **Least Squares**, **Generalized Additive Models** and **Trees** have moderate flexibility and moderate interpretability.

------

Variables in a statistical learning problem are either **quantitative** or **qualitative** (categorical). We tend to refer to problems with a quantitative response as **regression** problems while those involving a qualitative response are referred to as **classification** problems.

[Back to 2 Statistical Learning](#ch2)<br>
[Back to Table of Contents](#toc)

### <a name="2.2"></a>2.2 Assessing Model Accuracy

*There is no free lunch* in statistics: no one method dominates all others over all possible datasets. Hence, it is an important task to decide which method produces the best results for the particular dataset at hand.

To measure how well predictions match observed data we use the following error functions, where $y_i$ is the observed value and $\hat{f}(x_i)$ is the predicted value of the response:

* **Mean Squared Error** (MSE) for regression problems, $MSE=\frac{1}{n} \sum_{i=1}^{n}(y_i-\hat{f}(x_i))^2$.
* **Error Rate** for classification problems, $\text{Error rate}=\frac{1}{n}\sum_{i=1}^{n} I_{(y_i)}\neq \hat{f(x_i)}$.

Models with smaller error predict more accurately that those with larger error.

These accuracy metrics are meant to be performed on *unseen data that has not been used to fit the model*, known as the test set. In practice, computing the test error can be very difficult as response data is not usually available. Sometimes the training error can approximate the test error. Otherwise, **cross-validation** or **partitioning** must be used to estimate the test error using the training data.

------

In order to minimize expected test error, the chosen statistical method *must simulatenously acheive* **low variance** *and* **low bias** where:

* **Variance** is the amount by which $\hat{f}$ would change if the model were fitted using a different training set.
* **Bias** is the error that is introduced by approximating a real-life problem with a simplified model.

------

Test error rate is minimized, on average, by a classifier that *assigns each observation to the most likely class*.

The **Bayes Classifier** for quantitative responses operates under this premise, by predicting the class of $x_0$ to be $j$ when $P(Y=j \, | \, X=x_0) is the greatest out of all possible classes.

The **Bayes error rate** is $1-E\left(\max_j P(Y=j \, | \, X)\right)$, which is analogous to the irreducible error.

**K-Nearest Neighbors** (KNN) follows the same theory for qualitative responses. However, conditional probability can only be estimated rather than calculated directly so this method is weaker than the Bayes Classifier. 

KNN identifies the K closest observations to $x_0$, called $N_0$. It then estimates the conditional probability for class $j$ as the ratio of neighbouring responses in that class, $P(Y=j \, | \, X=x_0) \approx \frac{1}{K}\sum_{i\in N_0}I_{(y_i=j)}$, and predicts the class of $x_0$ in the same manner as Bayes.

*The choice of $K$ is very important.* As $K$ grows the model becomes less flexible. The optimal $K$ value is often neither small nor large, but somewhere in the middle.

[Back to 2 Statistical Learning](#ch2)<br>
[Back to Table of Contents](#toc)

## <a name="ch3"></a>3 Linear Regression 

[3.1 Simple Linear Regression](#3.1)<br>
[3.2 Multiple Linear Regression](#3.2)<br>
[3.3 Other Consideration in the Regression Model](#3.3)<br>
[3.4 The Marketing Plan](#3.4)<br>
[3.5 Comparison of Linear Regression with K-Nearest Neighbors](#3.5)<br>
[Back to Table of Contents](#toc)

### <a name="3.1"></a>3.1 Simple Linear Regression

We assume a linear relationship between a quantitative response Y and a single predictor variable X: $Y \approx \beta_0+\beta_1X$.

When we regress $Y$ on $X$ we obtain estimates ($\hat{\beta_0}$, \, $\hat{\beta_1}$) for ($\beta_0$, \, $\beta_1$) such that the model fits as close as possible to the available data, $Y = \hat{Y} + \epsilon = \hat{\beta_0}+\hat{\beta_0}X + \epsilon$.

The most common was to do this is by least squares regression, which minimizes the residual sum of squares (RSS). This gives:

\begin{aligned}
\hat{\beta_1} &= \text{slope} = \frac{\sum_i=1^n (x_i-\bar{x})(y_i-\bar{y})}{\sum_i=1^n (x_i-\bar{x})^2} \\
\hat{\beta_0} &= \text{intercept} = \bar{y}-\hat{\beta_1}\bar{x} \\
RSS &= \sum_i 1^n e_i^2 = \sum_i 1^n (y_i-\hat{y_i})^2 = \sum_i 1^n (y_i-\hat{\beta_0}-\hat{\beta_1}x_i})^2
\end{aligned}

The true relationships is expressed as $Y = \beta_0 + \beta_1 X + \epsilon$

An **unbiased** estimator does not systematically over- or under-setimate the true parameter. For example, averaging a parameter over many samples or datasets is (hopefully) unbiased, whereas relying on the value calculated from a single sample is (likely) biased.

We can measure **bias** with **standard error**, $\text{Var}(\hat{\mu})=\text{SE}(\hat{\mu})^2=\frac{\sigma^2}{n}$.

[Back to 3 Linear Regression](#ch3)<br>
[Back to Table of Contents](#toc)

### <a name="3.2"></a>3.2 Multiple Linear Regression

Text

[Back to 3 Linear Regression](#ch3)<br>
[Back to Table of Contents](#toc)

### <a name="3.3"></a>3.3 Other Consideration in the Regression Model

Text

[Back to 3 Linear Regression](#ch3)<br>
[Back to Table of Contents](#toc)

### <a name="3.4"></a>3.4 The Marketing Plan

Text

[Back to 3 Linear Regression](#ch3)<br>
[Back to Table of Contents](#toc)

### <a name="3.5"></a>3.5 Comparison of Linear Regression with K-Nearest Neighbors

Text

[Back to 3 Linear Regression](#ch3)<br>
[Back to Table of Contents](#toc)

## <a name="ch4"></a>4 Classification 

[4.1 An Overview of Classification](#4.1)<br>
[4.2 Why Not Linear Regression?](#4.2)<br>
[4.3 Logistic Regression](#4.3)<br>
[4.4 Linear Discriminant Analysis](#4.4)<br>
[4.5 A Comparison of Classification Methods](#4.5)<br>
[Back to Table of Contents](#toc)

### <a name="4.1"></a>4.1 An Overview of Classification

Text

[Back to 4 Classification](#ch4)<br>
[Back to Table of Contents](#toc)

### <a name="4.2"></a>4.2 Why Not Linear Regression?

Text

[Back to 4 Classification](#ch4)<br>
[Back to Table of Contents](#toc)

### <a name="4.3"></a>4.3 Logistic Regression

Text

[Back to 4 Classification](#ch4)<br>
[Back to Table of Contents](#toc)

### <a name="4.4"></a>4.4 Linear Discriminant Analysis

Text

[Back to 4 Classification](#ch4)<br>
[Back to Table of Contents](#toc)

### <a name="4.5"></a>4.5 A Comparison of Classification Methods

Text

[Back to 4 Classification](#ch4)<br>
[Back to Table of Contents](#toc)

## <a name="ch5"></a>5 Resampling Methods 

[5.1 Cross-Validation](#5.1)<br>
[5.2 The Bootstrap](#5.2)<br>
[Back to Table of Contents](#toc)

### <a name="5.1"></a>5.1 Cross-Validation

Text

[Back to 5 Resampling Methods](#ch5)<br>
[Back to Table of Contents](#toc)

### <a name="5.2"></a>5.2 The Bootstrap

Text

[Back to 5 Resampling Methods ](#ch5)<br>
[Back to Table of Contents](#toc)

## <a name="ch6"></a>6 Linear Model Selection and Regularization

[6.1 Subset Selection](#6.1)<br>
[6.2 Shrinkage Methods](#6.2)<br>
[6.3 Dimension Reduction Methods](#6.3)<br>
[6.4 Considerations in High Dimensions](#6.4)<br>
[Back to Table of Contents](#toc)

### <a name="6.1"></a>6.1 Subset Selection

Text

[Back to 6 Linear Model Selection and Regularization](#ch6)<br>
[Back to Table of Contents](#toc)

### <a name="6.2"></a>6.2 Shrinkage Methods

Text

[Back to 6 Linear Model Selection and Regularization](#ch6)<br>
[Back to Table of Contents](#toc)

### <a name="6.3"></a>6.3 Dimension Reduction Methods

Text

[Back to 6 Linear Model Selection and Regularization](#ch6)<br>
[Back to Table of Contents](#toc)

### <a name="6.4"></a>6.4 Considerations in High Dimensions

Text

[Back to 6 Linear Model Selection and Regularization](#ch6)<br>
[Back to Table of Contents](#toc)

## <a name="ch7"></a>7 Moving Beyond Linearity

[7.1 Polynomial Regression](#7.1)<br>
[7.2 Step Functions](#7.2)<br>
[7.3 Basis Functions](#7.3)<br>
[7.4 Regression Splines](#7.4)<br>
[7.5 Smoothing Splines](#7.5)<br>
[7.6 Local Regression](#7.6)<br>
[7.7 Generalized Additive Models](#7.7)
[Back to Table of Contents](#toc)

### <a name="7.1"></a>7.1 Polynomial Regression

Text

[Back to 7 Moving Beyond Linearity](#ch7)<br>
[Back to Table of Contents](#toc)

### <a name="7.2"></a>7.2 Step Functions

Text

[Back to 7 Moving Beyond Linearity](#ch7)<br>
[Back to Table of Contents](#toc)

### <a name="7.3"></a>7.3 Basis Functions

Text

[Back to 7 Moving Beyond Linearity](#ch7)<br>
[Back to Table of Contents](#toc)

### <a name="7.4"></a>7.4 Regression Splines

Text

[Back to 7 Moving Beyond Linearity](#ch7)<br>
[Back to Table of Contents](#toc)

### <a name="7.5"></a>7.5 Smoothing Splines

Text

[Back to 7 Moving Beyond Linearity](#ch7)<br>
[Back to Table of Contents](#toc)

### <a name="7.6"></a>7.6 Local Regression

Text

[Back to 7 Moving Beyond Linearity](#ch7)<br>
[Back to Table of Contents](#toc)

### <a name="7.7"></a>7.7 Generalized Additive Models 

Text

[Back to 7 Moving Beyond Linearity](#ch7)<br>
[Back to Table of Contents](#toc)

## <a name="ch8"></a>8 Tree-Based Methods

[8.1 The Basics of Decision Trees](#8.1)<br>
[8.2 Bagging, Random Forests, Boosting](#8.2)

### <a name="8.1"></a>8.1 The Basics of Decision Trees

Text

[Back to 8 Tree-Based Methods](#ch8)<br>
[Back to Table of Contents](#toc)

### <a name="8.2"></a>8.2 Bagging, Random Forests, Boosting

Text

[Back to 8 Tree-Based Methods](#ch8)<br>
[Back to Table of Contents](#toc)

## <a name="ch9"></a>9 Support Vector Machines 

[9.1 Maximal Margin Classifier](#9.1)<br>
[9.2 Support Vector Classifiers](#9.2)<br>
[9.3 Support Vector Machines](#9.3)<br>
[9.4 SVMs with More than Two Classes](9.4)<br>
[9.5 Relationship to Logistic Regression](9.5)<br>
[Back to Table of Contents](#toc)

### <a name="9.1"></a>9.1 Maximal Margin Classifier

Text

[Back to 9 Support Vector Machines](#ch9)<br>
[Back to Table of Contents](#toc)

### <a name="9.2"></a>9.2 Support Vector Classifiers

Text

[Back to 9 Support Vector Machines](#ch9)<br>
[Back to Table of Contents](#toc)

### <a name="9.3"></a>9.3 Support Vector Machines

Text

[Back to 9 Support Vector Machines](#ch9)<br>
[Back to Table of Contents](#toc)

### <a name="9.4"></a>9.4 SVMs with More than Two Classes

Text

[Back to 9 Support Vector Machines](#ch9)<br>
[Back to Table of Contents](#toc)

### <a name="9.5"></a>9.5 Relationship to Logistic Regression

Text

[Back to 9 Support Vector Machines](#ch9)<br>
[Back to Table of Contents](#toc)

## <a name="ch10"></a>10 Unsupervised Learning 

[10.1 The Challenge of Unsupervised Learning](#10.1)<br>
[10.2 Principal Components Analysis](#10.2)<br>
[10.3 Clustering Methods](#10.3)

### <a name="10.1"></a>10.1 The Challenge of Unsupervised Learning

Text

[Back to 10 Unsupervised Learning](#ch10)<br>
[Back to Table of Contents](#toc)

### <a name="10.2"></a>10.2 Principal Components Analysis

Text

[Back to 10 Unsupervised Learning](#ch10)<br>
[Back to Table of Contents](#toc)

### <a name="10.3"></a>10.3 Clustering Methods

Text

[Back to 10 Unsupervised Learning](#ch10)<br>
[Back to Table of Contents](#toc)
