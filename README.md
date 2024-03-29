# Catalogue of Performance Optimization Mechanisms

### Description

This repo is a systematized live catalogue of performance optimization mechanisms implemented on various levels of computer architecture.

Systematization is based on observation that it is possible to formulate generic optimization approaches that are agnostic to:
* HW/SW implementation (hardware- or software-only, mixed manner),
* nature of management engine (processor microarchitecture, OS kernel, software compiler, hardware synthesizer/generator, etc.),
* type of computational traffic elements (processing, communicational, memory operations),
* processed data (data bytes, network packets, graphic assets, etc.),
* stage of the system life cycle (both statically and dynamically),
* degree of automation (manually, fully automatically, and everything in between).

These approaches designate useful "computational effects" addressed by various optimization mechanisms. Also, they provide potential directions for generation of new mechanisms that improve density, regularity, scalability of computations, disposal of locks, congestions and other inefficiencies. Knowledge of these generic approaches can assist in both making computational artifacts "implementation-friendly" in general and adapting them to specific physical and/or platform capabilities and constraints. (Micro)Architectures are understood mostly as practical compositions of these mechanisms.

These approaches have been formulated as **Strategies of Computational Process Synthesis (SCPS)**. Preliminary version of the catalogue was published in previous works [1, 2].

![pic_test](img/strategies_en.png)

SCPS formulations:

* **relaxation** – reduction of coupling/interlocks between requests. Contains four subcategories:
	* **overlapping** – decoupling of initiation of new request processing with completion of previous requests;
	* **distribution** – partitioning of workload in loosely dependent parts enabling concurrent execution;
	* **reordering** – relaxation of ordering constraints, enabling forwarded/deferred execution;
	* **speculation** – performing (possibly redundant) computations in advance in the interest of latency reduction;

* **compression** – reduction of workload processing cost. Contains two subcategories:
	* **coalescing** – increasing granularity of workload elements to decrease management overhead;
	* **elimination** – detection and removal of redundant computations;

* **variation** – handling variability of workload elements. Contains three subcategories:
	* **resorting** – re-grouping workload elements in generic or dedicated categories based on various properties (spatial, parametric, functional) that affect their execution;
	* **reconfiguration** – introduction of changeability of system parameters and internal mechanisms, allocation of generic “hard” substrate for diverse “soft” workload elements;
	* **virtualization** – allocation of new management overlays that decouple selected mechanisms for their interoperable application in various scenarios.

Examples of performance optimization mechanisms grouped in SCPS categories:

Classic computer architecture levels | Relaxation (overlapping)
---------------------------- | ------------------------
Generic | Asynchronous processing, shadow/ping-pong/double buffering, data/task queuing
Web | Asynchronous web services, event loop (non-blocking I/O)
Graphics | Rendering pipeline
DBMS | Concurrency control protocols, data streams processing
System software (OS, VMs, drivers) | OS pipes, OS multitasking, spooling, asynchronous I/O
System software (compilers and runtimes) | Software pipelining, software register renaming, stall reduction, lock-free data structures and programming, asynchronous programming environments
Processor architecture | Software data hazard resolution, rotating register files, delay slots, lock-free synchronization instructions
Hardware microarchitecture (processing) | Instruction pipelining
Hardware microarchitecture (communication) | Packet switching, split transaction protocols, sliding window flow control, wormhole switching/routing
Hardware microarchitecture (memory) | Memory pipelining, hardware register renaming, non-blocking caches
Digital circuitry | Synchronous pipelines, wave pipelines

Classic computer architecture levels | Relaxation (distribution)
---------------------------- | -------------------------
Generic | Data partitioning, subtasks allocation
Web | Parallel HTTP requests, HTTP chunking, code splitting, segmented file transfer, microservices decoupling, multi-server setups, MapReduce model, content delivery networks
Graphics | Space partitioning, mesh decomposition
DBMS | Database partitioning, replication/sharding
System software (OS, VMs, drivers) | OS multithreading
System software (compilers and runtimes) | Parallel programming environments, work sharing/stealing, coroutines, static parallelization, loop fission, free heap blocks splitting
Processor architecture | Decoupled access/execute, multi/many-core architectures, simultaneous multithreading, asynchronous offload engines, multi-channel DMA
Hardware microarchitecture (processing) | Vector lanes, superscalar processing of instructions
Hardware microarchitecture (communication) | Parallel links, concurrent slaves arbitration, dense topologies, distributed NoC routing
Hardware microarchitecture (memory) | Multiporting, multibank partitioning, multi-way set-associative caches, coherent caches
Digital circuitry | Asynchronous clock domains (GALS), logic replication, parallel prefix addition, application mapping on multiple hardware resources in HLS

