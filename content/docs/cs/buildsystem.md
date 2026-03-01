+++
title = "build systems"
weight = 1
+++

This article aims to be a mathematical(algebraic) introduction to build systems, and their design and implementation issues. This will be helpful for:
- software developers who are frustrated by the complexity of many build systems
- software engineers who is new to build systems, but is mathematically inclined so he wants to understand the theory first.
- people who are interested in build systems and want to understand them from a theoretical perspective
- theoretical computer scientists or math hobbyists who want to see the application of directed acyclic graphs.


During the career of a software developer, you will encounter different build systems, and they are often a source of confusion and frustration, although they are usually not the focus of the project. Just to list a few build tools: Make, CMake, Bazel, Ninja, SBT, Mill, gradle, Maven, etc, Each has distinct features and requires learning when you switch between different software projects. 

Nowadays, as the software is becoming more complex, their build systems is getting more complex as well. So the obstacles of understanding the software project is not only the codebase itself, but also the build system that puts everything together. A while ago the Mill build system(written in Scala) sparked my interest(again) on how to understand build systems, so I decided to write this article to share my understanding as well as record my thoughts about build systems.


The core concepts of our discussion are:
- The definition of build systems
- The practical issues of build systems
- Designing a flexible build system based on explicit build graphs
- The implementation of build systems


## Definition of build systems
In general, a build system transforms the set of source files S into a set of target files T, so it's a function `b : S => T`. However, this is too abstract, and we discuss it in more details, so a build system mainly consists of:
1. A way to represent the codebase. This is usually represented as directed acyclic graph(DAG) where the nodes are tasks and the edges are dependencies between the tasks. We denote this as `Graph`. This `Graph` also contains other information, and the build system should provide a way to construct this `Graph` from the source files `S`. 
2. A mechanism to define, modify, and inspect the build/task graph. We denote the build graph as `Graph`, which is a directed acyclic graph(DAG). We let `Graph=(Nodes, Edges)`.
3. A mechanism to parameterize the build graph so it's modular and reusable. This can be denoted via function abstraction `A => Graph`, where `A` is the parameter type and `Graph` is the build graph. This allows us to define a build graph template that can be instantiated with different parameters.
4. A mechanism to represent the effect of executing the build graph, such as the input and output files, the environments, etc. For generality, we use `State` to represent the current state of the environment including all the input and output files, etc. 
5. The execution engine to execute the build graph, Denote as `exec: Graph => State => (Graph, State)`, which takes a build graph and the current state, and produces a new build graph and a new state after execution.
6. Practical features like caching, incremental build, parallel build, dependency management, etc. Those can think of as details of the execution engine `exec`.

The second point is actually about designing a domain specific language(DSL) for users to write the build graph, and that's why there are so many different build systems, because they implement different DSLs(makefile,sbt file,etc) to construct the build graph. The third point is about how to make the build graph modular and reusable, which is important for large projects. The fourth point is about how to execute the build graph, which is also important for performance.

In real world, the build system may also include many other features, such as dependency management, artifact publishing, etc. But we will focus on the core features of build systems in this article.


To open the stage for the discussion, let's see a typical scenario.
A user defines the build graph using some DSL or API, depending on what they want. Then this build graph is transformed and enriched with more information, or combined with existing build graphs. Finally, the execution engine executes the build graph to produce the desired targets. Later, users may inspect the build graph to see what tasks are defined, what dependencies are there, etc. The user may also modify the build graph to add more tasks or change existing tasks, where the parameterization mechanism helps a lot.


### The build graph
As mentioned above, the build graph(aka task graph) `Graph=(Nodes, Edges)` is a directed graph where the nodes are operations/tasks and the edges are dependencies between the operations. However, there is no ideal way to define the build graph, which contains extra information(operation, files, parameters, etc).

One possible way is to formalize via functions:
- A node in `Nodes` contains a unique identifier, a name(for readability), and an operation `op: State => State` that transforms the state of the environment.
- An edge in `Edges` is a directed edge from one node to another, indicating that the target node depends on the source node. This means that the operation of the target node can only be executed after the operation of the source node has been executed.


Another way is to use a wrapper type `T[A]` for the nodes, where `A` is the type of the output. An edge is a function: `edge:T[A] => T[B]=> Edge`, meaning that the output of the first node is the input of the second node. we shall note that:
- `T[B]` might be `A=>T[B]`
- 


