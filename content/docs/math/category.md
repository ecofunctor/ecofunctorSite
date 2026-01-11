+++
title = "category theory"
weight = 1
+++

This article explores category theory from a mathematical perspective, while providing examples in computer science. Since category theory is highly abstract, we aim not to avoid abstraction, but to present it in a clear manner with precise notions(might be verbose at times). Features of this tutorial:
- mathematical perspective, but people from other backgrounds can also follow
- jump to adjunctions quickly
- delay universal properties and yoneda lemma after monads,compare to traditional order
- use common notations
- we skip basic definitions like categories and functors, where current textbooks suffice

In contrast, "Category Theory for Programmers" posts by Bartosz Milewski or "Category Theory for computer scientists" are from computer science perspective, and Steven Awodey's "Category Theory" book is more of logic theory taste. This article is purely **mathematical**, meaning that the definitions and theorems introduced as mathematical objects, without much analogy to logic or programming.

We assume mathematical maturity in linear algebra and abstract algebra(not used directly, but the way of thinking matters).

This article covers standard topics in category theory:
- Definitions of categories, functors, and natural transformations
- Monads
- Yoneda lemma
- Kan extensions

For applications:
- Correspondence between category theory and Haskell
- Monads for splitting construction and execution

## Preliminaries

Recommended textbooks, from mathematical perspective:
- "Category theory in context" by Emily Riehl
- "Basic Category Theory" by Tom Leinster
- "A first course in category theory" by Ana Agore
- "Categories for the Working Mathematician" by Saunders Mac Lane (advanced)

The first book assumes basic knowledge of linear algebra. Compared to other category theory books the prerequisites are lighter.

There are many other excellent textbooks, but they may be from different perspectives(like computer science, logic, etc).


### Simplifications
To reduce the complexity of category theory, we make some simplifications here:
- only locally small categories(skip size discussions)
- postpone universal properties(initial/final objects, limits/colimits) which involves logical quantifiers like $\forall, \exists$.


### Diagram chasing:
A commutative diagram is a graphical representation of mathematical structures and their relationships, where the composition of morphisms along different paths between two objects yields the same result. In other words, no matter which path you take from one object to another, the outcome is the same.

Proving that a diagram commutes often involves the skill named "diagram chasing," where we pick up an element, and apply morphisms along different paths to show that the results are equal at the bottom right corner.

## Definitions of categories
Basic definitions about categories, functors are skipped here, please refer to recommended textbooks.

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
A monad can be constructed from an adjunction. Given an adjunction $F \dashv G$, we can define a monad $T$ on category $C$ as follows:
$$
T = G \circ F
$$

## Universal properties
Universal properties are a way to define objects in terms of their relationships to other objects.

**Initial objects:**

An object $i\in C$(category $C$) is called an initial object if(several equivalent definitions):
- $\forall x \in C$, there exists a unique morphism from $i$ to $x$.
- $\forall x \in C, Hom_C(i, x)$ is a singleton set.
- The functor $Hom_C(i, -): C \to Set$ is naturally isomorphic to the constant functor that maps every object to a singleton set.

### Representable functors
The concept of representation is prevalent in mathematics, we have:
- Riesz representation theorem in functional analysis, stating that continuous linear functionals on a Hilbert space can be represented as an inner product with a vector
- Caley's theorem in group theory, stating that every group is isomorphic to the permutation group.

Similarly, in category theory, a representable functor can be represented by the hom-functor with a specific object fixed.

**Definition of representable functor:**
- A functor $F: C \to Set$ is called representable if there exists an object $r \in C$ such that $F$ is naturally isomorphic to the hom-functor $Hom_C(r, -)$.


Examples:
- In the category of sets, the empty set $\emptyset$ is an initial object, since there is exactly one function from $\emptyset$ to any set $A$ (the empty function).

## Theorems
Here we give some important theorems in category theory as "abstract nonsense".

### Yoneda lemma
In the same vein as representation theorems in mathematics, The Yoneda lemma relates between objects in a category and the functors defined on that category. 
After introducing the representable functors, we want to know how to define a natural transformation $\mapsto_{nat} $ between a representable functor and an arbitrary functor, namely:
$$
Hom_C(c, -) \mapsto_{nat} F
$$
where $c \in C$ is a fixed object, and $F: C \to Set$ is an arbitrary functor. Before thinking about the general $\mapsto_{nat}$, we first consider a natural isomorphism $\cong_{nat}$.



**Theorem (Yoneda lemma):**
$$
Nat(Hom_C(c, -),F) \cong_{bij} F(c)
$$
That is, there's a bijection $\cong_{bij}$ between the set of natural transformations $Nat(Hom_C(c, -),F)$ and the set $F(c)$.

## Kan extensions

## Notions 
Different textbooks may use different notations, which might be confusing for beginners. Here we list some common notations.


**function/morphism related:**
| Notation                  | Meaning                                                                                     | Type                |
| ------------------------- | ------------------------------------------------------------------------------------------- | ------------------- |
| $Hom_C(a, b)$ , $C(a, b)$ | The set of morphisms from a to b in category C                                              | space of functions  |
| $Hom_C(a, -)$, $C(a, -)$  | The hom-functor, maps $b \in C$ to set of morphisms $C(a, b)$, aka functor represented by a | functor:$ C\to Set$ |
