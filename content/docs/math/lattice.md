+++
title = "lattice and domains"
weight = 2
+++

## Introduction
The theory of ordered structures like lattices and domain theory is a underlooked field in mathematics, compared to other algebraic fields about groups, vector spaces, graphs, etc.
Ordered structures are complicated, since the order relation is quite different from other algebraic operations like addition, multiplication.

As an example, Real analysis frequently studies inequalities and ordered structures. Additionally, order theory plays a crucial role in areas such as:
- denotational semantics of programming languages
- properties of topology and the real numbers

About the prerequisites,Basic order theory doesn't require much background, but the topics about topology and adjunctions require maturity in general topology and category theory.

We aim to cover the following topics:
- definitions of partial orders, lattices, domains
- the functions between these structures
- fixed point theorems
- the relation to topology, like Scott topology
- adjunction with topological spaces
- applications in semantics of programming languages

Some important questions in this field are:
- Is $D \cong D \to D$ solvable for some domain $D$?
- type issues for $x \to x(x)$ in untyped lambda calculus
- the relation between continuous functions and computability


we focus mainly on lattices and domains, and frames are still TBD.


Note: There are many closely related concepts in this field, like lattices, domains, frames, locales, etc, each having slightly different definitions and properties, which may be confusing. 

## the ordered structures
**preliminary notations:**
We start with the most basic notations for partial orders and domains:
- $\leq : D \times D \to Bool$ : partial order relation. 
- $\sqcup : D \times D \to D$ : least upper bound (supremum). 
- $\sqcap$ : greatest lower bound (infimum)
- $\bot$ : least element (bottom element)

notations for lattices:
- $\vee$ : join (least upper bound)
- $\wedge$ : meet (greatest lower bound)

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


## Applications: program analysis
program analysis is a formal method to analyze programs without executing them. It can be used to approximate the behavior of programs.The domain in program analysis represent the info of a program at it's execution point(in program graph or flow graph). 


In contrast to existing textbooks which first introduce specific analyses(like reaching definitions) and then present general frameworks(monotone framework, etc), we start from the general frameworks and then summarize specific analyses.


we start with some notations:
- $WholeProgram$ : the whole program
- $progGraph(Prog)$ or $flowGraph(Prog)$, etc, denotes the program graph or flow graph of the whole program. 
- $Prog$ : the program fragment, like statements, expressions, etc.
- $A$ : the abstract domain, representing the properties we want to analyze
- $Q$ : the program points. We assume $Q$ includes unknown point $?$, start point and end point.
- $Result = ProgPoint \to A$ : the result of program analysis, mapping each program point to the value in the abstract domain $A$.

Note:
- The $Result$ is usually implemented as a map.


**1.without abstract interpretation:**

The transfer function is defined as $tranA: Prog \to A \to A$. Given a whole program as $progGraph(Prog)$ or $flowGraph(Prog)$, we run a algorithm(worklist algorithm, etc) to apply the transfer function on each program point until reaching a fixed point. The termination is guaranteed by the ascending chain condition(ACC) on the abstract domain $A$. Each transformation is summarized as:
- $WholeProgram \to progGraph(Prog)$ : an algorithm to convert the whole program to a program graph or flow graph.
- $progGraph(Prog) \to Result$ : the worklist algorithm ($Wk: progGraph(Prog) \to (Prog \to A \to A) \to Result$) apply the transfer function $tranA: Prog \to A \to A$ on $progGraph(Prog)$ until reaching a fixed point.

The algorithm is given according to the fixed point theorem on domains, where the fixed point is reached by applying the transfer function $tranA(p, a)$ on  abstract domain $a$ iteratively until reaching a fixed point.

For reference, we also attach the definition of monotone framework here(from ProgAA,p53):
<img width="551" alt="image" src="https://github.com/user-attachments/assets/a131a94b-a1e3-4d9f-b340-d6f91e96d285" />



**2.abstract interpretation:**
The advantage of abstract interpretation is that the concrete transfer function $tran$ are defined once for all analyses, and we only need to define the abstraction and concretization functions $\alpha$ and $\gamma$ for different analyses, since the bulk of the work is to define $tran$.