For example, if we want to build a collection of java source files into a jar file, we can define the build graph as follows:
- each source file is contained in the information of the node
- the edges are defined by the dependencies between the source files, such as which source file imports which other source file, etc.
- the operation of each node is to compile the source file into a class file, and the operation of the final node is to package the class files into a jar file.

The code for the example with method 1 can be like this:
```scala
val sourceFile1: Node = Node(id = "sourceFile1", name = "Source
File 1", op = compileSourceFile("sourceFile1.java"))
val sourceFile2: Node = Node(id = "sourceFile2", name = "Source
File 2", op = compileSourceFile("sourceFile2.java"))
val jarFile: Node = Node(id = "jarFile", name = "Jar File",
op = packageJarFile(Set(sourceFile1, sourceFile2)))
val edge1: Edge = Edge(sourceFile1, jarFile)
val edge2: Edge = Edge(sourceFile2, jarFile)
val graph: Graph = Graph(Nodes = Set(sourceFile1, sourceFile2, jar
File), Edges = Set(edge1, edge2))
```

The code for the example with method 2 can be like this:
```scala
val sourceFile1: T[File] = T{ File("sourceFile1.java") }
val sourceFile2: T[File] = T{ File("sourceFile2.java") }
val jarFile: T[File] = T{ input => packageJarFile(Set(sourceFile1, sourceFile2)) }
val edge1: Edge = sourceFile1 --> jarFile
val edge2: Edge = sourceFile2 --> jarFile
val graph: Graph = Graph(Nodes = Set(sourceFile1, sourceFile2, jarFile), Edges = Set(edge1, edge2))
```

## practical issues
Let's discuss some practical issues:
 - Caching: to avoid rebuilding the same target
 - How to pass information between the nodes
 - Incremental build: to build only the changed targets
 - Parallel build: to build multiple targets in parallel
 - Dependency management: to manage the dependencies between the targets

Some of them are answered by the build graph:
- What tasks depends on what? use directed edges
- Where do input files come from? just read from the file system
- What needs to run in what order? topology sort
- What can be parallelized and what can’t? topological sort

Some issues are harder to answer:
- How to pass information between the nodes, like the output of one node to the input of another node?
- How to listen to events and do recompilation?


# Implementation
Constructing the build graph is a core feature of build systems, and it can be done in multiple ways, and we shall discuss some of them in detail. We categorize it into two ways:
- implicitly, like via function calls, like Mill and SBT
- explicitly via graph data structures(Makefile, Shake's DSL are this flavor)


Using function calls(like Mill):
- the nodes are function definitions and the edges are function calls. The final build graph is a composite function definition at top level.
- In more detail, the nodes are functions defined inside `T{}:T[A]`, enriching the function definition with more information needed for the build system.
- Parameterization and modularity are achieved via function parameters, class/trait based subtyping(inheritance, mixin, overriding).
- The inspection of the build graph may need help from meta-programming to record the function calls.
- Modification of the build graph is equal modify the final composite function, which may be hard and limited to pre and post composition. However, this is not a big issue since we can write a top level function to invoke the previously defined util functions.


Using function calls with imperative style(like SBT):
- the nodes are function definitions wrapped in `TaskKey` which is mutable, and the edges are delayed function calls `taskKey.value`(delayed because execution engine will decide the execution order later). This needs help from macros, a meta-programming feature in Scala.
- Since the `TaskKey` is mutable, it can help with the modification of the build graph, but it may be hard to track the changes.
- In contrast, the nodes in Mill are immutable.


Using graph data structures:
- the nodes and edges are explicitly defined. 
- The inspection and modification of the build graph is straightforward via standard graph algorithms once the particular nodes and edges are identified. 

## An ideal build system
Having discussed the implicit and explicit ways, we imagine an build system that is explicit but also has the flexibility of the implicit way:
- the build graph is explicitly defined as DAG, so inspection and manipulation is easier
- nodes and edges can be identified and modified later after construction of the build graph, for reusability.
- split into multiple stages: graph construction, graph transformation, graph execution, so that we can have more control over the build process, and also make it easier to implement features like caching, incremental build, parallel build, etc.
- utilize the concepts of graph for other features of the build system, such as caching, incremental build, parallel build, etc. For example, we can use the graph structure to determine which nodes need to be rebuilt when a source file changes, or which nodes can be executed in parallel.

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