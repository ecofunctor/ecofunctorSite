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

## Definitions of categories

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

## Monads
A monad can be construed from an adjunction. Given an adjunction $F \dashv G$, we can define a monad $T$ on category $C$ as follows:
$$
T = G \circ F
$$
