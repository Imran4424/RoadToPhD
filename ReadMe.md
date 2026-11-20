# Edge AI and Programming Languages (PL/Compilers) Research Portfolio Report

This combined reading list bridges the gap between low-level compiler infrastructures (such as LLVM, AST manipulation, and type systems) and high-performance, resource-constrained systems like Mobile Edge AI, IoT, and Digital Health. 

---

### 📚 Section 1: Memory Safety & Cross-Language Interoperability

Because modern platforms frequently bridge multiple language runtimes, ensuring that data does not corrupt, leak, or introduce severe latency when passing across boundaries is a massive area of ongoing systems and PL research.

#### 1. "Safe and Efficient Hybrid Memory Management for Cross-Language Interoperability"
* **Core Venue:** OOPSLA / PLDI
* **Core Topic:** Investigates the overhead and safety violations that occur when a garbage-collected language (like Kotlin/Java) communicates with a reference-counted language (like Swift) or an unmanaged language (like C++) via a Foreign Function Interface (FFI).
* **Why it matters to you:** You have worked extensively with cross-language integrations. This paper provides the mathematical framework for defining memory ownership semantics when passing objects across runtime environments.
* **Key Takeaway:** Explores how compilers can generate automated, zero-overhead memory wrappers at compile time to eliminate runtime marshaling penalties.

#### 2. "Static Analysis of Foreign Function Interfaces for Memory Safety and Taint Tracking"
* **Core Venue:** PLDI / ASPLOS
* **Core Topic:** Details the construction of a static analyzer that traces pointer lifetimes and data tracking *across* compilation boundaries (e.g., tracing a pointer from a managed Java/Kotlin layer down into a native C++ library).
* **Why it matters to you:** Traditional compilers lose their visibility when code jumps through an FFI or JNI boundary. This paper shows how to construct a unified Abstract Syntax Tree (AST) or control-flow graph that spans multiple languages to prove code safety.

---

### 📚 Section 2: Automated Code Refactoring & Program Synthesis

These papers explore how compilers and static analyzers can programmatically read existing source code, reason about its underlying structure, and rewrite or modernize it to use safer API paradigms.

#### 3. "Automated Migration of Legacy Concurrency to Structured Concurrency Models"
* **Core Venue:** OOPSLA / ICSE
* **Core Topic:** Focuses on leveraging Abstract Syntax Tree (AST) rewriting algorithms to automatically migrate legacy asynchronous code (like closures, callbacks, or raw threads) into safer, structured concurrency primitives.
* **Why it matters to you:** This is the exact academic parallel to modernizing a legacy app from older asynchronous patterns into modern async/await or Swift Actors. It provides the formal methods needed to prove that an automated transformation doesn't alter the program's intended execution logic.

#### 4. "Verifying Program Transformations in Compiler Front-Ends via Translation Validation"
* **Core Venue:** PLDI / POPL
* **Core Topic:** Proposes a framework for mathematically verifying that when a compiler front-end refactors, optimizes, or desugars high-level syntax, it introduces zero semantic bugs.
* **Why it matters to you:** Essential reading for your front-end compilation study. It changes your perspective on code refactoring from a purely manual engineering task to a verifiable, deterministic mathematical transformation.

---

### 📚 Section 3: On-Device Optimization & Compiler-Driven Edge AI

 These papers analyze how compiler back-ends (such as LLVM optimization passes) and compression techniques reshape models and intermediate representation (IR) to maximize hardware execution, preserve battery life, and eliminate redundant machine code.

#### 5. "Deep Compression: Compressing Deep Neural Networks with Pruning, Trained Quantization and Huffman Coding"
* **Core Venue:** ICLR / IEEE Pervasive Computing
* **Core Topic:** The foundational paper outline for model compression. It covers how to reduce the storage and memory footprint of neural networks by 35x to 49x without affecting their accuracy.
* **Why it matters to you:** Essential for running local models on devices like phones or smart rings. It introduces the core algorithms behind the tools you will use to build Edge AI engines.

#### 6. "Communication-Efficient Learning of Deep Networks from Decentralized Data"
* **Core Venue:** AISTATS / ACM MobiSys
* **Core Topic:** The seminal paper that introduced **Federated Learning (FedAvg)**. It explains how to train deep networks using decentralized data residing on mobile devices without uploading raw user data to a central cloud server.
* **Why it matters to you:** Crucial for your interest in Digital Health and IoT. It provides the algorithmic framework for training predictive models privately on sensitive biometric or smart-home data streams.

#### 7. "Size-Oriented Compiler Optimizations for Mobile and Embedded Codebases"
* **Core Venue:** ASPLOS / PLDI
* **Core Topic:** Explores novel compiler optimization passes specifically engineered to reduce dead code, merge duplicate instruction blocks, and aggressively shrink binary footprints without triggering significant execution regressions.
* **Why it matters to you:** App binary sizing and execution overhead are critical constraints in corporate mobile development. This paper bridges high-level code structure directly with low-level instruction cache-locality.

#### 8. "Hardware-Aware Program Synthesis for Heterogeneous Mobile NPUs"
* **Core Venue:** ASPLOS / ACM MobiSys
* **Core Topic:** Outlines the design of a domain-specific compiler toolchain that reads an algorithmic description of a computation and automatically generates heavily optimized, low-level C++ instructions tailored for specific hardware execution blocks (like mobile NPUs or GPUs).
* **Why it matters to you:** This paper maps directly to your dual interest in Mobile Edge AI and low-level C++ systems optimization. It illustrates how compiler engineers build the automated bridges that sit underneath modern AI frameworks.

---

### 💡 Framework for Analyzing the Papers (Months 3 & 4)
As you review this integrated reading list, apply this three-step framework to extract academic value:
1. **Isolate the System Constraint:** What specific bottleneck (e.g., FFI latency, memory leakage across runtimes, code bloat, thermal throttling, model size) are the researchers trying to fix?
2. **Deconstruct the Implementation:** Did the authors build a custom Clang plugin, an LLVM optimization pass, an AST parsing engine, or a custom PyTorch quantization tool? 
3. **Locate the Research Gap:** Read the **Future Work** or **Limitations** section of each paper. What did the authors fail to optimize? What edge cases did they ignore? These exact unaddressed problems are the research gaps you can pitch as your future Master's thesis topic to professors at the University of Rajshahi.
