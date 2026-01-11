+++
title = "lattice and domains"
weight = 2
+++

## Introduction
Compared to other algebras, such as groups and rings, ordered structures are more complicated, since the order relation is quite different from other algebraic operations like addition, multiplication, and real analysis often studies inequalities which is ordered structures. So this field is actually underlooked, despite its importance in various fields:
- denotational semantics of programming languages
- properties of topology and real numbers


More specifically, some important questions include:
- Is $D \cong D \to D$ solvable for some domain $D$?
- type issues for $x \to x(x)$ in untyped lambda calculus
- the relation between continuous functions and computability


We aim to cover the following topics:
- definitions of partial orders, lattices, domains
- the functions between these structures
- fixed point theorems
- the relation to topology, like Scott topology
- adjunction with topological spaces
- applications in semantics of programming languages

Basic order theory doesn't require much background, but the topics about topology and adjunctions require maturity in general topology and category theory.

Note: There are many closely related concepts in this field, like lattices, domains, frames, locales, etc, each having slightly different definitions and properties, which may be confusing. 

we focus mainly on lattices and domains, and frames are still TBD.

notations for partial orders and domains:
- $\leq : D \times D \to Bool$ : partial order relation. 
- $\sqcup : D \times D \to D$ : least upper bound (supremum). 
- $\sqcap$ : greatest lower bound (infimum)
- $\bot$ : least element (bottom element)

notations for lattices:
- $\vee$ : join (least upper bound)
- $\wedge$ : meet (greatest lower bound)

## the ordered structures
Now we give the definitions of various ordered structures from partial orders to lattices.

### partial order

**A partial order** is a set $P$ with a binary relation $\leq$ (P, $\leq$) such that:
- Reflexive: $\forall a \in P, a \leq a$
- Transitive: $\forall a, b, c \in P, (a \leq b \land b \leq c) \implies a \leq c$
- Antisymmetric: $\forall a, b \in P, (a \leq b \land b \leq a) \implies a = b$



A **complete partial order (CPO):** is a partial order $(D, \leq)$ such that every chain has a supremum:
$$
\forall d_0 \leq d_1 \leq d_2 \leq ...\implies\exists \sqcup d_i \in D
$$

where $\sqcup d_i$ is called least upper bound(lub, supremum)



A **domain** is a complete partial order (CPO) with a least element (bottom element) $\bot$. Here we shall list all definitions again:
- $(D, \leq)$ is a partial order
- every chain in $D$ has a least upper bound (supremum), (extra law for cpo)
- there exists a least element $\bot \in D$ such that $\forall d \in D, \bot \leq d$ (extra law for domain)


### lattice
Definition of **lattice:**
A lattice is a partial order $(L, \leq)$ such that :
- $\forall x, y \in L$, $x \sqcup y \in L$ (least upper bound of two elements exists)
- $\forall x, y \in L$, $x \sqcap y \in L$ (greatest lower bound of two elements exists)

So lattices have two more requirements than CPOs: the existence of supremum and infimum for every pair of elements.


Definition of **complete lattice:**

A complete lattice is a lattice $(L, \leq)$ such that :
- $\forall S \subseteq L$, a least upper bound (supremum) $\sqcup S$ in $L$ exists.

In contrast to complete partial orders vs partial orders, complete lattices require more from lattices: 
- the existence of supremum for every subset.
- while CPO only requires the existence of supremum for every chain.

### Terminologies
Some important terminologies:
- upper set : A subset $U \subseteq D$ of a poset $(D, \leq)$ is called an upper set if $\forall x, y \in D, x \in U \land x \leq y \implies y \in U$. We also denote it as $\uparrow x$ for some $x \in D$.
- lower set : A subset $L \subseteq D$ on the opposite of upper set, denoted as $\downarrow x$ for some $x \in D$.
- upper bound : An element $u \in D$ is called an upper bound of a subset $S \subseteq D$ if $\forall s \in S, s \leq u$.
- lower bound : the opposite of upper bound.
### Example poset and cpo
The power set:
-  $(P(S), \subseteq)$ is a partial order $(D, \leq)$.
- it is also a cpo since $(P(S), \subseteq, \cup)$ is a cpo $(D, \leq, \sqcup)$ 
- it is also a domain since $\emptyset$ is the bottom $\bot$.

The product domain from $D_1$ and $D_2$:
- $\leq$ is defined pointwise: $(d_1, d_2) \leq (d_1', d_2') \iff d_1 \leq d_1' \land d_2 \leq d_2'$ , so $(D_1 \times D_2, \leq)$ is a partial order.
- $\sqcup$ : $(d_1, d_2) \sqcup (d_1', d_2') = (d_1 \sqcup d_1', d_2 \sqcup d_2')$ 


