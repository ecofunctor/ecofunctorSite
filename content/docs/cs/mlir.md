+++
title = "MLIR compilers"
weight = 3
+++

This article introduces basics of MILR(Multi-Level Intermediate Representation) compilers framework, which is a set of languages and tools for building compilers.

## Dialects: languages in MLIR
The MLIR project predefines several dialects, which are different intermediate representation languages for different purposes(optimizations, target hardware, etc).

## transforming dialects
Another crucial part of MLIR is letting users transform dialects easily. 

### C++ API
MLIR only provides C++ API for transforming dialects. 

references:
- [MLIR official documentation](https://mlir.llvm.org/docs/)