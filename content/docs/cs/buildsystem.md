+++
title = "build systems"
weight = 1
+++

This article aims to be a mathematical(or algebraic) introduction to build systems, as well as a formal definition and practical issues about build systems. 

Specifically, we aim to present:
- The definition of build systems
- Other mathematical concepts used in build systems
- The practical issues of build systems
- Designing a flexible build system based on explicit build graphs
- The implementation of build systems



The above build tools are practical and uses functional programming concepts, but they do not operate explicitly on build graphs. In contrast, this document aims to discuss more on the theoretical side.

## Definition
A build system mainly consists of:
1. A mechanism to define, modify, and inspect the build/task graph
2. A mechanism to parameterize the build graph so it's modular and reusable
3. The execution engine to execute the build graph
4. Practical features like caching, incremental build, parallel build, etc.

A scenario is that users define the build graph using some DSL or API, depending on what they want. Then this build graph is transformed and enriched with more information, or combined with existing build graphs. Finally, the execution engine executes the build graph to produce the desired targets. Later, users may inspect the build graph to see what tasks are defined, what dependencies are there, etc. The user may also modify the build graph to add more tasks or change existing tasks, where the parameterization mechanism helps a lot.


## The build graph
The build graph is a directed graph where the nodes are operations and the edges are dependencies between the operations. It specifies the dependencies between the tasks.

For example, if we want to build the linux kernel Image, then the node may have the following:
1. The node name is "kernelImage"
2. The node id is 1
3. The node info is the make command to build the kernel Image

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

## An ideal build system
To keep the theoretical beauty and make it flexible, here are some points to consider:
- explicit build graph representation so inspection and manipulation is easier
- nodes and edges can be identified and modified later after construction of the build graph
- split into multiple stages: graph construction, graph transformation, graph execution
- utilize the concepts of graph for other features of the build system, such as caching, incremental build, parallel build

# Implementation
Constructing the build graph can be done in multiple ways, and we shall discuss some of them in detail:
Using function calls:
- the nodes are function definitions and the edges are function calls. The final build graph is a composite function definition at top level.
- Parameterization is just function parameters.
- The inspection of the build graph may need help from meta-programming to record the function calls.
- Modification of the build graph is to modify the final composite function, which may be hard and limited to pre and post composition.
  
  
Using graph data structures:
- the nodes and edges are explicitly defined. 
- The inspection and modification of the build graph is straightforward.
## Examples
Some noteable build systems in functional flavor are:
- [SBT](https://www.scala-sbt.org/): Scala's de facto build tool, imperative style using `TaskKey` to build the task graph
- [Mill](https://www.lihaoyi.com/mill/): Mainly for Scala, more functional style using function calls to build the task graph
- [Haskell's Shake](https://shakebuild.com/): a eDSL in Haskell that mimics Make but more powerful

And some other popular build systems are:
- [Make](https://www.gnu.org/software/make/): the classic build system using Makefiles, declare the build graph using `node`s in Makefiles
- [Bazel](https://bazel.build/)
- [Ninja](https://ninja-build.org/)

We list some existing build systems and their features in a table:
| Build System | graph construction                | task graph inspection |
| ------------ | --------------------------------- | --------------------- |
| Sbt          | imperative `TaskKey` reassignment |                       |
| Mill         | function calls                    | mill `visualize`      |
| Make         | `node` in Makefile                |                       |
| Shake        | `node` in Haskell                 |                       |

# Other thoughts
Hi, I'm wondering if Mill can be used as a build system to replace Make? like for building linux kernel? Maybe some integration with os-lib would help?

Wow thanks that's cool! Could you point me to the documentation? I guess it's related to the section Building Javascript with Mill

thanks, I'm thinking about writing some build scripts in Mill that invoke the old makefiles, which will be easier initially. 

I'm also writing an article about build systems from a mathematical perspective, will share it later.