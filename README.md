# Cluster LLVM (`cluster-llvm`)

Pure Native LLVM Intermediate Representation (IR), Builder, Text Parser, In-Memory Execution Engine, Optimizer, and Decompilation Lifter written in **100% Pure Cluster Language (`.zk` / `.cl`)**.

> 🚀 **100% Zero External Dependencies**: Does not link against `libLLVM.so` or external C++ runtimes. Compiles directly into native machine code with the Cluster compiler (`cl`).

---

## 🏗️ Architecture Overview

```
cluster-llvm/
├── package.zk                # Package manifest with CCFL v2.0 terms
├── README.md                 # Complete architecture and usage documentation
├── src/
│   ├── main.zk               # Unified demonstration and pipeline driver
│   ├── llvm.zk               # Master unified facade
│   ├── ir/
│   │   ├── types.zk          # Strongly typed LLVM type system (i1..i64, ptr, float, array)
│   │   ├── instructions.zk   # LLVM opcodes & valid textual .ll code emitter
│   │   └── builder.zk        # BasicBlock, Function, Module & IRBuilder API
│   ├── parser/
│   │   ├── lexer.zk          # Streaming tokenizer for LLVM textual IR (.ll)
│   │   └── parser.zk         # AST parser for textual LLVM IR modules & functions
│   ├── transform/
│   │   ├── const_fold.zk     # Compile-time constant folding optimization pass
│   │   └── dce.zk            # Dead code elimination (DCE) optimization pass
│   ├── execution/
│   │   └── interpreter.zk    # In-memory virtual machine & execution engine
│   └── lifter/
│       ├── decompiler.zk     # Decompiles LLVM IR back into pure Cluster code (.zk / .cl)
│       └── relooper.zk       # Loop structurizer (detects loops -> native while loops)
└── tests/
    ├── test_ir.zk            # IR construction and .ll text emission tests
    ├── test_parser.zk        # LLVM IR text lexer and parser verification tests
    ├── test_interpreter.zk   # Virtual machine execution engine tests
    ├── test_lifter.zk        # Constant folding and Cluster code decompilation tests
    ├── test_dce.zk           # Dead code elimination pass tests
    └── test_relooper.zk      # Relooper while loop recovery tests
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
   - **Constant Folding**: Compile-time constant calculation.
   - **Dead Code Elimination (DCE)**: Prunes unused instructions and dead registers.
5. **Cluster Lifter & Relooper**:
   - Converts unstructured branch graphs back into high-level, structured Cluster `while` loops and conditionals.

---

## 🧪 Pipeline Demo & Test Suite Execution

### 1. Run Complete Architecture Demo
```bash
cl run src/main.zk
```

### 2. Run All 6 Verification Test Suites
```bash
# 1. Test IR Builder & Text Emission
cl run tests/test_ir.zk

# 2. Test LLVM IR Lexer & Parser
cl run tests/test_parser.zk

# 3. Test In-Memory Execution Engine
cl run tests/test_interpreter.zk

# 4. Test Decompiler Lifter & Optimizations
cl run tests/test_lifter.zk

# 5. Test Dead Code Elimination
cl run tests/test_dce.zk

# 6. Test Relooper Loop Structurizer
cl run tests/test_relooper.zk
```

---

## 📜 Contributor & Stewardship

- **Contributor**: Mohammad Zaid `<zkalamgir@proton.me>`
- **Copyright Stewardship**: Managed by Mohammad Zaid / cluster under CCFL v2.0 Terms.
