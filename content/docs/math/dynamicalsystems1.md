+++
title = "dynamical systems 1"
weight = 3
+++
## Introduction

This article refines the post "Complex systems, Chaos and ecosystem part 1: the defiance to reductionism". In contrast to other articles in the math section, this article is more philosophical and conceptual, rather than focusing on rigorous mathematical definitions and proofs. 

Reductionism, a philosophy that seeks to handle complexity by breaking into parts, serves as the corner stone for industrial revolution and contemporary science. This top-down approach is also quite compatible with the social hierarchy that rich people have more power and control over the society, as the conerstone of modern neoliberal capitalism.


However, The whole is often greater than the sum of its parts, and the attempt to understand complex systems through reductionism neglects the interactions, emergent behaviors, and non-linear dynamics within the system.

For example,In neuroscience and artificial intelligence, attempting to understand consciousness through the examination of individual neurons can't answer how consciousness emerge from those simple parts, as well as trying to create intelligence by connect neurons in a predefined way, whatsoever it's convolutional, hierarchical or recurrent. Similarly, In ecology, reducing an ecosystem to its individual species is unable to explain the stability,resilience and at the same time, the fragility of ecosystem.


Aside from those complicated systems, simple deterministic system may show unpredictable behaviors. In this article, I will introduce the concept of dynamical systems and show some of those systems described with simple mathematical formula. 


Topics in part 1 are basics:
- basics concepts like phase space, trajectory
- bifurcation
- chaos and sensitivity to initial conditions


Advanced concepts like chaos, renormalization, self-organization will be discussed in the next part, as well as the mathematical tools.

# dynamical systems
is about analyzing systems that changes over time(or iteration).
the evolution of the system can be described by a thinking of a point moving in a space called phase space. The movement path is called trajectory. 

Differential equations are one way to describe the system, and another way is to use difference equations,aka iterated maps.

The current framework to study dynamical systems can be think of as the evolution of rules over time, divided into three main components:

    The Rules: This involves the formulation of the rules, such as differential equations, difference equations, and potentially  algebraic equations.

    Evolution: Time or the iterations

    Interpretation of Results: This involves determining whether the evolution process can be explained in a non-recursive form, similar to solving differential equations. Even if an exact solution cannot be obtained, we can often derive the topological or geometric structure of the space, allowing us to predict the form of the solution.

From this perspective, analysis, algebra, and geometry each play a role in the study of dynamical systems. Analysis pertains to differential dynamical systems, algebra relates to discrete dynamical systems, and geometry and topology are concerned with interpreting the characteristics of various models.

## phase space
The phase space is a space where the state of the system is represented by a point. The dimension of the phase space is equal to the number of variables needed to describe the state of the system. For example, a pendulum can be described by two variables: the angle and the angular velocity, so the phase space is two-dimensional.

**phase space diagram** is an important tool to analyze the behavior of the system. 
for example,for x'=f(x),treat it as iterated maps and calc next x and find it's movement

# examples

## weather prediction
Weather prediction is a classic example of a complex system that exhibits chaotic behavior. The prediction of weather is accurate only for a short period of time, but becomes increasingly uncertain for longer time scales. This is due to the sensitivity of the initial conditions, where small changes in the initial state can lead to drastically different outcomes.

## personal transportation

## free will vs determinism
it is actually a question of whether the system is deterministic or not,given the initial condition. 
for example, the double pendulum system is deterministic, but it is not predictable due to the sensitivity to the initial condition.

# psychology
dynamic systems theory can be applied to psychology, as it provides a framework for understanding the complex interactions between cognitive, emotional, and behavioral processes. For example, the development of personality traits, social relationships, and mental health can be viewed as dynamic systems that evolve over time in response to internal and external influences.

In psychology, normal personality traits can be understood as able to adapt to different situations, while maladaptive traits are characterized by rigidity and inflexibility. This rigidity can be seen as a failure to adapt to changing circumstances, leading to negative outcomes like anxiety, depression, and interpersonal conflicts.

for example, the concept of self-fulfilling prophecies in psychology can be understood through the lens of dynamic systems theory.
If someone consistently uses a strategy of seeking approval from others, they may sacrifice their assertiveness and independence. When this strategy is successful, they become even more focused on pleasing others. Conversely, if the strategy fails, they feel compelled to work harder to gain acceptance in the future.

This self-fulfilling cycle occurs regardless of the specific strategy used. Those who oppose others constantly face criticism, while those who distance themselves end up feeling lonely. Over time, this rigidity prevents the development of more adaptable strategies, as short-term adjustments aimed at avoiding harm hinder long-term growth.