Classic computer architecture levels | Relaxation (reordering)
---------------------------- | -----------------------
Generic | Lazy object initialization
Web | Lazy connections/loading, eager/lazy JS parsing
Graphics | Mesh vertices reordering, out-of-order rasterization, forwarded/deferred rendering
DBMS | Prioritized resource scheduling, query reordering
System software (OS, VMs, drivers) | Thread priority scheduling, I/O requests sorting
System software (compilers and runtimes) | Lazy evaluation, code motion, frequent branch prioritization, loop blocking (tiling), loop interchange
Processor architecture | Dataflow architectures, relaxed memory models
Hardware microarchitecture (processing) | Out-of-order execution of instructions, scoreboarding/Tomasulo scheduling algorithm
Hardware microarchitecture (communication) | Out-of-order completion of transfers
Hardware microarchitecture (memory) | Deferred store buffers
Digital circuitry | Retiming, slack borrowing, time stealing, permutable cell terminals interchange, multiplier partial products rearranging, operations reordering in HLS

Classic computer architecture levels | Relaxation (speculation)
---------------------------- | ------------------------
Generic | Data caching and prediction, speculative resource allocation, optimistic concurrency control, text auto-completion
Web | Link prefetching, preloading, prebrowsing, web/network/HTTP caching
Graphics | Texture caching, shader caches (precompiled shaders)
DBMS | Speculative query execution
System software (OS, VMs, drivers) | Storage data prefetching
System software (compilers and runtimes) | (Un)likely attributes, software transactional memory, thread-level speculation
Processor architecture | Branch prediction hints, cache hints, CAS instructions, hardware transactional memory instructions
Hardware microarchitecture (processing) | Branch prediction heuristics, multipath execution, return address stack, memory requests prediction, register/memory value prediction, computational caches
Hardware microarchitecture (communication) | NACK-able transmissions, speculative propagation and stomping
Hardware microarchitecture (memory) | Prefetching heristics, stream buffers, caching heuristics
Digital circuitry | Multiplexing pre-computed data

Classic computer architecture levels | Compression (coalescing)
---------------------------- | ------------------------
Generic | Data/task bundling, data buffering
Web | Web resource bundling, HTTP requests merging, media content buffering
Graphics | GPU thread coarsening, sparse textures
DBMS | Data clustering
System software (OS, VMs, drivers) | Increased OS scheduling time quantum, I/O requests coalescing, batch processing, slab allocation, scatter/gather I/O, file defragmentation, file archiving, VM proximity placement groups
System software (compilers and runtimes) | Instruction combining, loop unrolling, loop fusion, free heap blocks coalescing
Processor architecture | FMA instructions, SIMD, VLIW, CGRA architectures, interrupt coalescing, huge pages, CPU clustering
Hardware microarchitecture (processing) | Instruction fusion
Hardware microarchitecture (communication) | Enlarged packets (e.g. jumbo frames), burst transfers
Hardware microarchitecture (memory) | Memory accesses coalescing, write combining
Digital circuitry | Wide functional units, large FPGA LUTs, operation clustering (chaining) in HLS

Classic computer architecture levels | Compression (elimination)
---------------------------- | -------------------------
Generic | Data compression, data reduction, data indexing, data deduplication, acceleration structures, object pooling, source code minification
Web | HTTP compression, web media compression, tree shaking, partial page update
Graphics | Partial redraw, texture compression, tiled rendering, view frustum culling, occlusion culling, polygon clipping, game world sectorization, levels of detail, decreased distant animation update rate
DBMS | (De)normalization, recycling of intermediate results
System software (OS, VMs, drivers) | Context switch minimization, zero-copy data transfers, memory balooning, memory overlays, page combining, file compression
System software (compilers and runtimes) | Constant folding/propagation, floating- to fixed-point conversion, register recycling/reuse, register promotion, structure packing, dead code elimination, common subexpression elimination, strength reduction, branchless programming (branch elimination), branch tables, loop-invariant code motion, loop splitting, computation reuse, memoization, precompiled headers, deforestation, heap blocks reuse, garbage collection, neural network pruning/quantization
Processor architecture | Predicated instructions, compressed (with increased code density) ISA
Hardware microarchitecture (processing) | Loop stream detection, dynamic instruction reuse, interrupt tail-chaining
Hardware microarchitecture (communication) | Sparse NoC topologies, NoC traffic compression
Hardware microarchitecture (memory) | Hardware data compression, reducing processor-memory traffic using caches, caching exclusivity, write-back caching policy
Digital circuitry | Power/clock gating, redundant reset elimination, bitwidth narrowing, register merging, dead/duplicated logic removal, logic minimization, partial FPGA reconfiguration, process uniqueness in discrete-event simulation runnable queue

