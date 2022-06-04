---
title: 'Variational Lower and Upper Bounds of Mutual Information'
date: 2022-06-04
permalink: /posts/2012/08/blog-post-4/
tags:
  - Information Theory
  - Representation Learning
---


# Variational Lower and Upper Bounds of Mutual Information

Mutual information (MI) has been widely used in many fields of machine learning, especially in representation learning. Almost all the works focus on the Information Maximization problem. MI between data and representation is maximized to ensure that the representation retains as much information as possible. However, maximizing MI can lead to the issue of overfitting. I derive the variational lower and upper bound pf MI. And thereby I discuss the information maximization principle and the dual version, the information minimization principle. With the upper and lower bound, I explore the corresponding applications: Variational Information Bottleneck and Joint Source-channel Coding.

Let us consider a inference model $x\to z$ and use the following **notation**:

1. $p(x)$: data distribution

2. $p_{\phi}(z|x)$:  represenation distribution (or encoder equivalently)

3. $p_{\phi}(z)$: marginal distribution

4. $p_{\phi}(x|z)$:  posterior

5. $I_{\phi}(X,Z)=\int p_{\phi}(z|x)p(x)\log\frac{p_{\phi}(z|x)p(x)}{p_{\phi}(z)p(x)}dzdx$ : the mutual information that depends on $p_{\phi}(z|x)$.

Since the marginal $p_{\phi}(z) = \int p(x)p_{\phi}(z|x)dx$ and posterior $p_{\phi}(x|z)$ are intractable, the MI is generally intractable.

## Variational Lower Bound of MI

The following equality of MI: 

$I_{\phi}(X,Z) = H(X)-H(X|Z)$

where $H(X)$ is constant for a given data distribution $p(x)$. The second term, conditional entropy $H(X|Z)$, is also intractable due to the intractability of $p_{\phi}(x|z)$.  By introducing the variational distribution $p_{\theta}(x|z)$, one can have the variational approximation:

$H(X|Z) = \mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log p_{\phi}(z|x)]$

                  $=\mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log p_{\theta}(z|x)] -\underbrace{\mathbb{E}_{p(x)p_{\phi}(z|x)}[\log\frac{p_{\phi}(z|x)}{p_{\theta}(z|x)}]}_{KL(p_{\phi}(z|x)||p_{\theta}(z|x))}$

                 $\leq \mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log p_{\theta}(z|x)]$

Hence, the variational lower bound of MI, $I'(X,Z; \phi, \theta)$, can be obtained by :

$I_{\phi}(X,Z) \geq  H(X)+\mathbb{E}_{p(x)p_{\phi}(z|x)}[\log p_{\theta}(z|x)] = I'(X,Z; \phi, \theta)$

We can maximize the variational lower to solve the information maximization problem.

## Variational Upper Bound of MI

The following equality of MI:

$I_{\phi}(Z;X) = H(Z) -H(Z|X)$

where the conditional entropy $H(Z|X)$ is fully defined by $H(Z|X) = \mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log p_{\phi}(z|x)]$. The first term, the entropy of marginal distribution $H(Z)$, is intractable due to the intractability of $p_{\phi}(z)$. By introducing the variational distribution $q(z)$, one can easily derive the variational approximation:

$H(Z) = \mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log p_{\phi}(z)]$

             $=\mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log q(z)]- \underbrace{\mathbb{E}_{p(x)p_{\phi}(z|x)}[\log \frac{p_{\phi}(z)}{q(z)}]}_{KL(p_{\phi}(z)||q(z))}$ 

            $\leq \mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log q(z)]$

Hence, the variational information minimization objective can be obtained by the variational upper bound of MI,

$I_{\phi}(Z,X) \leq \mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log q(z)] +\mathbb{E}_{p(x)p_{\phi}(z|x)}[\log p_{\phi}(z|x)] = I''(X,Z;\phi)$

We can minimize the upper bound to minimize the mutual information between $X$ and $Z$. However, the proposed variational distribution $q(z)$ will act as a prior in the optimization and induce the learned representation $p_{\phi}(z|x)$ to have the desired properties. 

