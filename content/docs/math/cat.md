+++
title = "category theory"
weight = 1
+++

This document explores category theory from a mathematical perspective, while providing examples in computer science. Since category theory is highly abstract, we aim not to avoid abstraction, but to present it in a clear manner with precise notions(might be verbose at times).

In contrast, "Category Theory for Programmers" posts by Bartosz Milewski or "Category Theory for computer scientists" are from computer science perspective, and Steven Awodey's "Category Theory" book is more of logic theory taste. This article is purely **mathematical**, and assumes some mathematical maturity like linear algebra and abstract algebra(not used directly, but the way of thinking matters).

This article covers standard topics in category theory:
- Definitions of categories, functors, and natural transformations
- Monads
- Yoneda lemma
- Kan extensions

For applications:
- Correspondence between category theory and Haskell
- Monads for splitting construction and execution
## Preliminaries
Textbooks:
- "Category theory in context" by Emily Riehl

This book assumes basic knowledge of linear algebra. Compared to other category theory books the prerequisites are lighter.


Diagram chasing:
A commutative diagram is a graphical representation of mathematical structures and their relationships, where the composition of morphisms along different paths between two objects yields the same result. In other words, no matter which path you take from one object to another, the outcome is the same.

Proving that a diagram commutes often involves the skill named "diagram chasing," where we pick up an element, and apply morphisms along different paths to show that the results are equal at the bottom right corner.

## Definitions of categories

### Natural transformations
On the surface, a transformation is just a function $\eta_x: D \to D$ between objects in a category $D$. A natural transformation is a special kind of such transformation. Here we fix the index $x$, and later we will see $x$ varies over objects in another category $C$.

To talk about the naturality, the target category $D$ is insufficient, and actually we need two functors $F, G: C \to D$ to make the notion of naturality precise.

Given two functors $F, G: C \to D$, a natural transformation $\eta$ from $F$ to $G$ assigns to each object $c$ in $C$ a morphism $\eta_c: F(c) \to G(c)$ in category $D$(more vaguely, $\eta_c: D \to D$). 

The naturality condition requires that for every morphism $f: c_1 \to c_2$ in category $C$, the following diagram commutes:

This means that applying $F$ to $f$ and then $\eta_{c_2}$ is the same as applying $\eta_{c_1}$ and then $G$ to $f$:

## Adjunctions
An adjunction is a pair of functors that stand in a particular relationship to each other. Specifically, a functor $F: C \to D$ is left adjoint to a functor $G: D \to C$ if there is a natural isomorphism between the hom-sets:
$$
Hom_D(F(c), d) \cong Hom_C(c, G(d))
$$

The $\cong$ here might be confusing, but it acutally means that $\cong$ is just a bijection, and the notion of bijection requires $Hom_D(F(c), d)$ and $Hom_C(c, G(d))$ to be sets. So we may also write:
$$
Hom_D(F(c), d) \leftrightarrow_{bij} Hom_C(c, G(d))
$$

We write the adjunction as $F \dashv G$.
Note: Adjunctions are also called Galois connections in fields like order theory, abstract algebra, etc.

## Monads
A monad can be construed from an adjunction. Given an adjunction $F \dashv G$, we can define a monad $T$ on category $C$ as follows:
$$
T = G \circ F
$$
