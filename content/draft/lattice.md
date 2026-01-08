+++
title = "lattice and domains"
weight = 2
+++

## Introduction
The theory about ordered structures, such as lattices and domains, is profoundly underlooked, despite its importance in various fields:
- denotational semantics of programming languages
- properties of topology and real numbers
Compared to other algebras, such as groups and rings, ordered structures are more complicated, since the order relation is quite different from other algebraic operations like addition, multiplication, and real analysis often studies inequalities which is ordered structures.

Basic order theory doesn't require much background, but the topics in this article require substantial familiarity with category theory(especially adjunctions), since category theory is required in the very first chapters of the standard references.

Caution: There are many closely related concepts in this field, like lattices, domains, frames, locales, etc, each having slightly different definitions and properties, which may be confusing. 

we focus mainly on lattices and domains, and frames are still TBD.

notations for partial orders and domains:
- $\leq$ : partial order relation
- $\sqcup$ : least upper bound (supremum)
- $\sqcap$ : greatest lower bound (infimum)
- $\bot$ : least element (bottom element)

notations for lattices:
- $\vee$ : join (least upper bound)
- $\wedge$ : meet (greatest lower bound)

## Definitions of lattices/domains

### partial order
Definition of partial order(aka po,poset)

A partial order is a set $P$ with a binary relation $\leq$ (P, $\leq$) such that:
- Reflexive: $\forall a \in P, a \leq a$
- Transitive: $\forall a, b, c \in P, (a \leq b \land b \leq c) \implies a \leq c$
- Antisymmetric: $\forall a, b \in P, (a \leq b \land b \leq a) \implies a = b$


Definition of **complete partial order (CPO):**

A complete partial order is a partial order $(D, \leq)$ such that every chain has a supremum:
$$
\forall d_0 \leq d_1 \leq d_2 \leq ...\implies\exists \sqcup d_i \in D
$$

where $\sqcup d_i$ is called least upper bound(lub, supremum)

Definition of **domain**

A domain is a complete partial order (CPO) with a least element (bottom element) $\bot$. Here we shall list all definitions again:
- $(D, \leq)$ is a partial order
- every chain in $D$ has a least upper bound (supremum), (extra law for cpo)
- there exists a least element $\bot \in D$ such that $\forall d \in D, \bot \leq d$ (extra law for domain)

**functions between partial orders:**
- monotonic functions: $f: D_1 \to D_2$ such that $\forall x, y \in D_1, x \leq y \implies f(x) \leq f(y)$
- continuous functions for cpos: $f: D_1 \to D_2$ such that $\forall \text{chains } d_0 \leq d_1 \leq d_2 \leq ... \in D_1$, $f(\sqcup d_i) = \sqcup f(d_i)$

Note:
- Every continuous function is monotonic, but not vice versa.

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


Below topics about frames are TBD.
Definition of frame. A frame is a complete lattice that satisfies the infinite distributive law:
$$
\forall x \in L, \forall S \subseteq L, \quad x \wedge \left( \bigvee S \right) = \bigvee \{ x \wedge s \mid s \in S \}
$$

functions between frames are called frame homomorphisms, which preserve finite meets and arbitrary joins:
$$
f: L_1 \to L_2 \\\\
\forall S \subseteq L_1, \forall x, y \in L_1 \\\\
f\left( \bigvee S \right) = \bigvee f(S) \text{ , } f(x \wedge y) = f(x) \wedge f(y)
$$

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