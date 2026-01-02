+++
title = "Mathematics"
weight = 1
+++

Here's the place for advanced mathematics topics, including category theory, algebra, and more. The word "advanced" merely indicates the topics requires some mathematical maturity.

## Motivations
For many advanced mathematical topics there's not a single best textbook to learn from, aside from a few exceptions like:
- Linear Algebra Done Right by Sheldon Axler
- Homotopy Type Theory book
and others(PRs are welcome)

The issues are:
- Many textbooks are too concise, and skip many details in proofs or put too much content as exercises.
- The subjects are not standardized, requiring readers to reference many resources, like lattices theory
- The subjects are very abstract, and the textbooks are either too abstract or not abstract enough(not teaching abstraction good enough).

## styles
The styles of the articles are inspired by the book "Homotopy Type Theory". Each article is structured as follows:
- Motivations and backgrounds
- Definitions
- Theorems and proofs
- Examples, Remarks

Specifically, mathematical objects like definitions, theorems are quoted as 
> Definition ...
> A is consisted of ...

or in code blocks:
```
Definition of A:
A is consisted of ...
```

formulas are written in LaTeX style:
$$
\\\\
A = \pi r^2
\\\\
Hom_{grp}(A,F(B)) \cong Hom_{set}(U(A),B)
\\\\
f: Int \to Int
\\\\
f := x \to x^2
\\\\
\mapsto_{bijection}
$$ 

or inline as $A = \pi r^2$.