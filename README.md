# Cluster LLVM (`cluster-llvm`)

Pure Native LLVM Intermediate Representation (IR), Builder, Optimizer, and Decompilation Lifter written in **100% Pure Cluster Language (`.zk` / `.cl`)**.

> **Zero External Dependencies**: Does not link against libLLVM.so or C++ runtimes. Compiles directly into native machine code with the Cluster compiler (`cl`).

---

## Architecture Overview

```
cluster-llvm/
├── package.zk                # Package manifest with CCFL v2.0 terms
├── src/
│   ├── ir/
│   │   ├── types.zk          # Strongly typed LLVM type system
│   │   ├── instructions.zk   # LLVM instruction model, opcodes & IR string emitter
│   │   └── builder.zk        # High-level IRBuilder, BasicBlock & Module manager
│   ├── parser/
│   │   ├── lexer.zk          # Lexer for LLVM textual IR (.ll)
│   │   └── parser.zk         # AST parser for .ll files
│   ├── transform/
│   │   ├── pass_manager.zk   # Optimization pass manager
│   │   ├── const_fold.zk     # Constant folding pass
│   │   └── dce.zk            # Dead code elimination pass
│   └── lifter/
│       ├── cfg.zk            # Control flow graph analyzer & loop detector
│       ├── relooper.zk       # Relooper algorithm (unstructured jumps -> structured loops)
│       └── decompiler.zk     # Emits idiomatic Cluster code (.zk / .cl)
└── tests/
    └── test_ir.zk            # IR Builder & LLVM emission verification tests
```

---

## Quick Start

### 1. Verification & Testing
Run the test suite using the native Cluster compiler:
```bash
cl run tests/test_ir.zk
```

---

## Contributor & Stewardship

- **Contributor**: Mohammad Zaid `<zkalamgir@proton.me>`
- **Copyright Stewardship**: Managed by Mohammad Zaid / cluster under CCFL v2.0 Terms.
