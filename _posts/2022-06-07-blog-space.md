---
title: 'Metric Spaces, Topological Spaces and Measurable Spaces'
date: 2022-06-10
permalink: /posts/2012/08/blog-post-4/
tags:

- Notes
- Probability

---

We discuss the basic mathematic concepts of metric space, topological space and measurable space in a very narrow but interesting view. 

# Classic Question: What is the open set ?

The easy way to think this question is to refer the open interval in  a real number line. Intuitively speaking, open sets are the sets such that, for any points in the set, any points sufficiently near to the points are contained in the set. Notice the key point is about "sufficiently near" which depends on the distance quantity as we define in the real number. We need to generalize the distance concept from the real number line to sets. Then, the metric is defined as follows:

**Metric.** Let $\mathcal{X}$ be a set. A metric on $\mathcal{X}$ is given by a function $d:\mathcal{X}\times\mathcal{X}\to \mathbb{R}$ such that, for any elements $x, y \in \mathcal{X}$,

- $d(x,y)= 0$ iff $x=y$.

- $d(x, y)= d(y,x)$.

- $d(x, y) \leq d(x, z)+d(z, y)$ for any $z\in \mathcal{X}$.

In order to characterize the concept of "near", we have the following definition of *open ball* (I prefer to call it "near ball"" to emphasize the purpose), 

**Open ball.** Given a set $\mathcal{X}$ and a metric $d$ on $\mathcal{X}$, let $r\geq 0 $ be a real number and $a\in \mathcal{X}$. Denote open ball $B_{r}(a)$ by 

$$
B_{r}(a):= \{x\in \mathcal{X}|d(x, a) \leq r\}
$$

Actually, the open ball is a powerful tool to characterize a set with a metric. For example, we can use the open ball to classify the elements. Given a set $\mathcal{X}$ and a metric $d$ on $\mathcal{X}$, let us consider the set  $X \subset \mathcal{X}$:

1. **Interior.** Consider the interior points of  $X$ such that $x\in X,  \exist r>0, B_{r}(x) \in X$. And we define the interior of $X$ as $int(X)$ by,
   
   $$
   \textrm{int}(X) = \{x \in X| \exist r \geq 0, B_{r}(x) \subset X\}  
   $$

2. **Boundary.** Consider the points of $\mathcal{X}$ such that its neighborhood always intersects both $X$ and $\bar{X}$. Formally, the boundary can be defined by :
   
   $$
   \partial X = \{x \in \mathcal{X}| \forall r\geq 0, B_r(x)\cap X\not=\varnothing , B_{r}(x) \cap \bar{X} \not = \varnothing\}
   $$

Now, we are ready to define the open set formally. A set $X \in \mathcal{X}$ is open set if 

$$
X = \textrm{int}(X)
$$

In another word, the open set is the set such that every point in the set is the interior point of the set. After the definition of open set, it is vital to present the properties of open set. Given a set $\mathcal{X}$ and the collection of open subset of 

1. # Metric Spaces and Topological Spaces

Recalling what we do in the last section, we always need to state a set and a metric on this set before any definition, e.g., "given a set $\mathcal{X}$ and a metric $d$ on $\mathcal{X}$". So the above concepts are defined in a specific set with a desired structure such as metric, and the set with some structure we called **space**. For example, A **metric space** is a set $\mathcal{X}$ together with a metric $d$ on $\mathcal{X}$, denoted as $(\mathcal{X}, d)$. In the last section, we define the open set in a metric space.

Let us continue to focus on the properties of open set. Given a set $\mathcal{X}$, the open sets in $\mathcal{X}$ satisfy the following three properties:

1. $\varnothing$ and $\mathcal{X}$ are open sets.

2. The union of any collection of open sets is a open set.

3. The intersection of any finite open sets is a open set.

The above properties of open set are vital in mathematics. But, all the properties do not involve the metric even we define the open set by the metric and the open ball! This intrinsically reflects more basic structure for a class of space which is consistent with the metric space. We formally define the **topology** to capture the structure. And the corresponding **topology** is defined by:

**Topology.**  Given a set $\mathcal{X}$ , the topology is a collection $\mathcal{O}$ of subsets of $\mathcal{X}$ such that,

1. $\varnothing \in \mathcal{O}$ and $\mathcal{X} \in \mathcal{O}$.

2. The intersection of any finite collection of sets in $\mathcal{O}$ is in $\mathcal{O}$.

3. The union of any collection of sets in $\mathcal{O}$ is in $\mathcal{O}$.

A **topological space** is a set $\mathcal{X}$ together with a topology $\mathcal{O}$ , denoted as $(\mathcal{X}, \mathcal{O})$, and any subset in $\mathcal{O}$ is open set. Remarkably, we can also use the metric to define a topology. Thus, a topological space with a metric that defines the topology is a metric space.

# Measure Spaces

Similar to above metric and topology, we introduce a new concept to capture a new structure of sets, called **$\sigma$-algebra** (The reason why we need this structure will be discussed later). A non-empty collection $\mathcal{E}$ of subsets of set $\mathcal{X}$ is called a $\sigma$-algebra on $\mathcal{X}$ if it is closed under complements and countable unions, that is,

1. For any $X\in \mathcal{E}$, $\mathcal{X}-X \in \mathcal{E}$.

2. For any $X_1, X_2, \dots \in \mathcal{E}$, then $\cup_{i}X_i \in \mathcal{E}$.

Remarkably, if $\mathcal{X}$ is a topological space, then the corresponding $\sigma$-algebra from the topology on $\mathcal{X}$ is called the *Borel $\sigma$-algebra* and its elements are called *Borel sets*. Hence, the set with the structure captured by $\sigma$-algebra is called **measurable space**, denoted as a pair $(\mathcal{X}, \mathcal{E})$. Then, we present the **measure** on the measurable space $(\mathcal{X}, \mathcal{E})$ , defined by : A measure on a measurable space $(\mathcal{X}, \mathcal{E})$ is a mapping $\mu: \mathcal{E} \to \bar{\mathbb{R}}^+$ such that

1. $\mu(\varnothing) = 0$.

2. $\mu(\cup_{i}X_i) = \sum_{i}\mu(X_i)$ for any disjointed sequence $\{X_i\}$ in $\mathcal{E}$.

A **measure space** is the triplet $(\mathcal{X}, \mathcal{E}, \mu)$, where $(\mathcal{X}, \mathcal{E})$ is a measurable space and $\mu$ is a measure on it. 

Q: Why we need the $\sigma$-algebra, measure and measure spaces?

A: Probability space.

Let us review probability spaces. In probability, there are three key elements for probability space: samples, events and probability function. The samples are the possible outcomes of experiments. The events are the sets of samples. The probability function assigns each event a non-negative number that is between 0 and 1. Formally, we define a probability space with a triplet $(\Omega, \mathcal{H}, \mathbb{P})$ where $\Omega$ is a set, $\mathcal{H}$ is a $\sigma$-algebra and $\mathbb{P}$ is a measure on measurable space $(\Omega, \mathcal{H})$. *Probability space is a special measure space.*

# Takeaways

**Space is the set with associated structure.**
