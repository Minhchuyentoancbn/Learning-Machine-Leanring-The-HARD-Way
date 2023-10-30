# Topic 1: Probability and Statistics

## 0. Table of Contents

- [1. Univariate Models](#1-univariate-models)
    - [1.1. Univariate Gaussian Distribution](#11-univariate-gaussian-distribution)
    - [1.2. Student's t Distribution](#12-students-t-distribution)
    - [1.3. Cauchy distribution](#13-cauchy-distribution)
    - [1.4. Laplace distribution](#14-laplace-distribution)
    - [1.5. Beta distribution](#15-beta-distribution)
    - [1.6. Gamma distribution](#16-gamma-distribution)
    - [1.7. Transformation of Random Variables](#17-transformation-of-random-variables)
- [2. Multivariate Models](#2-multivariate-models)
    - [2.1. Joint distributions for multiple random variables](#21-joint-distributions-for-multiple-random-variables)
    - [2.2. The multivariate Gaussian (normal) distribution](#22-the-multivariate-gaussian-normal-distribution)
    - [2.3. Linear Gaussian systems](#23-linear-gaussian-systems)

- [Reference](#reference)


## 1. Univariate Models

### 1.1. Univariate Gaussian Distribution

- Dirac delta function:

![](./dirac%20delta%20function.png)

### 1.2. Student's t Distribution

- Student's t distribution:

![](./Student%20Distribution.png)

- We see that the probability density decays as a polynomial function of the squared distance from the center, as opposed to an exponential function, so there is more probability mass in the tail than with a Gaussian distribution. We say that the Student distribution has heavy tails, which makes it robust to outliers. 

### 1.3. Cauchy distribution

![](./Cauchy%20Distribution.png)

### 1.4. Laplace distribution

![](./Laplace%20Distribution.png)

### 1.5. Beta distribution

![](./Beta%20Distribution.png)

### 1.6. Gamma distribution

![](./Gamma%20Distribution%201.png)
![](./Gamma%20Distribution%202.png)

### 1.7. Transformation of Random Variables 
![](./Transformation%20of%20RVs.png)

## 2. Multivariate Models

### 2.1. Joint distributions for multiple random variables 
![](./Joint%20Distribution.png)

### 2.2. The multivariate Gaussian (normal) distribution

![](./MVN.png)

- Can be used for missing value imputation.

### 2.3. Linear Gaussian systems

![](./Linear%20Gaussian.png)

### 2.4. Mixture of Models

- Gaussian Mixture Model (GMM): If we let the number of mixture
components grow sufficiently large, a GMM can approximate any smooth distribution

## Reference

- [1] Kevin P. Murphy. 2022. Probabilistic Machine Learning: An introduction. MIT Press.