---
layout: page
title: Principal Component Analysis
author: Rozenn Dahyot
date:   2023-11-13 19:41:59 +0000
---



# Introduction




- These notes follow notations used in this recommended reading: Section 12.1.1. of  [Pattern Recognition and Machine Learning](https://www.microsoft.com/en-us/research/uploads/prod/2006/01/Bishop-Pattern-Recognition-and-Machine-Learning-2006.pdf) by Christopher Bishop.

- **Appendix C** of that same book also provides a reminder on Linear Algebra (e.g. eigenvectors of matrices etc.)
	
	
- Some of the results presented here are using these  [Linear Algebra Formula ](https://roznn.github.io/SLIDES/Slides_Formula.html) showing how to differentiate w.r.t. a vector.
	





# Maximum variance formulation 



<blockquote class="twitter-tweet"><p lang="en" dir="ltr">PCA equivalently <br>- maximizes the variance of the projected data<br>- minimizes the reconstruction error<br><br>Kick off our <a href="https://twitter.com/Olissipo_eu?ref_src=twsrc%5Etfw">@olissipo_eu</a> minicourse of dimensionality reduction with <a href="https://twitter.com/t_vayer?ref_src=twsrc%5Etfw">@t_vayer</a>! <a href="https://t.co/pkLaGKj40l">pic.twitter.com/pkLaGKj40l</a></p>&mdash; Mathurin Massias (@mathusmassias) <a href="https://twitter.com/mathusmassias/status/1622623539109978119?ref_src=twsrc%5Etfw">February 6, 2023</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>



## Data

Consider that we have a set of vectors $\lbrace \mathbf{x}_n \rbrace _{n=1,\cdots ,N}$ in $\mathbb{R}^D$. 
This means that any vector $\mathbf{x}_n$ has $D$ coordinates as follows:
$$
\mathbf{x}_n =
\left\lbrack 
\begin{array}{c}
x_n[1]\\
x_n[2]\\
\vdots\\
x_n[D]\\
\end{array}
\right\rbrack
$$


## Mean

 We can define the mean $\overline{\mathbf{x}}$ such that 
$$
\overline{\mathbf{x}}=\frac{1}{N}\sum_{n=1}^{N} \mathbf{x}_n
$$
Spatially, the mean can be understood as the [center of gravity](https://en.wikipedia.org/wiki/Center_of_mass) of the clouds of points $\lbrace \mathbf{x}_n \rbrace _{n=1\cdots N}$.

$\overline{\mathbf{x}}$ is a also vector of dimension $D$:
$$
\overline{\mathbf{x}} =
\left\lbrack 
\begin{array}{c}
\frac{1}{N} \sum_{n=1}^N x_n[1]\\
\frac{1}{N} \sum_{n=1}^N x_n[2]\\
\vdots\\
\frac{1}{N} \sum_{n=1}^N x_n[D]\\
\end{array}
\right\rbrack
$$

## Covariance matrix


The covariance matrix $\mathrm{S}$ is defined as:
$$
\mathrm{S}=\frac{1}{N} \sum_{n=1}^{N} (\mathbf{x}_n-\overline{\mathbf{x}}) (\mathbf{x}_n-\overline{\mathbf{x}})^{T}
$$

with defining $\mathbf{\tilde{x}}_n=\mathbf{x}_n-\mathbf{\overline{x}}$, $\forall n$ then
$$
\mathrm{S}=\frac{1}{N} \sum_{n=1}^{N} \mathbf{\tilde{x}}_n \ \mathbf{\tilde{x}}_n^T
$$
or
$$
\mathrm{S}=\frac{1}{N} \sum_{n=1}^N 
\left \lbrack
\begin{array}{cccc}
(\tilde{x}_{n}[1])^2 & (\tilde{x}_{n}[1]\times \tilde{x}_{n}[2]) &\cdots
&(\tilde{x}_{n}[1] \times \tilde{x}_{n}[D])\\
&&&\\
 (\tilde{x}_{n}[1]\times \tilde{x}_{n}[2])& (\tilde{x}_{n}[2])^2  &&\\
&&&\\
&&\ddots&\\
&&&\\
&&& (\tilde{x}_{n}[D])^2 \\
\end{array}
\right\rbrack
$$


Defining the $D\times N$ matrix $\mathrm{\tilde{X}}=[\tilde{x}_{1},\cdots,\tilde{x}_{N}]$ then the covariance matrix is
$$
\mathrm{S}=\frac{1}{N} \mathrm{\tilde{X}}\mathrm{\tilde{X}}^T
$$
The covariance matrix $\mathrm{S}$ is of size $D\times D$.


## Maximum variance formulation

Consider unit vector $\mathbf{u}_1$ (i.e. such that $\|\mathbf{u}_1\|^2=\mathbf{u}_1^T\mathbf{u}_1=1$).

The variance of the projected data is:
$$
\frac{1}{N}\sum_{n=1}^N \left( \mathbf{u}_1^T\mathbf{x}_n - \mathbf{u}_1^T\overline{\mathbf{x}} \right)^2 = \mathbf{u}_1^T \mathrm{S}\ \mathbf{u}_1
$$
We want to find the vector $\mathbf{u}_1$ such that: 

$$
\hat{\mathbf{u}}_1=\arg \max_{\mathbf{u}_1} \lbrace \mathbf{u}_1^T \mathrm{S}\ \mathbf{u}_1\rbrace \quad \text{subject to} \quad \|\mathbf{u}_1 \|^2=1
$$
Introducing the Lagrange multiplier $\lambda_1$, this is the same as optimising:  
$$
\hat{\mathbf{u}}_1,\hat{\lambda}_1=\arg \max_{\mathbf{u}_1,\lambda_1}\  \lbrace \ \mathcal{E}(\mathbf{u}_1,\lambda_1)=\mathbf{u}_1^T \mathrm{S}\ \mathbf{u}_1 +\lambda_{1} \ (1-\mathbf{u}_1^T\mathbf{u}_1 ) \  \rbrace
$$
This means that we are looking for the  vector $\mathbf{u}_1$ that maximizes the energy function   $\mathcal{E}$.


### Finding $\mathbf{u}_1$ and $\lambda_1$

The solution is  such that the derivatives of $\mathcal{E}$ are zeros, so we need to find $(\mathbf{u}_1,\lambda_1)$ such that: 


$$
\frac{\partial\mathcal{E}}{\partial \mathbf{u}_1}=0 \quad (\star)
$$
and
$$
\frac{\partial\mathcal{E}}{\partial \lambda_1}=0   \quad (\star \star)
$$

### Solving $(\star\star)$ 

$\lambda_1$ is a scalar so :
$$
\frac{\partial\mathcal{E}}{\partial \lambda_1}= (1-\mathbf{u}_1^T\mathbf{u}_1 )=0
$$
and this differentiation w.r.t. the Lagrange multiplier $\lambda_1$ allows to recover the constraint 
$$
\mathbf{u}_1^T\mathbf{u}_1=\|\mathbf{u}_1\|^2=1
$$


### Solving $(\star)$ 

The derivative w.r.t. vector $\mathbf{u}_1$ can be computed using   [Linear Algebra Formula](https://roznn.github.io/SLIDES/Slides_Formula.html)
$$
\frac{\partial\mathcal{E}}{\partial \mathbf{u}_1}=\underbrace{\frac{\partial (\mathbf{u}_1^T \mathrm{S}\ \mathbf{u}_1 )}{\partial \mathbf{u}_1}}_{(a)}
-\lambda_{1} \ \underbrace{\frac{\partial (\mathbf{u}_1^T\mathbf{u}_1 )}{\partial \mathbf{u}_1}}_{(b)}+\lambda_{1} \ \underbrace{\frac{\partial (1)}{\partial \mathbf{u}_1}}_{=0}
$$

For (a)  using the last  [formula](https://roznn.github.io/SLIDES/Slides_Formula.html#2) 
$$
\frac{\partial (\mathbf{u}_1^T \mathrm{S}\ \mathbf{u}_1 )}{\partial \mathbf{u}_1}
= \mathrm{S}\ \mathbf{u}_1 +\mathrm{S}^T\ \mathbf{u}_1=2\ \mathrm{S}\ \mathbf{u}_1
$$
because the convariance matrix $\mathrm{S}$ is a $D\times D$ symmetric matrix hence $\mathrm{S}^T=\mathrm{S}$.

For (b)  using the third [formula](https://roznn.github.io/SLIDES/Slides_Formula.html#2) 
$$
\frac{\partial (\mathbf{u}_1^T\mathbf{u}_1 )}{\partial \mathbf{u}_1}=2\ \mathbf{u}_1
$$

### Solution 

 The vector $\mathbf{u}_1$ that maximizes the variance is the eigenvector of the covariance matrix $\mathrm{S}$ with eigenvalue $\lambda_1$:
 $$
 \mathrm{S}\ \mathbf{u}_1=\lambda_1\ \mathbf{u}_1
  $$
 
Eigenvalue $\lambda_1$ is also the variance of the projections:
$$
\mathbf{u}_1^T\mathrm{S}\mathbf{u}_1=\lambda_1
$$
$\lambda_1$ is the highest eigenvalue of $\mathrm{S}$.

### How to find the direction with second most maximum variance? 

Once we have the direction $\mathbf{u}_1$ with its associated eigenvalue $\lambda_1$ (variance of the projections of centered data on  $\mathbf{u}_1$), the direction $\mathbf{u}_2$  with second maximum variance can be found such that:
$$
\mathbf{u}_2^T\mathrm{S}\mathbf{u}_2
$$
in maximised with constraints $\|\mathbf{u}_2\|=1$ and $\mathbf{u}_2^T\mathbf{u}_1=0$ ($\mathbf{u}_2$ is orthogonal to $\mathbf{u}_1$).





#  Principal components


## Computing PCA

From a set of  vectors $\lbrace \mathbf{x}_n \rbrace_{n=1,\cdots,N}$ 

1. Compute the mean $\overline{\mathbf{x}}$
2. Center each observations $\mathbf{\tilde{x}}_n=\mathbf{x}_n-\overline{\mathbf{x}}$
3. Compute the covariance matrix 
$$
\mathrm{S}=\frac{1}{N} \sum_{n=1}^{N} \mathbf{\tilde{x}}_n \mathbf{\tilde{x}}_n^T
$$
4. Compute the eigenvectors of  $\mathrm{S}$ and sort them  from the one associated with the highest eigenvalue , to the one associated with the lowest eigenvalue. 



$$
\text{eigenvectors} \quad \equiv \quad \text{Principal components}
$$





## Using PCA

Each vector in the set  can be written as a linear combination of the mean and the eigenvectors:
$$ 
\mathbf{x} = \overline{\mathbf{x}} +\sum_{j=1}^D \alpha_j\  \mathbf{u}_j
$$
How many eigenvectors are really needed for a good reconstruction?


## Applications

- Compression / Dimensionality reduction
- Visualisation of data distribution
- etc.

Example PCA applied to images of faces : https://en.wikipedia.org/wiki/Eigenface


```{r echo=FALSE, out.width = "50%", fig.align = "center"}
knitr::include_graphics("https://upload.wikimedia.org/wikipedia/commons/6/67/Eigenfaces.png")
```


# Questions



- What is the dimension of the matrix $\tilde{\mathrm{X}}$?

- What is the dimension of the covariance matrix $\mathrm{S}$?

- What are the properties of the covariance matrix $\mathrm{S}$?
  
-  Using these [Linear Algebra Formula](https://roznn.github.io/SLIDES/Slides_Formula.html), 
show that the solution is such that:
$$
\mathrm{S}\ \mathbf{u}_1 = \lambda_1\ \mathbf{u}_1
$$