The concrete semantics(collect semantics) domain $C$
represents the most precise state of the program, while the abstract domain $A$ represents an approximation of the concrete domain and the specific properties we want to analyze.

extra further notations:
- $C$ : the concrete domain, representing the semantics of the program
- $\alpha: C \to A$ : abstraction function, mapping concrete states to abstract states
- $\gamma: A \to C$ : concretization function, mapping abstract states to concrete
- proof that $\alpha$ and $\gamma$ form a Galois connection: $\forall c \in C, a \in A, \alpha(c) \leq a \iff c \leq \gamma(a)$, aka adjunction
- $tran: Prog \to C \to C $ : the transfer function, given a program fragment and domain, returns the new domain.


The goal of program analysis is to calculate the values of the abstract domain $A$ at each program point, given the information above. Depending on whether abstract interpretation is used, there are two approaches:
- with abstract interpretation: we first define the abstraction and concretization functions $\alpha$ and $\gamma$, then we define the concrete transfer function $tran: Prog \to C \to C$
- derive the abstract transfer function $tranA: Prog \to A \to A$ as $tranA(p, a) = \alpha(tran(p, \gamma(a)))$, defined via composition with $\alpha$, $\gamma$ and $tran$.
- now we have $tranA: Prog \to A \to A$, and same as before.

**common abstract domains**

we summarize some common domains in a table:
| Analysis                     | Lattice/Domain                                      | Description                                                          |
| ---------------------------- | --------------------------------------------------- | -------------------------------------------------------------------- |
| Reaching definitions         | $Var \to Pow(Q*Q)$  or $Pow(Var \times Q \times Q)$ | For each variable, the set of program points where it may be defined |
| Live variables               | $Pow(Var)$                                          | The set of variables used in the program point                       |
| Interval analysis            | $Var \to Interval$                                  | For each variable, the range of it's possible values                 |
| Collective semantics(ProgAA) | $Pow(Var \to Value)$                                | The set of all possible variable assignments at a program point      |
| Collective semantics(ProgA)  | $Pow(Var \to ProgPoint)$                            | Program points where each variable changed                           |


The lattices structures are defined as follows:
| Lattice/Domain                                     | $\leq$                                      | $\sqcup$               | $\bot$      |
| -------------------------------------------------- | ------------------------------------------- | ---------------------- | ----------- |
| $Var \to Pow(Q*Q)$ or $Pow(Var \times Q \times Q)$ | induced from subset inclusion of $Pow(Q*Q)$ | induced from set union | $\emptyset$ |


Note : 
- The collecting semantics in ProgAA and ProgA are different, since the former is more introductory and simpler.
- $ProgPoint$ is the type representing program points, like blocks numbers.
- For reaching definitions, $Var \to Pow(Q*Q)$ is equivalent to $Pow(Var \times Q \times Q)$ via currying.
- For induced $\leq$ it means that $a \leq b$ iff $\forall v \in Var, a(v) \subseteq b(v)$.


The summary from ProgA, p70 is attached here for reference:

<img width="500" alt="image" src="https://github.com/user-attachments/assets/86ffbf78-602f-49fc-9a98-3ea1b5cc323b" />


## Applications: program semantics
Denotational semantics is a formal method to define the semantics of programming languages by mapping the syntax of programs to elements in domains. The domains represent the possible values and states of the programs during execution.
The main steps to define denotational semantics using domains are:

## Applications: logical systems

## References
Textbooks:
- Lectures on Domains and Denotational Semantics, Glynn Winskel (main reference)
- SemPL The Formal Semantics of Programming Languages: An Introduction, Glynn Winskel
- Semantics with Applications: An Appetizer, Hanne Riis Nielson and Flemming Nielson
- Domain theory by Abramsky and Jung (From the book "Handbook of Logic in Computer Science", Volume 3)
- Introduction to Lattices and Order (Stone duality, topology)
- A lambda Calculus for Real Analysis, Paul Taylor
- ProgAA, Program Analysis an Appetizer, Flemming Nielson
- ProgA, Principles of Program Analysis, Flemming Nielson