To maximize or minimize the MI, we can push up the variational lower bound or push down the upper bound, respectively. Combining the information maximization and minimization, a typical application is Information Bottleneck. With the variational lower and upper bound of MI, we can derive a variational approximation to Information Bottleneck, which has been proposed in [Variational IB](https://arxiv.org/abs/1612.00410v7) .

## Variational Information Bottleneck

In the Information Bottleneck (IB) problem, a target variable $Y$ is introduced for the original data $X$ with a Markov chain $Y\to X \to Z$. The representation $Z$ is learned to retain maximal information about target with a constraint of data compression, e.g., $I(X;Z)\leq R$. The IB optimization problem is formulated as 

$\max\limits_{\phi} I_{\phi}(Z, Y) \text{\ \ \ s.t.} I_{\phi}(Z,X) \leq R$,

which can be regarded as a rate-distortion tradeoff between data compression and  target-relevant information preserving. By introducing the Lagrange multiplier $\beta$, the IB problem is equivalent to maximize the following objective function:

$\mathcal{L}_{IB}(\phi) = I_{\phi}(Z,Y)-\beta I_{\phi}(Z,X)$.

Using the above variational upper and lower bounds, we recast the objective functio in variational IB as follws:

$\mathcal{L}_{IB}(\phi) \geq \mathcal{L}_{VIB}(\phi, \theta)$

               $= I'(Y,Z; \phi, \theta) -\beta I''(X,Z;\phi)$                

                        $=\mathbb{E}_{p(x)p_{\phi}(z|x)}[\log p_{\theta}(y|z)] - \beta (\mathbb{E}_{p(x)p_{\phi}(z|x)}[-\log q(z)] +\mathbb{E}_{p(x)p_{\phi}(z|x)}[\log p_{\phi}(z|x)])$

$=\mathbb{E}_{p(x)p_{\phi}(z|x)}[\log p_{\theta}(y|z)] - \beta KL(p_{\phi}(z|x)||q(z))$ 

Let us consider another problem, joint source-channel coding.

## Joint Source-channel Coding

Let us consider a comunication system with encoder $p_{\phi}(z|x)$ and a noisy channel $p_{\text{channel}}(\hat{z}|z)$ with a Markov chain: $X\to Z\to \hat{Z}\to \hat{X}$ that which satisfies $p(\hat{z}|x) = p_{\phi}(\hat{z}|x)p_{\text{channel}}(\hat{z}|z)$.

The optimal channel-source coding depends on the given distortion-cost function (The single-letter joint source-channel coding will be introduced in the following blogs, please stay tuned!). We adopt the cost measure $\rho: \mathcal{Z}\to \mathbb{R}^+$ as :

$\rho(z) = KL(p_{\text{channel}}(\hat{z}|z)||p(\hat{z}))$

which is equivalent to the mutual information between channel input $Z$ and output $\hat{Z}$.

We adopt the distortion measure $d: \mathcal{X}\times \hat{\mathcal{Z}} \to \mathbb{R}^+$ as :

$d(x, \hat{z}) = -\log p_{\phi}(x|\hat{z})$

which is equivalent to the negative mutual information between the data $X$ and received corrupted representation $\hat{Z}$.

We want to design a coding scheme to minimize cost and distortion. However, the received signal will be heavily corrupted and thereby lead to high distortion if the input cost is low. So there is an inherent tradeoff between input cost and reconstruction performance. We formulate this problem to minimize the following objective function with $\beta > 0$ controlling the tradeoff:

$\mathcal{L}_{\text{JSCC}}(\phi) = d(x, \hat{z}) + \beta \rho(z) $

                    $=\mathbb{E}_{p(x)p_{\phi}(\hat{z}|x)}[-\log p_{\phi}(x|\hat{z})] + \beta \mathbb{E}_{p(x)p_{\phi}(z|x)}[\text{KL}(p(\hat{z}|z)||p(\hat{z}))]$

Recalling the variational upper and lower bound, a variational objective function $\mathcal{L}_{VJSCC}(\phi, \theta)$ is proposed by introducing the variational approximation $p_{\theta}(x|\hat{z})$ and $q(\hat{z})$:

$\mathcal{L}_{JSCC}(\phi) \leq \mathcal{L}_{VJSCC}(\phi, \theta) $

                    $=\mathbb{E}_{p(x)p_{\phi}(\hat{z}|x)}[-\log p_{\theta}(x|\hat{z})] + \beta \mathbb{E}_{p(x)p_{\phi}(z|x)}[\text{KL}(p(\hat{z}|z)||q(\hat{z}))]$

## Takaways

**Information Maximization is not the whole world. Information minimization is also important to improve the model generalization. The combination of InfoMax and InfoMin is also core of many applications like information bottleneck and joint source-channel coding.**