Classic computer architecture levels | Variation (resorting)
---------------------------- | ---------------------------
Generic | Diverse data structures, traffic types, and algorithms
Web | Internet media types
Graphics | Shader types, variable rate shading
DBMS | Query prioritization, heterogeneous DBMSs
System software (OS, VMs, drivers) | Priority classes, process/thread affinity, QoS scheduling, asymmetric multiprocessing environments
System software (compilers and runtimes) | Instruction replacement, task partitioning for heterogeneous platforms
Processor architecture | ISA extensions, cache partitioning, interrupt priority levels, general-purpose/domain specific processors, asymmetric multiprocessors
Hardware microarchitecture (processing) | Variably optimized (e.g. for performance/power) processor microarchitectures
Hardware microarchitecture (communication) | Topology variability, heterogeneous networks, QoS traffic classes
Hardware microarchitecture (memory) | Memory hierarchy, NUMA
Digital circuitry | High performance and low power process technologies, variably optimized (e.g. for speed/leakage) standard cells, clock/data networks, generic LUTs and hard macro blocks in FPGA, pipeline balancing, voltage-frequency island partitioning

Classic computer architecture levels | Variation (reconfiguration)
---------------------------- | ---------------------------
Generic | Platform programmability/reconfigurability, performance tuning options, floating-point types 
Web | Microservices continuous delivery
Graphics | Shader programmability
DBMS | SQL performance tuning
System software (OS, VMs, drivers) | Process priorities reconfiguration, microkernel architecture, disk cache modes
System software (compilers and runtimes) | Compiler optimization flags, neural network learning
Processor architecture | Processors’ programmability, switchable ISAs, modes of execution, customizable memory models
Hardware microarchitecture (processing) | Branch predictor adaptation, microprogrammable processors, FPGAs, conservation cores
Hardware microarchitecture (communication) | Adaptive routing, reconfigurable QoS, reconfigurable NoC topology, software-defined networking
Hardware microarchitecture (memory) | Cache mapping adaptation
Digital circuitry | DVFS, FPGA reconfigurability, reconfigurable macro blocks, back-annotated synthesis, synthesis/implementation constraints

Classic computer architecture levels | Variation (virtualization)
---------------------------- | --------------------------
Generic | Multi-layer system architecture
Web | OSI multi-layer model, language embedding in HTML, WebAssembly, cloud services
Graphics | Standardized graphics APIs, unified shader model
DBMS | Database virtualization, common query languages
System software (OS, VMs, drivers) | OS containers, platform emulation
System software (compilers and runtimes) | Managed programming environments, multi-stage compilation
Processor architecture | CPU ISA/microarchitecture separation, virtual forwarding/routing, virtual memory, FPGA temporal partitioning, logical processors, hardware CPU virtualization
Hardware microarchitecture (processing) | Dynamic binary translation, composed multicores, dynamic synthesis of thread accelerators ("thread warping")
Hardware microarchitecture (communication) | Virtual channels, multi-layer protocols, link auto-training, cognitive radio
Hardware microarchitecture (memory) | Hardware cache hierarchy management
Digital circuitry | Logic simulation, programmable logic, hardware emulation

### Publications

* A. Antonov, “Methods and Tools for Computer-Aided Synthesis of Processors Based on Microarchitectural Programmable Hardware Generators,” Ph.D dissertation, ITMO University, Saint-Petersburg, 28.12.2018. URL: http://fppo.ifmo.ru/dissertation/?number=63419

* A. Antonov, P. Kustarev, “Strategies of Computational Process Synthesis – a System-Level Model of HW/SW (Micro)Architectural Mechanisms,” in 2020 9th Mediterranean Conference on Embedded Computing (MECO), 2020. URL: https://ieeexplore.ieee.org/document/9134071
