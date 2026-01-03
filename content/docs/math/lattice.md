+++
title = "lattice and domains"
weight = 2
+++

## Prerequisites
Basic order theory doesn't require much background, but the topics in this article require substantial familiarity with category theory(especially adjunctions), since category theory is required in the very first chapters of the standard references.

Caution: There are many closely related concepts in this field, like lattices, complete lattices, frames, locales, domains, etc, each having slightly different definitions and properties, which may be confusing. 

## Definitions of lattices
Definition of partial order:
$$
\text{A partial order is a set } P \text{ with a binary relation } \leq \text{ such that:} 
\\\\
\begin{align*}
& \text{1. Reflexive: } \forall a \in P, a \leq a. \\\\
& \text{2. Antisymmetric: } \forall a, b \in P, (a \leq b \land b \leq a) \implies a = b. \\\\
& \text{3. Transitive: } \forall a, b, c \in P, (a \leq b \land b \leq c) \implies a \leq c.
\end{align*}
$$

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
Let us consider a topology $(X, T )$ and its lattice $L(X)$ of open sets, with set inclusion $\subseteq$ as the partial order $\leq$. The $L(X)$ is a functor from the category of topological spaces to the category of frames. The functor is also denoted as $\Omega$.


The category of lattices:
> objects: Lattices
> arrow: monotonic functions

The category of topological spaces:
> objects: Topological spaces
> arrow: continuous functions

The functor from lattices to topological spaces: