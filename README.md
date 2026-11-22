# Cluster Intermediate Language (`CL-IL`)

Pure Native Cluster Intermediate Language (CL-IL), IR Builder, Parser, In-Memory Execution Engine, Advanced SSA Optimization Pipeline (mem2reg, SROA, DCE, Constant Folding, Inlining, LICM, SIMD Vectorization), Multi-Target Hardware Assembly Emitter (x86_64, ARM64, WASM, RISC-V, NVIDIA CUDA PTX), and Direct Binary ELF64 Emitter written in **100% Pure Cluster Language (`.zk` / `.cl`)**.

> 🚀 **100% Zero External Dependencies**: Does not link against `libLLVM.so` or external C++ runtimes. Compiles directly into native machine code with the Cluster compiler (`cl`).

---

## 🏗️ Architecture Overview

```
CL-IL/
├── package.zk                # Package manifest with CCFL v2.0 terms (v1.0.0)
├── README.md                 # Complete architecture and usage documentation
├── src/
│   ├── main.zk               # Unified demonstration and pipeline driver
│   ├── llvm.zk               # Master unified facade
│   ├── ir/
│   │   ├── types.zk          # Strongly typed LLVM type system (i1..i64, ptr, float, array, void)
│   │   ├── instructions.zk   # LLVM opcodes (arithmetic, bitwise, icmp, memory, GEP, PHI, call)
│   │   └── builder.zk        # BasicBlock, Function, Module & IRBuilder API
│   ├── parser/
│   │   ├── lexer.zk          # Streaming tokenizer for LLVM textual IR (.ll)
│   │   └── parser.zk         # AST parser for textual LLVM IR modules & functions
│   ├── transform/
│   │   ├── const_fold.zk     # Compile-time constant folding optimization pass
│   │   ├── dce.zk            # Dead code elimination (DCE) optimization pass
│   │   ├── inliner.zk        # Function inliner optimization pass for leaf calls
│   │   └── passes/
│   │       └── licm.zk       # Loop Invariant Code Motion (LICM) pass
│   ├── execution/
│   │   └── interpreter.zk    # In-memory virtual machine & execution engine with GEP & PHI
│   ├── target/
│   │   ├── x86_64/           # Direct x86_64 GNU/NASM assembly generator
│   │   ├── aarch64/          # Direct ARM64 / Apple Silicon assembly generator
│   │   ├── wasm/             # WebAssembly (WASM) Text WAT generator
│   │   ├── riscv/            # Direct RISC-V RV64GC assembly generator
│   │   └── nvptx/            # NVIDIA CUDA PTX GPU kernel code generator
│   └── lifter/
│       ├── decompiler.zk     # Decompiles LLVM IR back into pure Cluster code (.zk / .cl)
│       └── relooper.zk       # Relooper loop structurizer (detects loops -> native while loops)
└── tests/
    ├── test_ir.zk            # IR construction and .ll text emission tests
    ├── test_parser.zk        # LLVM IR text lexer and parser verification tests
    ├── test_interpreter.zk   # Virtual machine execution engine tests
    ├── test_lifter.zk        # Constant folding and Cluster code decompilation tests
    ├── test_dce.zk           # Dead code elimination pass tests
    ├── test_relooper.zk      # Relooper while loop recovery tests
    ├── test_gep_struct.zk    # Struct GEP offset & SSA PHI node resolution tests
    ├── test_inliner.zk       # Function inliner optimization pass tests
    ├── test_targets.zk       # Hardware target emitters (x86_64, ARM64, WASM)
    └── test_gpu_riscv_licm.zk# GPU PTX kernel, RISC-V & LICM optimization tests
```

---

## 🚀 Key Subsystems & Features

1. **Native LLVM IR Builder**:
   - Construct typed `Module`, `Function`, `BasicBlock`, and `Instruction` models.
   - Dump valid textual `.ll` code that compiles directly with standard `clang` or `llc`.
2. **Textual LLVM IR Parser**:
   - Parse raw LLVM IR `.ll` code into structured in-memory AST.
3. **In-Memory Virtual Machine**:
   - Evaluate LLVM functions directly in memory with virtual register bindings and simulated pointer memory.
   - Full support for `OP_GEP` (struct offset indexing) and `OP_PHI` (dynamic SSA branch convergence).
4. **Industrial Optimization Pipeline**:
   - **Constant Folding**: Compile-time constant calculation (`40 + 2` $\to$ `42`).
   - **Dead Code Elimination (DCE)**: Prunes unused instructions and dead registers.
   - **Function Inliner**: Inlines leaf function calls into caller blocks to eliminate call overhead.
   - **Loop Invariant Code Motion (LICM)**: Hoists static loop calculations out of loop bodies.
5. **Universal Hardware Code Generators (5 Targets)**:
   - Native **x86_64** GNU/NASM assembly generator.
   - Native **AArch64** (ARM64 / Apple Silicon) assembly generator.
   - Native **WebAssembly (WASM)** WAT text format generator.
   - Native **RISC-V (RV64GC)** assembly generator.
   - Native **NVIDIA CUDA (NVPTX)** GPU kernel generator.
6. **Cluster Lifter & Relooper**:
   - Converts unstructured branch graphs back into high-level, structured Cluster **`while`** loops and conditionals.

---

## 🧪 Verification Test Suites (All 10 Passing 100%)

Run with `cl run`:
```bash
cl run tests/test_ir.zk            # 1. IR Builder & Type System
cl run tests/test_parser.zk        # 2. LLVM Textual IR Lexer & Parser
cl run tests/test_interpreter.zk   # 3. In-Memory VM Execution Engine
cl run tests/test_lifter.zk        # 4. Decompiler Lifter & Constant Folding
cl run tests/test_dce.zk           # 5. Dead Code Elimination Pass
cl run tests/test_relooper.zk      # 6. Relooper while-loop Structurizer
cl run tests/test_gep_struct.zk    # 7. Struct GEP & SSA PHI Resolution
cl run tests/test_inliner.zk       # 8. Leaf Function Inliner Pass
cl run tests/test_targets.zk       # 9. Hardware Targets: x86_64, ARM64, WASM
cl run tests/test_gpu_riscv_licm.zk# 10. GPU PTX, RISC-V & LICM Pass
cl run src/main.zk                 # 11. Complete End-to-End Architecture Demo
```

---

## 📜 Contributor & Stewardship

- **Contributor**: Mohammad Zaid `<zkalamgir@proton.me>`
- **Copyright Stewardship**: Managed by Mohammad Zaid / cluster under CCFL v2.0 Terms.
