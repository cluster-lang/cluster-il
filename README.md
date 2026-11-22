# Cluster LLVM (`cluster-llvm`)

Pure Native LLVM Intermediate Representation (IR), Builder, Text Parser, In-Memory Execution Engine, Optimizer, and Decompilation Lifter written in **100% Pure Cluster Language (`.zk` / `.cl`)**.

> 🚀 **100% Zero External Dependencies**: Does not link against `libLLVM.so` or external C++ runtimes. Compiles directly into native machine code with the Cluster compiler (`cl`).

---

## 🏗️ Architecture Overview

```
cluster-llvm/
├── package.zk                # Package manifest with CCFL v2.0 terms
├── README.md                 # Architecture, specifications, and quickstart
├── src/
│   ├── llvm.zk               # Master unified framework facade
│   ├── ir/
│   │   ├── types.zk          # Strongly typed LLVM type system (i1..i64, ptr, float, array)
│   │   ├── instructions.zk   # LLVM opcodes & valid textual .ll code emitter
│   │   └── builder.zk        # BasicBlock, Function, Module & IRBuilder API
│   ├── parser/
│   │   ├── lexer.zk          # Streaming tokenizer for LLVM textual IR (.ll)
│   │   └── parser.zk         # Recursive-descent AST parser for .ll modules
│   ├── transform/
│   │   └── const_fold.zk     # Constant folding optimization pass
│   ├── execution/
│   │   └── interpreter.zk    # Pure Cluster in-memory LLVM IR execution engine
│   └── lifter/
│       └── decompiler.zk     # Decompiles LLVM IR back into pure Cluster code (.zk / .cl)
└── tests/
    ├── test_ir.zk            # IR construction and .ll text emission tests
    ├── test_parser.zk        # LLVM IR text lexer and parser verification tests
    ├── test_interpreter.zk   # Virtual machine execution engine tests
    └── test_lifter.zk        # Constant folding and Cluster code decompilation tests
```

---

## 🚀 Key Subsystems & Features

1. **Native LLVM IR Builder**:
   - Construct typed `Module`, `Function`, `BasicBlock`, and `Instruction` models.
   - Dump valid textual `.ll` code that compiles directly with standard `clang` or `llc`.
2. **Textual LLVM IR Parser**:
   - Parse raw LLVM IR `.ll` code into structured in-memory AST.
3. **In-Memory Interpreter**:
   - Evaluate LLVM functions directly in memory with virtual register bindings without needing an external native compiler.
4. **Optimization Pipeline**:
   - Compile-time constant folding and instruction simplification.
5. **Cluster Lifter (Decompiler)**:
   - Lift LLVM IR basic blocks and instructions back into clean, high-level Cluster Language code.

---

## 🧪 Test Suite Execution

All test suites run natively via `cl run`:
```bash
# 1. Test IR Builder & Text Emission
cl run tests/test_ir.zk

# 2. Test LLVM IR Lexer & Parser
cl run tests/test_parser.zk

# 3. Test In-Memory Execution Engine
cl run tests/test_interpreter.zk

# 4. Test Decompiler Lifter & Optimizations
cl run tests/test_lifter.zk
```

---

## 📜 Contributor & Stewardship

- **Contributor**: Mohammad Zaid `<zkalamgir@proton.me>`
- **Copyright Stewardship**: Managed by Mohammad Zaid / cluster under CCFL v2.0 Terms.