# Anarchism
Anarchism is a political philosophy that advocates for the abolition of hierarchical power structures and the establishment of self-governing communities based on voluntary cooperation and mutual aid. This philosophy is rooted in the belief that individuals are capable of organizing themselves without the need for external authority or coercion. 

Through the lens of dynamic systems theory, it can be argued that hierarchical power structures are inherently unstable and prone to collapse due to their rigid and inflexible nature. In contrast, self-organizing systems based on voluntary cooperation and mutual aid are more resilient and adaptable to changing circumstances and able to emerge unforeseen creative solutions and insights.

Thus, the current societal structure can be seen as built on a reductionist approach. However, it's also not 100% reductionist, as there are some self-organizing systems in the society, like open source projects, social movements, grassroots organizations, even a team in a company can be seen as having some self-organizing properties.

# management

## reductionist top-down approach in management
In corporate management, the reductionist approach is often advertised as professional management, where the organization is structured hierarchically, with clear roles, responsibilities, and reporting lines. This approach is used to break down complex problems into simpler components that can be analyzed and solved independently. KPIS, OKRs, and other metrics are used to measure the performance of individuals and teams, and to align their goals with the organization's objectives. The advantage of this approach is that it provides a clear framework for setting goals, tracking progress, and making decisions. However, it can also lead to a focus on short-term results at the expense of long-term sustainability and adaptability.

This tree-like structure is similar to the tree structure in computer science, where the problem is divided into smaller subproblems, and each subproblem is solved independently. the disadvantage of this approach is that it can lead to siloed thinking, discouraging self-organization and collaboration between teams. team members tend to follow orders from the top without sufficient communication with others, which can lead to inefficiency, duplication of effort.

## dynamic systems approach in management
In contrast, the dynamic systems approach emphasizes the interactions between individuals and teams, and the emergent properties that arise from these interactions. Rather than breaking down problems into isolated components, this approach goes from the parts to the whole, understanding the backgroud from the parts.

This approach recognizes that complex problems cannot be solved by optimizing individual components in isolation, but require a holistic understanding of the system as a whole. By focusing on relationships, feedback loops, and self-organization, managers can create an environment that fosters creativity, innovation, and adaptability.

specifically, the concept of self-organization can be applied to management by creating a culture of trust, autonomy, and collaboration. By empowering employees to take ownership of their work, make decisions, and experiment with new ideas, managers can tap into the collective intelligence of the organization and unleash its full potential. This approach requires a shift from a command-and-control mindset to a facilitative leadership style that supports and empowers employees to self-organize and co-create value. 

Currently some companies claim to be using this approach with flat organization structure, etc, but it's still a long way to go to fully embrace the dynamic systems approach.

# reductionism
reductionism is a philosophical approach that seeks to explain complex phenomena by reducing them to simpler components. This approach has been highly successful in some fields since the industrial revolution, such as mechanics, physics, chemistry, engineering, computer science,etc.

It is also similar to the greedy algorithm in computer science, which seeks to solve complex optimization problems by making locally optimal choices at each step. While this approach can be effective in some cases, it can also lead to suboptimal solutions rather than the global optimum.

This methodology is so popular because it's easy to understand for human mind and implement, and it's also easy to measure the performance of the system. It's also very compatible with the current society structure, where the power is centralized and the decision-making process is top-down.

However, reductionism has its limitations when applied to complex systems that exhibit emergent properties, such as consciousness, intelligence, and social behavior.
However, it's not always the best approach to solve complex problems, as it can lead to tunnel vision, siloed thinking, and missed opportunities for innovation and creativity.


## emergence
the contrary of reductionism is called emergence, which is the idea that complex systems can exhibit properties that cannot be explained by analyzing their individual components in isolation. Instead, these properties arise from the interactions between components, leading to new behaviors, patterns, and structures that are not present at the micro level.

# thoughts about another approach
The reductionist approach is based on the idea that complex systems can be understood by breaking them down into simpler components, thus we can understand the whole system by understanding the parts. However, this approach has limitations when applied to complex systems, as the interactions between components can lead to emergent properties that cannot be predicted from the individual components alone.

Thinking in another way, we can consider the system as a whole, and study the interactions between components to understand the system's behavior. This is similar to category theory, where the focus is on the relationships between objects rather than the objects themselves. 

We still want to analyze properties of the system, but we give up the idea of predicting the future behavior of the system. 


# ref:

Nonlinear dynamics and Chaos by Steven Strogatz