The function space $D_1 \to D_2$ where $D_1, D_2$ are both cpos:
- $\leq$ is defined pointwise: $f \leq g \iff \forall x \in D_1, f(x) \leq g(x)$ , so $(D_1 \to D_2, \leq)$ is a partial order.
- $\sqcup$ : $(\sqcup_i f_i)(x) = \sqcup_i f_i(x)$ , so $(D_1 \to D_2, \leq, \sqcup)$ is a cpo.
- if $D_1, D_2$ are both domains, then $(D_1 \to D_2, \leq, \sqcup, \bot)$ is also a domain


The evaluation map $eval: (D_1 \to D_2) \times D_1 \to D_2$ defined as $eval(f, x) = f(x)$ is continuous on domains $(D_1 \to D_2)$ and $D_1$.

### functions: monotone and continuous
functions between partial orders and lattices:
- monotonic functions: $f: D_1 \to D_2$ such that $\forall x, y \in D_1, x \leq y \implies f(x) \leq f(y)$
- continuous functions for cpos: $f: D_1 \to D_2$ such that $\forall \text{chains } d_0 \leq d_1 \leq d_2 \leq ... \in D_1$, $f(\sqcup d_i) = \sqcup f(d_i)$
- strict functions: $f: D_1 \to D_2$ such that $f(\bot_{D_1}) = \bot_{D_2}$

Note:
- Every continuous function is monotonic, but not vice versa.


Examples of monotonic functions:

Let $(P{a, b, c}, \leq)$ and $(P{d, e}, \leq)$ be two posets, then the function $f: P{a, b, c} \to P{d, e}$ can be defined in multiple ways, some are continuous and some are not. 

Let $C$ be cpo, consider the function $f: (C \to C) \to (C \to C)$ 
- $f$ defined as $f(g) = g $ is 

### fixed point theorem
First, we define fixed points and pre-fixed points.

Let $(P, \leq)$ be a poset, and $f: P \to P$ be a monotonic function:
- **fixed point** A point $x \in P$ is called a fixed point of $f$ if $f(x) = x$.
- **pre-fixed point** An element $x \in P$ is called a pre-fixed point of $f$ if $f(x) \leq x$.
- **least fixed point** The least fixed point of $f$ is the smallest element among all fixed points of $f$, satisfying $f(lfp(f)) \leq lfp(f)$ and $\forall x \in P, f(x) = x \implies lfp(f) \leq x$.

Now we state some important theorems about fixed points in posets and domains.

**Theorem: least fixed point for monotonic functions**

Statement: 
- Let $(D, \leq)$ be a poset and 
- $f: D \to D$ be a function and
- $lfp(f)$ be the least pre-fixed point of $f$

Then if $f$ is monotonic, then $lfp(f)$ is a fixed point of $f$ so $lfp(f) = fix(f)$.


**Theorem: Tarski's fixed point theorem**

Statement:
- Let $(D, \leq, \sqcup, \bot)$ be a domain
- $f: D \to D$ be a continuous function

Then:
- $lfp(f)$ of $f$ is constructed as $lfp(f) = \sqcup_{n \geq 0} f^n(\bot)$
- and $lfp(f) = fix(f) $


Application:
Tarski's fixed point theorem is widely used in denotational semantics of programming languages to define the semantics of recursive functions, since the semantics of recursive functions can be defined as the least fixed point of some continuous function on a suitable domain.

## Adjunction between lattice and topology
**Scott topology**
First, we define Scott open sets on a CPO $(D, \leq)$. A subset $U \subseteq D$ is open iff:
- $\forall x, y \in D, x \in U \land x \leq y \implies y \in U$ (upper set)
- $\forall \text{chains } d_0 \leq d_1 \leq d_2 \leq ... \in D, \sqcup d_i \in U \implies \exists i, d_i \in U$ (inaccessible by directed suprema)

(ref: Exercise 8.4 in SemPL)


Let us consider a topology $(X, T )$ and its lattice $L(X)$ of open sets, with set inclusion $\subseteq$ as the partial order $\leq$. The $L(X)$ is a functor from the category of topological spaces to the category of frames. The functor is also denoted as $\Omega$.


The category of lattices:
> objects: Lattices
> arrow: monotonic functions

The category of topological spaces:
> objects: Topological spaces
> arrow: continuous functions

The functor from lattices to topological spaces:


## References
- Lectures on Domains and Denotational Semantics, Glynn Winskel (main reference)
- SemPL The Formal Semantics of Programming Languages: An Introduction, Glynn Winskel
- Semantics with Applications: An Appetizer, Hanne Riis Nielson and Flemming Nielson
- Domain theory by Abramsky and Jung (From the book "Handbook of Logic in Computer Science", Volume 3)
- Introduction to Lattices and Order
- A lambda Calculus for Real Analysis, Paul Taylor