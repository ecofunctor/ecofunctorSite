+++
title = "MLIR compilers"
weight = 3
+++

This article introduces basics of MILR(Multi-Level Intermediate Representation) compilers framework, which is a set of languages and tools for building compilers. We aim to cover:
- MLIR syntax and dialects
- Transforming dialects: How to write a pass

Aside from that the compilers are inherently difficult to learn. We also discuss the difficulties in learning MLIR:
- lack of systematic tutorials and documentation
- C++ api documentation is nonexistent aside from source code
- complex build system based on CMake and Ninja
- TableGen, another language on top of C++
- C++ is a complex language itself
- lots of concepts: Operations, Regions, Blocks, Values, Types, Attributes, Dialects, Passes, Patterns, etc.
- no clear separation between llvm, MLIR, CIRCT
- in addition, there are many algorithms for AI optimizations, hardware synthesis, etc.

## Dialects: languages in MLIR
**General syntax of MLIR**

MLIR is fundamentally based on a graph-like data structure of nodes, called Operations, and edges, called Values. Each Value is the result of exactly one Operation or Block Argument, and has a Value Type defined by the type system. Operations are contained in Blocks and Blocks are contained in Regions.

The syntax for the IR is defined like this:

```
Operation
    list of Regions
    Region
        list of Blocks
        Block
            list of Block Arguments
            list of Operations
```

Example MLIR code:
```
module {
  // a region started  
  func @my_function(%arg0: i32, %arg1: i32) -> i32 {
    // another region started
    %0 = addi %arg0, %arg1 : i32
    return %0 : i32
  }
}
```
Here `module` is an Operation called `moduleOp`, which contains a Region. The Region contains a Block, which contains two Operations: `funcOp` and `returnOp`. The `funcOp` contains another Region, which contains a Block with two Operations: `addiOp` and `returnOp`. The `%arg0` and `%arg1` are Block Arguments, and `%0` is a Value produced by the `addiOp`.


There are several types of regions in MLIR:
- graph region: concurrent semantics, not sequential

**Dialects in MLIR**
The MLIR project predefines several dialects, which are different intermediate representation languages for different purposes(optimizations, target hardware, etc).

## transforming dialects
Another crucial part of MLIR is letting users transform dialects easily. 

### C++ API
MLIR only provides C++ API for transforming dialects. 
The main entry is `runOnOperation()` :

```cpp
void MyPass::runOnOperation() {
  // get the current operation
  Operation *op = getOperation();

  // traverse all operations in the current operation
  op->walk([](Operation *nestedOp) {
    // perform transformations on nestedOp
  });
  // or manually iterate over regions
  op->getRegions()
}
```
A Region does not hold anything other than a list of Blocks. A Block holds a list of arguments and a list of Operations. 


**traversing with helper functions `walk()`**

MLIR exposes the walk() helper on Operation, Block, and Region. This helper takes a single argument: a callback method that will be invoked for every operation recursively:
```cpp
getFunction().walk([](Operation *op) {
  // perform transformations on op
});
// can also pattern-match on specific types of operations
getFunction().walk([](AddIOp addOp) {
  // perform transformations on addOp
});
```

the walk process can be stopped or continued:
```cpp
getFunction().walk([](Operation *op) {
  if (shouldStop(op)) {
    return WalkResult::interrupt(); // stop walking
  }
  // perform transformations on op
  return WalkResult::advance(); // continue walking
});
```

**putting it all together**
We use the CIRCT project as an example. Compile the CIRCT project after following the instructions [here](https://circt.llvm.org/getting_started/):
``` bash
# Configure the build Debug
# DCMAKE_BUILD_TYPE = RelWithDebInfo, Debug, Release
cmake -G Ninja llvm/llvm -B build \
    -DCMAKE_BUILD_TYPE=Release \ 
    -DLLVM_ENABLE_ASSERTIONS=ON \
    -DLLVM_TARGETS_TO_BUILD=host \
    -DLLVM_ENABLE_PROJECTS=mlir \
    -DLLVM_EXTERNAL_PROJECTS=circt \
    -DLLVM_EXTERNAL_CIRCT_SOURCE_DIR=$PWD
    -DLLVM_ENABLE_LLD=ON

# Build the circt-opt tool
ninja -C build bin/circt-opt
```

To summarize the steps:
- Define the pass in TableGen (.td file).
- Generate headers using TableGen.
- Implement the pass logic in a C++ (.cpp file).
- Register the pass in the build system (CMakeLists.txt).
- Build the project to compile the new pass.

### Scala API
There's some experimental Scala API for MLIR:
- [Scair](https://github.com/edin-dal/scair)
- [Java CPP bindings](https://github.com/sequencer/zaozi/tree/master/mlirlib/src/capi)


First we introduce the basic usage of Scair.

For an example snippet of MLIR code:
```
%0 = "arith.constant"() <{value = 5}> : () -> i32
%1 = "arith.constant"() <{value = 5}> : () -> i32
%2 = "arith.addi"(%0, %1) : (i32, i32) -> i32
func.call @print(%2) : (i32) -> ()
```
We can write a pattern to fold the addition of two constant integers:
```scala
val AddIFold = pattern {
	case AddI(
		Owner(Constant(c0: IntegerAttr, _)),
		Owner(Constant(c1: IntegerAttr, _)),
		_
	) =>
		Constant(c0 + c1, Result(c0.typ))
}
```

references：
- (Scair tutorial)[https://edin-dal.github.io/scair/docs/transformations.html]

## References and further reading
references:
- (mlir syntax)[https://mlir.llvm.org/docs/LangRef/#high-level-structure]
- (mlir traversal api)[https://mlir.llvm.org/docs/Tutorials/UnderstandingTheIRStructure/]