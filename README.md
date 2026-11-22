# Cluster LLVM (`cluster-llvm`)

Pure Native LLVM Intermediate Representation (IR), Builder, Text Parser, In-Memory Execution Engine, Optimizer, Multi-Target Assembly Code Generator (x86_64, ARM64, WASM), and Decompilation Lifter written in **100% Pure Cluster Language (`.zk` / `.cl`)**.

> 🚀 **100% Zero External Dependencies**: Does not link against `libLLVM.so` or external C++ runtimes. Compiles directly into native machine code with the Cluster compiler (`cl`).

---

## 🏗️ Architecture Overview

```
cluster-llvm/
├── package.zk                # Package manifest with CCFL v2.0 terms (v1.0.0)
├── README.md                 # Complete architecture and usage documentation
├── src/
│   ├── main.zk               # Unified demonstration and pipeline driver
│   ├── llvm.zk               # Master unified facade
│   ├── ir/
│   │   ├── types.zk          # Strongly typed LLVM type system (i1..i64, ptr, float, array, void)
│   │   ├── instructions.zk   # LLVM opcodes (arithmetic, bitwise, icmp, alloca, load, store, GEP, PHI, call)
│   │   └── builder.zk        # BasicBlock, Function, Module & IRBuilder API
│   ├── parser/
│   │   ├── lexer.zk          # Streaming tokenizer for LLVM textual IR (.ll)
│   │   └── parser.zk         # AST parser for textual LLVM IR modules & functions
│   ├── transform/
│   │   ├── const_fold.zk     # Compile-time constant folding optimization pass
│   │   ├── dce.zk            # Dead code elimination (DCE) optimization pass
│   │   └── inliner.zk        # Function inliner optimization pass for leaf calls
│   ├── execution/
│   │   └── interpreter.zk    # In-memory virtual machine & execution engine with GEP & PHI
│   ├── target/
│   │   ├── x86_64/
│   │   │   ├── registers.zk  # AMD64/x86_64 register ABI
│   │   │   └── emitter.zk    # Direct x86_64 assembly code generator
│   │   ├── aarch64/
│   │   │   ├── registers.zk  # ARM64/Apple Silicon register ABI
│   │   │   └── emitter.zk    # Direct ARM64 assembly code generator
│   │   └── wasm/
│   │       └── emitter.zk    # WebAssembly (WASM) Text WAT generator
│   └── lifter/
│       ├── decompiler.zk     # Decompiles LLVM IR back into pure Cluster code (.zk / .cl)
│       └── relooper.zk       # Loop structurizer (detects loops -> native while loops)
└── tests/
    ├── test_ir.zk            # IR construction and .ll text emission tests
    ├── test_parser.zk        # LLVM IR text lexer and parser verification tests
    ├── test_interpreter.zk   # Virtual machine execution engine tests
    ├── test_lifter.zk        # Constant folding and Cluster code decompilation tests
    ├── test_dce.zk           # Dead code elimination pass tests
    ├── test_relooper.zk      # Relooper while loop recovery tests
    ├── test_gep_struct.zk    # Struct GEP offset & SSA PHI node resolution tests
    ├── test_inliner.zk       # Function inliner optimization pass tests
    └── test_targets.zk       # Multi-target hardware emitter tests (x86_64, ARM64, WASM)
```

---

## 🚀 Key Subsystems & Features

1. **Native LLVM IR Builder**:
   - Construct typed `Module`, `Function`, `BasicBlock`, and `Instruction` models.
   - Dump valid textual `.ll` code that compiles directly with standard `clang` or `llc`.
2. **Textual LLVM IR Parser**:
   - Parse raw LLVM IR `.ll` code into structured in-memory AST.
3. **In-Memory Interpreter**:
   - Evaluate LLVM functions directly in memory with virtual register bindings and simulated pointer memory.
   - Full support for `OP_GEP` (struct offset indexing) and `OP_PHI` (dynamic SSA branch convergence).
4. **Optimization Pipeline**:
   - **Constant Folding**: Compile-time constant calculation (`40 + 2` $\to$ `42`).
   - **Dead Code Elimination (DCE)**: Prunes unused instructions and dead registers.
   - **Function Inliner**: Inlines leaf function calls into caller blocks to eliminate call overhead.
5. **Multi-Target Hardware Code Generators**:
   - Native **x86_64** GNU/NASM assembly generator.
   - Native **AArch64** (ARM64 / Apple Silicon) assembly generator.
   - Native **WebAssembly (WASM)** WAT text format generator.
6. **Cluster Lifter & Relooper**:
   - Converts unstructured branch graphs back into high-level, structured Cluster **`while`** loops and conditionals.

---

## 🧪 Pipeline Demo & Test Suite Execution

### 1. Run Complete Architecture Demo
```bash
cl run src/main.zk
```

### 2. Run All 9 Verification Test Suites
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

# 7. Test Struct GEP & PHI Resolution
cl run tests/test_gep_struct.zk

# 8. Test Function Inliner Pass
cl run tests/test_inliner.zk

# 9. Test Hardware Emitters (x86_64, ARM64, WASM)
cl run tests/test_targets.zk
```

---

## 📜 Contributor & Stewardship

- **Contributor**: Mohammad Zaid `<zkalamgir@proton.me>`
- **Copyright Stewardship**: Managed by Mohammad Zaid / cluster under CCFL v2.0 Terms.
