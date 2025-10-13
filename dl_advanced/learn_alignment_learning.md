# Alignment learning


The basic idea is NOT learn a function $f$ to get $y = f(x)$, but learn a function $g$ to judge the alignment of $x$ and $y$. The alignment score is $s = s(x, y)$. To obtain $y$ for a given $x$, we need to perform search, which is another optimization problem.

Formally:

$$
y^{*} =\min_{y} s_{\theta}(x^{*}, y)
$$


Reference:
- https://www.youtube.com/watch?v=yUmDRxV0krg

## Introduction


In a simple example:
- Use $f_x$ to encode $x$
- Use reversible $z_y = f_y(y)$ to encode $y$
- Trained $s_{\theta}$

In inference time, given $x_{*}$:
1. Find $z^{*}_y$ that minimizes $s_{\theta}(z_{x^{*}}, z_{y^{*}})$
2. Recover $y^{*} = f^{-1}_y(z^{*}_y)$

Formally:
$$
z_y^{*} = \min_{z_y} s_{\theta}(f_x(x^{*}), z_y)
$$
$$
y^{*} = f_y^{-1}(z_y^{*})
$$

This rather simple optimization technique can be:
- Mathmatical optimization
- Bayesian model
- Gradient descent

Theoretially, even if the inference algorithm is hard, and it is quite time consuming to get a $y^{*}$ given $x^{*}$. once we have $s$, we can generate as much as (x, y) pairs as we want. Using that almost endless data, we can train a DL model out of it.

## Train the score function
- Contrastive
- Self-distillate
- Regularization (eg. Make embedding matrix to be orthogonal.)


## Category

### Joint Embedding 

Lets have some assumption:
- $x$ and $y$ is from same data distribution. For example, both images.
- trainable encoder $f_x$ and decoder $g_z$.

Then the problem can be model as:

1. train $s=s_{\theta}(f_x(x), f_x(y))$
2. $z_y^{*} = \min_{z_y} s_{\theta}(f_x(x^{*}), z_y)
$
3. $y^{*} = g_z(z_y^{*})$
