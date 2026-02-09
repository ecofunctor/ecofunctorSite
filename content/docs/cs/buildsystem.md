+++
title = "build systems"
weight = 1
+++

This article aims to be a mathematical(algebraic) introduction to build systems, and their design and implementation issues. 

Just to list a few build tools: Make, CMake, Bazel, Ninja, SBT, Mill, gradle, Maven, etc, Each has distinct features and requires learning when you switch between different software projects. 

A while ago Mill sparked my interest on how to understand build systems from a mathematical perspective. As the software is becoming more complex, their build systems is getting more complex as well, so the obstacles of understanding the project is not only the code itself, but also the process of building the code, which is much less formalized than the theory of programming languages. I hope this article can help  to understand build systems in a theoretical way.


The core concepts of our discussion are:
- The definition of build systems
- Other mathematical concepts used in build systems
- The practical issues of build systems
- Designing a flexible build system based on explicit build graphs
- The implementation of build systems


## Definition of build systems
A build system mainly consists of:
1. A mechanism to define, modify, and inspect the build/task graph. We denote the build graph as `Graph`, which is a directed acyclic graph.
2. A mechanism to parameterize the build graph so it's modular and reusable. This can be denoted via function abstraction `A => Graph`, where `A` is the parameter type and `Graph` is the build graph. This allows us to define a build graph template that can be instantiated with different parameters.
3. A mechanism to represent the effect of executing the build graph, such as the input and output files, the environments, etc. For generality, we use `State` to represent the current state of the environment including all the input and output files, etc. 
4. The execution engine to execute the build graph, Denote as `exec: Graph => State => (Graph, State)`, which takes a build graph and the current state, and produces a new build graph and a new state after execution.
5. Practical features like caching, incremental build, parallel build, dependency management, etc. Those can think of as details of the execution engine `exec`.

The first point is actually about designing a domain specific language(DSL) for users to write the build graph, and that's why there are so many different build systems, because they implement different DSLs to construct the build graph. The second point is about how to make the build graph modular and reusable, which is important for large projects. The third point is about how to execute the build graph, which is also important for performance.

In real world, the build system may also include many other features, such as dependency management, artifact publishing, etc. But we will focus on the core features of build systems in this article.


To open the stage for the discussion, let's see a typical scenario.
A user defines the build graph using some DSL or API, depending on what they want. Then this build graph is transformed and enriched with more information, or combined with existing build graphs. Finally, the execution engine executes the build graph to produce the desired targets. Later, users may inspect the build graph to see what tasks are defined, what dependencies are there, etc. The user may also modify the build graph to add more tasks or change existing tasks, where the parameterization mechanism helps a lot.


## The build graph
The build graph is a directed graph where the nodes are operations and the edges are dependencies between the operations. It specifies the dependencies between the tasks. It's also called the task graph.

For example, if we want to build the linux kernel Image, then the node may have the following:
1. The node name is "kernelImage"
2. The node id is 1
3. The node operation is to compile the kernel source code

## practical issues
Practical issues aside from the mathematical beauty of build systems:
 - Caching: to avoid rebuilding the same target
 - How to pass information between the nodes
 - Incremental build: to build only the changed targets
 - Parallel build: to build multiple targets in parallel
 - Dependency management: to manage the dependencies between the targets

The Task Graph is a directed acyclic graph where the nodes are tasks:
- What tasks depends on what? use directed edges
- Where do input files come from? just read from the file system
- What needs to run in what order? topology sort
- What can be parallelized and what can’t? topological sort

Some issues are hard to solve:
- How to pass information between the nodes, like the output of one node to the input of another node?
- How to listen to events and do recompilation?


# Implementation
Constructing the build graph is one of the core features of a build system, and it can be done in multiple ways, and we shall discuss some of them in detail.

Using function calls(like Mill):
- the nodes are function definitions and the edges are function calls. The final build graph is a composite function definition at top level.
- In more detail, the nodes are functions defined inside `T{}:T[A]`, enriching the function definition with more information needed for the build system.
- Parameterization and modularity are achieved via function parameters, class/trait based subtyping(inheritance, mixin, overriding).
- The inspection of the build graph may need help from meta-programming to record the function calls.
- Modification of the build graph is equal modify the final composite function, which may be hard and limited to pre and post composition. However, this is not a big issue since we can write a top level function to invoke the previously defined util functions.


Using function calls with imperative style(like SBT):
- the nodes are function definitions wrapped in `TaskKey` which is mutable, and the edges are delayed function calls `taskKey.value`(delayed because execution engine will decide the execution order later). This needs help from macros, a meta-programming feature in Scala.
- Since the `TaskKey` is mutable, it can help with the modification of the build graph, but it may be hard to track the changes.
- In contrast with Mill, the nodes in Mill are immutable.


Using graph data structures:
- the nodes and edges are explicitly defined. 
- The inspection and modification of the build graph is straightforward via standard graph algorithms.

## An ideal build system
To keep the theoretical beauty and make it flexible, here are some points to consider:
- explicit build graph representation so inspection and manipulation is easier
- nodes and edges can be identified and modified later after construction of the build graph
- split into multiple stages: graph construction, graph transformation, graph execution
- utilize the concepts of graph for other features of the build system, such as caching, incremental build, parallel build

## Examples
Some noteable build systems in functional flavor are:
- [SBT](https://www.scala-sbt.org/): Scala's de facto build tool, imperative style using `TaskKey` to build the task graph
- [Mill](https://www.lihaoyi.com/mill/): Mainly for Scala, more functional style using function calls to build the task graph
- [Haskell's Shake](https://shakebuild.com/): a eDSL in Haskell that mimics Make but more powerful

And some other popular build systems are:
- [Make](https://www.gnu.org/software/make/): the classic build system using Makefiles, declare the build graph using `node`s in Makefiles
- [Bazel](https://bazel.build/)
- [Ninja](https://ninja-build.org/)

We sommarize the features of the build systems according to the core concepts:

| Build System | graph node                   | graph edge      | graph inspection |
| ------------ | ---------------------------- | --------------- | ---------------- |
| Sbt          | `TaskKey` assign/reassign    | `taskKey.value` | `inspect`        |
| Mill         | function def wrapped in`T{}` | function call   | mill `visualize` |
| Make         | `node` in Makefile           |                 |                  |
| Shake        | `node` DSL in Haskell        |                 |                  |

# References
- [How mill works](https://www.lihaoyi.com/post/SoWhatsSoSpecialAboutTheMillScalaBuildTool.html)