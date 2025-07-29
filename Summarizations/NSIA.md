### Additional Link

[https://arxiv.org/pdf/2503.01162](https://arxiv.org/pdf/2503.01162)

[arxiv.orghttps://arxiv.org/pdf/2503.01162](https://arxiv.org/pdf/2503.01162)

[https://arxiv.org/pdf/2504.19323](https://arxiv.org/pdf/2504.19323)

[arxiv.orghttps://arxiv.org/pdf/2504.19323](https://arxiv.org/pdf/2504.19323)

### Explanations

### Intro

- What?

- Why?

- Advantage

- Disadvantage

- Hardware solutions

DEFINITIONS

- NSAI

- VSA

Neurosymbolic AI(NSAI)= strengths of NNs + symbolic reasoning to create more advanced and intelligent AI systems.

Potential path towardhuman-like fluid intelligenceandAGI, mirroring human cognitive processes that involve both "thinking fast" (intuitive perception) and "thinking slow" (logical reasoning).

Foundational Understanding of Neurosymbolic AI◦Neural Networks: ✅ 1.Identifying patterns, 2.handling perceptual tasks, 3. flexible and scalable.                                                                                      ❌ transparency, black-box.◦Symbolic AI:          ✅ 1. Excels in reasoning, interpretability. 2. Less training data.                                                                                                                   ❌ Struggle with learning from raw data.

◦Neural Networks: ✅ 1.Identifying patterns, 2.handling perceptual tasks, 3. flexible and scalable.                                                                                      ❌ transparency, black-box.

◦Symbolic AI:          ✅ 1. Excels in reasoning, interpretability. 2. Less training data.                                                                                                                   ❌ Struggle with learning from raw data.

Neurosymbolic AI bridges this gap, synergistically integrating these two approaches to achieve a more comprehensive cognitive ability.◦Enhanced Transparency, Interpretability, and Trustworthiness.◦Superior Cognitive Capabilities:Google DeepMind’s AlphaGeometry, solves geometry problems at the level of human Olympiad gold medalists, where GPT-4 completely fails.IBM’s neuro-vector-symbolic system achieved98.8% accuracyon spatial-temporal reasoning tasks, significantly surpassing human (84.4%), ResNet (53.4%), and GPT-4 (89.0%).◦Higher Data Efficiency: making them promising for edge deployments.◦Generalizability and Robustness:

◦Enhanced Transparency, Interpretability, and Trustworthiness.

◦Superior Cognitive Capabilities:Google DeepMind’s AlphaGeometry, solves geometry problems at the level of human Olympiad gold medalists, where GPT-4 completely fails.IBM’s neuro-vector-symbolic system achieved98.8% accuracyon spatial-temporal reasoning tasks, significantly surpassing human (84.4%), ResNet (53.4%), and GPT-4 (89.0%).

Google DeepMind’s AlphaGeometry, solves geometry problems at the level of human Olympiad gold medalists, where GPT-4 completely fails.

IBM’s neuro-vector-symbolic system achieved98.8% accuracyon spatial-temporal reasoning tasks, significantly surpassing human (84.4%), ResNet (53.4%), and GPT-4 (89.0%).

◦Higher Data Efficiency: making them promising for edge deployments.

◦Generalizability and Robustness:

### Algorithmic Flow

1. Typically, aneural modulehandles perception tasks by interpreting sensory data and generating meaningful scene and object representations (e.g., visual/language representation, pattern recognition).

1. These extracted features are then fed into asymbolic systemfor reasoning tasks, applying logical rules and knowledge. This mirrors the human sense-reason-act cognitive cycle.

1. Vector-Symbolic Architecture (VSA) is the Key Symbolic Operations:◦Turns symbolic info into vectorwhich enables the combination of symbolic reasoning with NNs◦Core VSA operation =circular convolution, combines two vectors to represent composite symbols while preserving information from both.◦Symbolic knowledge is often stored in aknowledge codebook, which integrates learned knowledge and symbolic rules. These codebooks can be large (tens to hundreds of MB),making them challenging to cache on-chip in edge accelerators.

◦Turns symbolic info into vectorwhich enables the combination of symbolic reasoning with NNs

◦Core VSA operation =circular convolution, combines two vectors to represent composite symbols while preserving information from both.

◦Symbolic knowledge is often stored in aknowledge codebook, which integrates learned knowledge and symbolic rules. These codebooks can be large (tens to hundreds of MB),making them challenging to cache on-chip in edge accelerators.

### Challenges for Current Hardware

1. Memory: VSA-based systems often generatelarge intermediate codebooks and rely on vectoroperations, leading to substantial memory footprints that are impractical foron-chip caching in edge devices.

1. GreaterCompute Heterogeneity: involve a diverse mix of neural operations (likeGEMMs, and convolutions) and symbolic operations (like circular convolution,element-wise vectoroperations). →💁🏽Proudful Moment: iMatch perfectly suggests the best approximate computational block to optimize these computations!!

1. ParallelismChallenge: Symbolic operations=irregular dataflows, data dependencies, and sequential processing≠parallelism and increases critical path latency.EXP: symbolic depends on the output of neural modules

1. Lack ofReal-timePerformance: A neuro-vector-symbolic system can take >3 minutes for a single task even on a TPU and desktop GPU.

### Architectural and Hardware Solutions

These challenges are address through algorithm-hardware co-design frameworksCogSysandNSFlow

1. CogSysAchieve real-time efficiency and scalability, through 3 layers:Algorithm Level:Factorizes vectors in an interactive manner : Turn vectors (O(d²) to vector (O(d)Applying additive Gaussian noise during factorization helps escape limit cyclesQuantizationHardware Level:Reconfigurable Neuro/Symbolic PE(nsPEs)instead of sepearated PE.Each nsPE supports three modes (load, GEMM, and circular convolution) and contains four registers for efficient operation.Bubble Streaming (BS) Dataflow:This novel dataflow is designed for efficient circular convolution reduce TPU-systolic form O(d²)  memory footprint to O(d) and It also enables column-wise parallelism.→🟡Check the circular convolution for iMatchAdaptive Spatial-Temporal (ST) MappingTo handlevarying dimensions of vector-symbolicoperations.Adaptive choicebetween spatial mapping (parallelizing a single convolution into folds, good for large vector dimensions) and temporal mapping (parallelizing multiple convolutions, good for smaller vector dimensions) to balance bandwidth and latency.Scalable Array Architecture:scale-up + scale-out strategies =                                                                                                                📈 design utilization and scalability.                                                                                                         🎗️ systolic cell-wise parallelism (ScWP) & column-wise                                                                           parallelism (CWP) for circular convolutions.Custom SIMD Units:Accelerate vector reductions and element-wise operations and 📉 data transfer.System LevelAdaptive Workload-Aware SchedulerThe scheduling is performed offline to ensure optimal or near-optimal scheduling with zero runtime latency.

- Achieve real-time efficiency and scalability, through 3 layers:Algorithm Level:Factorizes vectors in an interactive manner : Turn vectors (O(d²) to vector (O(d)Applying additive Gaussian noise during factorization helps escape limit cyclesQuantizationHardware Level:Reconfigurable Neuro/Symbolic PE(nsPEs)instead of sepearated PE.Each nsPE supports three modes (load, GEMM, and circular convolution) and contains four registers for efficient operation.Bubble Streaming (BS) Dataflow:This novel dataflow is designed for efficient circular convolution reduce TPU-systolic form O(d²)  memory footprint to O(d) and It also enables column-wise parallelism.→🟡Check the circular convolution for iMatchAdaptive Spatial-Temporal (ST) MappingTo handlevarying dimensions of vector-symbolicoperations.Adaptive choicebetween spatial mapping (parallelizing a single convolution into folds, good for large vector dimensions) and temporal mapping (parallelizing multiple convolutions, good for smaller vector dimensions) to balance bandwidth and latency.Scalable Array Architecture:scale-up + scale-out strategies =                                                                                                                📈 design utilization and scalability.                                                                                                         🎗️ systolic cell-wise parallelism (ScWP) & column-wise                                                                           parallelism (CWP) for circular convolutions.Custom SIMD Units:Accelerate vector reductions and element-wise operations and 📉 data transfer.System LevelAdaptive Workload-Aware SchedulerThe scheduling is performed offline to ensure optimal or near-optimal scheduling with zero runtime latency.

### Achieve real-time efficiency and scalability, through 3 layers:

1. Algorithm Level:Factorizes vectors in an interactive manner : Turn vectors (O(d²) to vector (O(d)Applying additive Gaussian noise during factorization helps escape limit cyclesQuantization

1. Factorizes vectors in an interactive manner : Turn vectors (O(d²) to vector (O(d)

1. Applying additive Gaussian noise during factorization helps escape limit cycles

1. Quantization

1. Hardware Level:Reconfigurable Neuro/Symbolic PE(nsPEs)instead of sepearated PE.Each nsPE supports three modes (load, GEMM, and circular convolution) and contains four registers for efficient operation.Bubble Streaming (BS) Dataflow:This novel dataflow is designed for efficient circular convolution reduce TPU-systolic form O(d²)  memory footprint to O(d) and It also enables column-wise parallelism.→🟡Check the circular convolution for iMatchAdaptive Spatial-Temporal (ST) MappingTo handlevarying dimensions of vector-symbolicoperations.Adaptive choicebetween spatial mapping (parallelizing a single convolution into folds, good for large vector dimensions) and temporal mapping (parallelizing multiple convolutions, good for smaller vector dimensions) to balance bandwidth and latency.Scalable Array Architecture:scale-up + scale-out strategies =                                                                                                                📈 design utilization and scalability.                                                                                                         🎗️ systolic cell-wise parallelism (ScWP) & column-wise                                                                           parallelism (CWP) for circular convolutions.Custom SIMD Units:Accelerate vector reductions and element-wise operations and 📉 data transfer.

1. Reconfigurable Neuro/Symbolic PE(nsPEs)instead of sepearated PE.Each nsPE supports three modes (load, GEMM, and circular convolution) and contains four registers for efficient operation.

instead of sepearated PE.Each nsPE supports three modes (load, GEMM, and circular convolution) and contains four registers for efficient operation.

1. Bubble Streaming (BS) Dataflow:This novel dataflow is designed for efficient circular convolution reduce TPU-systolic form O(d²)  memory footprint to O(d) and It also enables column-wise parallelism.→🟡Check the circular convolution for iMatch

This novel dataflow is designed for efficient circular convolution reduce TPU-systolic form O(d²)  memory footprint to O(d) and It also enables column-wise parallelism.→🟡Check the circular convolution for iMatch

1. Adaptive Spatial-Temporal (ST) MappingTo handlevarying dimensions of vector-symbolicoperations.Adaptive choicebetween spatial mapping (parallelizing a single convolution into folds, good for large vector dimensions) and temporal mapping (parallelizing multiple convolutions, good for smaller vector dimensions) to balance bandwidth and latency.

To handlevarying dimensions of vector-symbolicoperations.Adaptive choicebetween spatial mapping (parallelizing a single convolution into folds, good for large vector dimensions) and temporal mapping (parallelizing multiple convolutions, good for smaller vector dimensions) to balance bandwidth and latency.

1. Scalable Array Architecture:scale-up + scale-out strategies =                                                                                                                📈 design utilization and scalability.                                                                                                         🎗️ systolic cell-wise parallelism (ScWP) & column-wise                                                                           parallelism (CWP) for circular convolutions.

scale-up + scale-out strategies =                                                                                                                📈 design utilization and scalability.                                                                                                         🎗️ systolic cell-wise parallelism (ScWP) & column-wise                                                                           parallelism (CWP) for circular convolutions.

1. Custom SIMD Units:Accelerate vector reductions and element-wise operations and 📉 data transfer.

Accelerate vector reductions and element-wise operations and 📉 data transfer.

1. System LevelAdaptive Workload-Aware SchedulerThe scheduling is performed offline to ensure optimal or near-optimal scheduling with zero runtime latency.

1. Adaptive Workload-Aware SchedulerThe scheduling is performed offline to ensure optimal or near-optimal scheduling with zero runtime latency.

The scheduling is performed offline to ensure optimal or near-optimal scheduling with zero runtime latency.

1. NSFlowFPGA-based acceleration framework, first automated end-to-end solution for generic NSAI.Frontend :Design Architecture Generator (DAG)Extracts an execution trace from user-provided workloads →  b.  Generates adataflow graph        →  c.  Performs a two-phase design space co-exploration strategyBackend:Flexible Hardware Architecturepre-defined accelerator template instantiated based on DAG-generated configurationsInspired by CogSys and its nsPE, NS-adaptive Systolic Array (AdArray) and utilizes a "passing register" in each PE to enable the specific streaming for circular convolution.Adaptive Mixed Precision Computation. 🎗️ FP16/8 to INT8/4Custom SIMD Unit,  element-wise operations with compact logic circuits, allowing fluid data transfer and multi-level quantization.→ potential for other approximate techniques

- FPGA-based acceleration framework, first automated end-to-end solution for generic NSAI.Frontend :Design Architecture Generator (DAG)Extracts an execution trace from user-provided workloads →  b.  Generates adataflow graph        →  c.  Performs a two-phase design space co-exploration strategyBackend:Flexible Hardware Architecturepre-defined accelerator template instantiated based on DAG-generated configurationsInspired by CogSys and its nsPE, NS-adaptive Systolic Array (AdArray) and utilizes a "passing register" in each PE to enable the specific streaming for circular convolution.Adaptive Mixed Precision Computation. 🎗️ FP16/8 to INT8/4Custom SIMD Unit,  element-wise operations with compact logic circuits, allowing fluid data transfer and multi-level quantization.→ potential for other approximate techniques

### FPGA-based acceleration framework, first automated end-to-end solution for generic NSAI.

1. Frontend :Design Architecture Generator (DAG)Extracts an execution trace from user-provided workloads →  b.  Generates adataflow graph        →  c.  Performs a two-phase design space co-exploration strategy

1. Extracts an execution trace from user-provided workloads →  b.  Generates adataflow graph        →  c.  Performs a two-phase design space co-exploration strategy

1. Backend:Flexible Hardware Architecturepre-defined accelerator template instantiated based on DAG-generated configurationsInspired by CogSys and its nsPE, NS-adaptive Systolic Array (AdArray) and utilizes a "passing register" in each PE to enable the specific streaming for circular convolution.Adaptive Mixed Precision Computation. 🎗️ FP16/8 to INT8/4Custom SIMD Unit,  element-wise operations with compact logic circuits, allowing fluid data transfer and multi-level quantization.→ potential for other approximate techniques

1. pre-defined accelerator template instantiated based on DAG-generated configurations

1. Inspired by CogSys and its nsPE, NS-adaptive Systolic Array (AdArray) and utilizes a "passing register" in each PE to enable the specific streaming for circular convolution.

1. Adaptive Mixed Precision Computation. 🎗️ FP16/8 to INT8/4

1. Custom SIMD Unit,  element-wise operations with compact logic circuits, allowing fluid data transfer and multi-level quantization.→ potential for other approximate techniques
