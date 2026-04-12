# Advanced Techniques: LoRA, RAG, and Emergent Behaviours

### *EmergentEvolution — Document 2 of the Foundational Series*

---

> *The previous document established what AI is at the foundational level — what machine learning is, how neural networks work, what large language models are, and how they become commercial products. This document goes deeper into the techniques that are actively pushing AI systems beyond the static, closed-form model — the techniques that make the AGI boundary question harder to answer, and the philosophical questions more urgent. Read the Introduction first.*

---

## Table of Contents

1. [Beyond the Static Model](#beyond-static)
2. [Fine-Tuning: Teaching a Trained Model New Tricks](#fine-tuning)
3. [LoRA: Parameter Efficiency and Bounded Self-Modification](#lora)
   - 3.1 [The Problem LoRA Solves](#lora-problem)
   - 3.2 [How LoRA Works](#lora-how)
   - 3.3 [What LoRA Means Architecturally](#lora-architectural)
   - 3.4 [The Philosophical Implications](#lora-philosophical)
4. [RAG: Externalised, Persistent Memory](#rag)
   - 4.1 [The Memory Problem in Language Models](#memory-problem)
   - 4.2 [How RAG Works](#rag-how)
   - 4.3 [What RAG Actually Provides](#rag-provides)
   - 4.4 [The Limits of RAG as Memory](#rag-limits)
5. [LoRA + RAG: What the Combination Produces](#lora-rag-combined)
6. [Agentic AI: Tool Use, Environment Coupling, and Feedback Loops](#agentic)
   - 6.1 [What Tool Use Is](#tool-use)
   - 6.2 [Agentic Architectures](#agentic-architectures)
   - 6.3 [The Closed Loop Problem](#closed-loop)
7. [Continual Learning: The Self-Modifying System](#continual-learning)
   - 7.1 [The Catastrophic Forgetting Problem](#catastrophic-forgetting)
   - 7.2 [Current Approaches to Continual Learning](#continual-approaches)
   - 7.3 [What Genuine Continual Learning Would Mean](#continual-genuine)
8. [Emergent Behaviours: What They Are and Are Not](#emergence)
   - 8.1 [Defining Emergence Precisely](#emergence-definition)
   - 8.2 [Documented Emergent Behaviours in LLMs](#emergence-documented)
   - 8.3 [Why Emergence Is Contested](#emergence-contested)
   - 8.4 [Phase Transitions and Capability Jumps](#phase-transitions)
   - 8.5 [The Philosophical Weight of Emergence](#emergence-philosophical)
9. [In-Context Learning: The Other Kind of Adaptation](#in-context)
10. [Mixture of Experts: Conditional Computation](#moe)
11. [Chain-of-Thought and Extended Reasoning](#chain-of-thought)
12. [What These Techniques, Combined, Produce](#combined)
13. [The Architectural Horizon: Where This Is Going](#horizon)

---

## 1. Beyond the Static Model {#beyond-static}

The foundational model described in the Introduction — a Transformer trained on text, deployed with fixed weights — is a powerful but fundamentally closed system. It was trained once, on a fixed dataset, and then deployed. Everything it "knows" is encoded in its weights at training time. It cannot learn from deployment experience. It has no persistent memory across conversations. It cannot update its own parameters. It operates in a single forward pass per response, with no extended deliberation.

This architecture is responsible for the most capable AI systems currently available to the public. But it is also the architecture's limitations that define the gap between current AI and any conception of AGI worth taking seriously.

The techniques described in this document are the active research and engineering frontier — the methods being used to push beyond the closed static model toward systems that are more adaptive, more persistent, and more capable of functioning as ongoing agents rather than one-shot responders.

These techniques matter in two ways. Practically: they determine what AI systems can do in deployment. Philosophically: they change the nature of the questions you can ask about these systems. A system that can update its own parameters, maintain persistent memory, use tools to act in the world, and operate in feedback loops with its environment is a categorically different object of analysis than a static-weights model, even if the underlying architecture is similar.

Understanding these techniques is necessary for understanding why the philosophical debates around AI have become more urgent, and why easy dismissals — "it's just weights," "it can't really learn," "it has no memory" — are becoming less accurate as a description of actually-deployed systems.

---

## 2. Fine-Tuning: Teaching a Trained Model New Tricks {#fine-tuning}

Before examining LoRA specifically, we need to understand fine-tuning in general.

Pre-training — training a large language model from scratch on a massive text corpus — is enormously expensive. GPT-3-scale pre-training was estimated to cost millions of dollars in compute. Current frontier models are estimated to cost tens to hundreds of millions.

Fine-tuning addresses this by taking an already pre-trained model and training it further on a smaller, more targeted dataset. The idea: the pre-trained model has already learned general representations of language, world knowledge, and reasoning patterns. Fine-tuning can adapt those representations to a specific task, domain, or behaviour without relearning everything from scratch.

The benefits: dramatically lower cost than pre-training, faster iteration, and the ability to customise model behaviour without access to the original pre-training infrastructure.

The challenge: fine-tuning can degrade performance on tasks outside the fine-tuning domain (catastrophic forgetting, discussed later), requires careful management of learning rates and data mixing, and can introduce new failure modes if the fine-tuning data is not carefully curated.

Full fine-tuning updates all of the model's parameters. This is expensive at large scales — a model with hundreds of billions of parameters requires enormous memory just to hold all the gradients during training. This is the problem that parameter-efficient fine-tuning methods, including LoRA, were designed to address.

---

## 3. LoRA: Parameter Efficiency and Bounded Self-Modification {#lora}

### 3.1 The Problem LoRA Solves {#lora-problem}

Full fine-tuning of a large model is expensive in two ways: memory (you need to store all the weight updates, not just the weights themselves) and compute (gradients must be computed for every parameter).

For a 70-billion parameter model, full fine-tuning requires hardware that is simply inaccessible to most researchers and practitioners, even with large budgets. And even where hardware is available, full fine-tuning often produces poor results on small fine-tuning datasets — the model has too many degrees of freedom to be reliably shaped by limited data.

The hypothesis behind parameter-efficient fine-tuning: the changes that fine-tuning needs to make to a pre-trained model are low-dimensional. The task-specific adaptation does not require modifying the entire weight space — it requires moving in a relatively small subspace of that space. If this is true, we should be able to represent the needed changes efficiently, without updating every parameter.

### 3.2 How LoRA Works {#lora-how}

LoRA (Low-Rank Adaptation) was introduced by Hu et al. in 2021. The key insight: weight changes during fine-tuning tend to lie in a low-rank subspace.

Formally: a weight matrix W in a Transformer has some shape (d × k). A full update to this matrix is another (d × k) matrix — expensive to store and compute. LoRA approximates this update as the product of two smaller matrices: an (d × r) matrix A and an (r × k) matrix B, where r << d,k. The rank r controls the expressiveness of the update — small r means the update is tightly constrained; larger r allows more complex changes.

During fine-tuning, the original weights W are frozen — not updated at all. Only the LoRA matrices A and B are trained. The effective weight matrix is W + AB (scaled by a factor). At inference, the LoRA matrices can either be merged back into W (so there is no runtime overhead) or kept separate (so the base model can be swapped without retraining LoRA).

The reduction in trainable parameters is dramatic. For large Transformer models, LoRA can reduce the number of trainable parameters by one to four orders of magnitude — from billions to millions — while maintaining most of the fine-tuning performance.

### 3.3 What LoRA Means Architecturally {#lora-architectural}

LoRA's architectural implications go beyond efficiency. They change what is possible in deployment.

Because LoRA weights are small, they are:

**Modular** — multiple LoRA adapters can be applied to the same base model, potentially switched between. A single base model can have many associated LoRA adapters for different tasks, personas, or domains, and these can be selected or blended at inference time.

**Composable** — in principle, multiple LoRA adapters can be combined by summing their rank-decomposed updates, allowing capabilities from different fine-tunes to be mixed.

**Fast to train** — a LoRA fine-tune of a large model can run in hours on consumer hardware, enabling rapid iteration and personalisation at a scale that full fine-tuning cannot support.

**Locally deployable** — because LoRA adapters are small, a user running a local model can maintain multiple adapters and switch between them without large infrastructure.

The ecosystem of open-weight models (Llama series, Mistral, etc.) plus freely trained LoRA adapters has produced a large community of practitioners doing fine-tuning at every level of technical sophistication. This democratisation of fine-tuning has accelerated the pace of exploration well beyond what centralised labs could achieve alone.

### 3.4 The Philosophical Implications {#lora-philosophical}

LoRA matters philosophically because it represents a form of bounded parameter plasticity — the model's weights can change based on interaction, within limits set by the rank constraint.

In the context of the AGI debate (developed in the next document), this matters because:

A system with static weights is clearly not adapting. A system with LoRA fine-tuning loops has a mechanism by which its behaviour can be shaped by accumulated experience. The question of how much this resembles biological learning depends on the specifics of the update loop — but the architecture no longer excludes the possibility of something learning-like.

The rank constraint is also interesting: it means LoRA updates cannot make arbitrary changes to the model. They can modify behaviour within a constrained subspace. This is somewhat analogous to constrained plasticity in biological systems — the brain can change, but not arbitrarily; its architecture constrains the direction and extent of learning.

However — and this is important — current LoRA deployments are typically not running continuous update loops during deployment. A fine-tune is performed offline, then deployed as a fixed adapter. The model is still static in deployment; the plasticity happens between deployments, not within them. The distinction between "offline learning" and "online learning" matters significantly for the philosophical question of whether the system is genuinely adaptive.

---

## 4. RAG: Externalised, Persistent Memory {#rag}

### 4.1 The Memory Problem in Language Models {#memory-problem}

A fundamental limitation of the basic LLM architecture is its relationship to memory.

A language model has two forms of "memory" in a loose sense:

**Parametric memory** — information encoded in the weights during training. This is fixed at deployment. The model "knows" that Paris is the capital of France because patterns in the training data were consistent with this fact, and those patterns were encoded in the weights. This memory cannot be updated without retraining.

**Context window memory** — the model attends to everything in its current context: the conversation history, any documents provided, system prompt, tool outputs. This is temporary — it exists only for the current inference and disappears afterward.

Neither of these provides the kind of persistent, queryable, updatable external memory that humans or more sophisticated information systems use. If you want the model to remember something from a previous conversation, you must explicitly include it in the current context. If you want it to access up-to-date information not in its training data, you have no mechanism for this within the basic architecture.

This is a severe limitation for practical deployment. It means models have knowledge cutoffs (they don't know about events after training), they cannot recall prior conversations, and they cannot be updated with new information without expensive retraining.

RAG addresses this.

### 4.2 How RAG Works {#rag-how}

Retrieval-Augmented Generation (RAG) was introduced by Lewis et al. (Facebook AI Research) in 2020 and has become one of the most practically important techniques in deployed AI systems.

The basic architecture:

1. A large collection of documents (or any text data) is pre-processed into chunks and encoded into dense vector representations (embeddings) using an encoder model.

2. These embeddings are stored in a vector database — a data structure optimised for nearest-neighbour search in high-dimensional embedding spaces.

3. When a query arrives, the query is also encoded into an embedding.

4. The vector database is searched for documents whose embeddings are closest (most similar) to the query embedding — these are the most semantically relevant documents.

5. The retrieved documents are inserted into the context window alongside the query.

6. The language model generates a response using both the query and the retrieved context.

The result: the model can access information outside its training data, sourced from a persistent, queryable store that can be updated without retraining the model.

### 4.3 What RAG Actually Provides {#rag-provides}

RAG effectively extends the model's accessible knowledge from the fixed parametric memory in its weights to an arbitrary external knowledge base. This has several important properties:

**Currency** — the knowledge base can be updated continuously. A RAG system can have access to documents published after the model's training cutoff.

**Specificity** — the knowledge base can contain highly domain-specific information that was sparse or absent in general pre-training data.

**Attribution** — because retrieved documents are explicitly provided, the model can cite its sources and users can verify claims.

**Scalability** — the knowledge base can be arbitrarily large. The model does not need to "fit" knowledge into its weights.

**Persistence** — information stored in the vector database persists across conversations. If a user's prior conversation transcripts are stored and indexed, a RAG system can retrieve relevant prior interactions and effectively "remember" them.

The last point is particularly important for the philosophical analysis in this study. RAG can function as a form of episodic memory — a persistent store of past interactions that can be retrieved when relevant. This is not the same as biological episodic memory, but it is functionally analogous in important ways.

### 4.4 The Limits of RAG as Memory {#rag-limits}

RAG is powerful but has important limitations that prevent it from being equivalent to human memory.

**Retrieval is approximate.** The nearest-neighbour search finds documents that are semantically similar to the query, but "semantically similar" is defined by the embedding model — and embedding models have their own failure modes. Important information can be missed if it is embedded differently from the query.

**Retrieval is not automatic.** Unlike human associative memory, RAG retrieval is triggered by a specific query. If the model does not know to query for something, it will not retrieve it. Spontaneous recall — information surfacing without explicit query — is not a native feature of RAG.

**Context injection is not integration.** Inserting retrieved documents into the context window is not the same as the model integrating that information into its weights. The model can use the retrieved information in its current response, but this does not change its parametric memory. The knowledge "lives" in the external store, not in the model.

**Conflicts between parametric and retrieved memory.** When retrieved documents conflict with parametric memory (the model's training-encoded knowledge), the model may not resolve the conflict correctly. Hallucinations can occur where the model blends parametric and retrieved information in incorrect ways.

These limitations mean RAG provides something like working memory or long-term external storage — useful and important, but not equivalent to the deeply integrated, automatically consolidated, continuously updated memory of biological systems.

---

## 5. LoRA + RAG: What the Combination Produces {#lora-rag-combined}

LoRA and RAG address different aspects of the static model problem. Combining them produces a system with properties that neither provides alone.

LoRA provides: parameter plasticity — the model's internal representations can be shaped by experience, within constraints.

RAG provides: persistent external memory — the model can access and add to a store of information that persists across interactions.

Together, they produce a system that can:

- Adapt its internal processing based on accumulated experience (via LoRA updates)
- Access and accumulate persistent external knowledge (via RAG)
- Use that knowledge to inform its generation in ways that are not purely parametric

This combination begins to resemble, in a loose functional sense, the distinction between procedural memory (how to do things — roughly analogous to parametric weights shaped by LoRA) and declarative memory (facts and episodes — roughly analogous to the RAG knowledge store).

The degree to which this resemblance is meaningful depends on how the update loops are configured. An offline LoRA fine-tune + static RAG database is still fundamentally different from biological memory systems. A system with continuous online LoRA updates driven by interaction, combined with a RAG store that is continuously updated with interaction transcripts and tool outputs, is closer to a genuinely adaptive system — though still different in important ways.

The important point for this study: the easy statement "it can't learn, it has no memory" is already not true of deployed systems at the frontier. The question is not whether these systems have some form of learning and memory, but whether the forms they have constitute anything like the learning and memory relevant to questions of intelligence and agency.

---

## 6. Agentic AI: Tool Use, Environment Coupling, and Feedback Loops {#agentic}

### 6.1 What Tool Use Is {#tool-use}

A language model operating purely in a generation loop — input text in, output text out — is informationally isolated from the world. It cannot browse the internet, execute code, query databases, control software, or take actions with external consequences.

Tool use breaks this isolation. A model with tool access can be given the ability to call external functions: search the web, run a Python interpreter, query an API, read and write files, send messages, or control a computer. The model receives the results of these tool calls as additional context and can use them in its response.

Tool use changes the fundamental nature of what the model is doing. Instead of generating a response from static parametric memory plus context, it is executing a sequence of actions, observing their results, and updating its behaviour accordingly. This is not text generation — it is action selection in an environment.

The model is still using text to represent actions (a tool call is a structured text output) and process results (tool outputs are text inputs). But the consequential loop between action and environment fundamentally changes the system's relationship to the world.

### 6.2 Agentic Architectures {#agentic-architectures}

An "agent" in AI is a system that perceives its environment, selects actions, and receives feedback in a loop. Classical reinforcement learning agents operate this way. Modern "agentic" LLM systems implement a similar loop using language model generation as the action selection mechanism.

Common agentic architectures include:

**ReAct (Reasoning + Acting)** — the model interleaves reasoning steps (generating text that thinks through the problem) with action steps (calling tools). Each tool result is incorporated into the context, and the cycle continues until the task is complete or the model decides to respond.

**Plan-and-Execute** — the model first generates a plan (a sequence of steps), then executes the plan step by step, potentially revising when steps fail or produce unexpected results.

**Multi-agent systems** — multiple model instances operating in parallel or in sequence, each handling a subtask, with outputs passed between agents. Coordination can be handled by a separate "orchestrator" model or by structured communication protocols.

**Self-reflective agents** — systems that explicitly generate self-critiques of their outputs and revise before responding, implementing a form of deliberation through multiple generation passes.

These architectures are not purely theoretical — they are deployed in products. Claude's agentic capabilities, AutoGPT, and various commercial "AI agent" platforms all implement variations of these patterns.

### 6.3 The Closed Loop Problem {#closed-loop}

When a language model has tool use and operates in a feedback loop with an environment, the system's behaviour becomes harder to characterise and predict.

In a simple generation case, the model takes an input and produces an output. The system is functionally a function: same input, similar output (with some stochasticity). In an agentic loop, the model's actions change the environment, which produces new observations, which change subsequent actions. The system is now a dynamical process, not a function.

This has important consequences:

**Path dependence** — what the system does depends on the history of its actions and observations, not just the initial input. Small differences in early steps can propagate into dramatically different trajectories.

**Emergent plan structures** — the model can develop multi-step action sequences that were not specified by the user and may not be easily interpretable from the individual steps. Behaviour at the plan level is not always deducible from behaviour at the step level.

**Failure mode amplification** — errors in early steps can compound. A hallucinated intermediate result, used as input to subsequent steps, can produce a cascade of incorrect actions.

**External consequence** — in systems where the agent has write access to the environment (can send emails, post content, execute commands, make purchases), the agentic loop has real-world consequences that are not easily reversed.

The closed-loop agentic system is therefore a qualitatively more complex object than a simple language model, both technically and philosophically. It is the agentic loop, combined with LoRA plasticity and RAG memory, that produces the kind of system the EmergentEvolution founding conversation was examining when it asked where the AI/AGI boundary lies.

---

## 7. Continual Learning: The Self-Modifying System {#continual-learning}

### 7.1 The Catastrophic Forgetting Problem {#catastrophic-forgetting}

Continual learning — the ability to learn new things over time without losing previously acquired knowledge — is a fundamental capability of biological learning systems. A human who learns calculus does not forget how to read. A child who learns a new language retains their native language.

Artificial neural networks suffer from a well-documented failure mode called catastrophic forgetting (also called catastrophic interference): when a trained model is fine-tuned on new data, it tends to overwrite the weights encoding prior knowledge. The new task dominates; the old task performance degrades.

This is a consequence of the gradient descent training process. Weights are adjusted to minimise loss on the current training data. These adjustments move weights away from the values that encoded previous knowledge. Without mechanisms to preserve prior knowledge, new learning destroys old learning.

Catastrophic forgetting is one of the most significant barriers between current AI systems and human-like continual learning. A static pre-trained model avoids this problem by not learning at all in deployment — but this comes at the cost of all the other limitations described above.

### 7.2 Current Approaches to Continual Learning {#continual-approaches}

Several approaches have been developed to address catastrophic forgetting, with varying degrees of success:

**Elastic Weight Consolidation (EWC)** — identifies which weights are most important for previous tasks (using the Fisher information matrix as a proxy) and penalises large changes to those weights during new training. Works for small-scale scenarios but scales poorly.

**Progressive Neural Networks** — adds new network columns for each new task, with lateral connections to prior columns. Prior columns are frozen; new columns can leverage prior representations. Avoids forgetting but grows unboundedly.

**Memory replay / Experience replay** — maintains a buffer of examples from previous tasks and interleaves them with new training data. The model is prevented from forgetting by being continuously reminded of prior tasks. Works reasonably well but requires storing data and scales poorly as the number of tasks grows.

**Meta-learning (Learning to Learn)** — trains models to adapt quickly to new tasks with minimal data, rather than training to perform any specific task. If successful, a meta-learned model should be able to acquire new capabilities quickly without forgetting because its weights encode a learning algorithm, not specific knowledge.

**LoRA-based continual learning** — using separate LoRA adapters for each task, keeping previous adapters frozen, and learning new adapters for new tasks. This avoids direct weight interference at the cost of growing the adapter set over time.

None of these approaches fully solves the problem at the scale and generality that would be needed for truly human-like continual learning. The field treats it as an open problem.

### 7.3 What Genuine Continual Learning Would Mean {#continual-genuine}

Genuine continual learning — the kind that would matter for the AGI question — would require a system that:

Acquires new knowledge and skills through interaction with the world, without explicit retraining by an external process.

Retains prior knowledge while integrating new knowledge, with the integration happening at the representational level (changing weights or equivalent) not just at the retrieval level (storing new documents in a RAG store).

Revises prior beliefs when new evidence conflicts with them, rather than holding both in parallel.

Maintains a unified, coherent model of the world that is updated by experience — not a collection of disconnected adapters and retrieval stores.

No current deployed system meets these criteria robustly. Research prototypes exist; some partially succeed on constrained benchmarks. The gap between these and biological continual learning remains large.

This matters because continual learning is one of the key architectural properties that would transform a sophisticated language model into something with a genuinely different relationship to time and experience. A system that genuinely learns continuously from interaction has a different kind of history than one that is periodically retrained offline. The difference is not just technical — it changes what it means to interact with the system over time.

---

## 8. Emergent Behaviours: What They Are and Are Not {#emergence}

Emergence is one of the most discussed and most misunderstood phenomena in contemporary AI. It is essential to characterise it carefully.

### 8.1 Defining Emergence Precisely {#emergence-definition}

In complex systems theory, emergence refers to the appearance of properties at the system level that are not straightforwardly predictable from the properties of the system's components.

There are weak and strong versions of this concept:

**Weak emergence** — the property is in principle derivable from the component-level description but is practically unpredictable because the derivation is too computationally expensive to perform. Traffic jams are a weakly emergent property of individual driving behaviours: each driver's behaviour is fully described by local rules, but the global traffic pattern is not easily predicted from those rules.

**Strong emergence** — the property is not derivable even in principle from the component-level description. Strong emergence is philosophically controversial; many scientists and philosophers are sceptical it exists, or reserve it only for consciousness.

For AI systems, essentially all discussed emergence is weak emergence: properties that arise from the training process and architecture but were not explicitly programmed and were not straightforwardly predicted in advance.

### 8.2 Documented Emergent Behaviours in LLMs {#emergence-documented}

Several behaviours have been documented as apparently emergent in large language models — appearing at certain scales but not at smaller scales of the same architecture:

**In-context learning** — the ability to perform a new task given only a few examples in the context window, without any weight updates. This capability was not present in smaller GPT models and appeared at GPT-3 scale. The underlying mechanism is still not fully understood.

**Chain-of-thought reasoning** — the ability to produce step-by-step reasoning traces that improve performance on complex problems. This ability emerged with scale and was not easily observed in smaller models.

**Instruction following** — before fine-tuning, larger models showed a qualitatively better ability to interpret and follow natural language instructions without the same fine-tuning overhead required for smaller models.

**Arithmetic and symbolic reasoning** — certain mathematical and symbolic reasoning capabilities appeared more abruptly at specific model scales than would be expected from a smooth scaling curve.

**Theory of mind proxies** — larger models show better performance on theory-of-mind tasks (inferring mental states of characters in stories, false belief tasks) than smaller models, with some tasks showing threshold-like behaviour.

**Analogical reasoning** — the ability to identify and apply abstract structural analogies improved with scale in ways that were not uniformly smooth.

### 8.3 Why Emergence Is Contested {#emergence-contested}

The existence and interpretation of emergent capabilities in LLMs is actively contested in the research community.

The main challenge: many apparent emergent capabilities may be artifacts of measurement rather than genuine threshold phenomena. If you measure performance with a strict metric (e.g., exact string match on a mathematical task), you may see a sharp jump from zero to non-zero performance at some scale — not because the capability emerged suddenly, but because the underlying competence was gradual and the metric only registers it above some threshold.

A 2023 paper by Schaeffer et al. argued that many apparent emergent capabilities disappear when measured with smoother metrics, suggesting they are metric artifacts. This is a serious methodological challenge.

The counterargument: even if some apparent emergences are metric artifacts, some are robust to alternative measurement — and the question of why complex capabilities sometimes appear more abruptly than expected from smooth loss curves is still an open scientific question.

The honest position: some apparent emergences are probably metric artifacts; some are probably genuine phase-transition-like phenomena in capability. Distinguishing them is currently an active area of research.

### 8.4 Phase Transitions and Capability Jumps {#phase-transitions}

A more technically precise way to think about emergence in AI is through the lens of phase transitions in statistical mechanics.

In physics, a phase transition is a rapid change in the macroscopic properties of a system as a control parameter (temperature, pressure) crosses a critical value. Water transitioning from liquid to gas is a familiar example. The macroscopic change is sharp even though the microscopic physics is continuous.

Analogously, as model scale (a control parameter) crosses certain values, macroscopic capabilities (task performance) may change rapidly — not because anything discontinuous is happening at the parameter level, but because the system crosses some threshold in its ability to represent or leverage certain patterns.

This framing is useful because it:

- Does not require strong emergence (the capability was always "implicit" in the architecture; scale unlocked it)
- Provides a physical intuition for why capabilities can appear without smooth gradual build-up
- Suggests that more capabilities may appear as scale increases, without requiring prediction of which capabilities or at what scale

The phase-transition framing is consistent with the position taken in the EmergentEvolution founding conversation: there is no single moment where "intelligence becomes real," but there are macroscopic transitions that are real even though the underlying system changes continuously.

### 8.5 The Philosophical Weight of Emergence {#emergence-philosophical}

Emergence matters philosophically for the AI/AGI question in a specific way: it suggests that the capabilities and properties of a system cannot be fully read off from its architecture and training procedure.

If a system with 10 billion parameters cannot do X, and a system with 100 billion parameters trained the same way can do X, then X is a property of scale — not just of architecture. And if capabilities can emerge without being explicitly programmed, then the question "what is this system capable of" has an empirical rather than a purely architectural answer.

This is uncomfortable for both overclaiming and dismissive positions. The dismissive "it's just pattern matching" position implicitly assumes that the capabilities of a system are fully characterised by its training objective. Emergence suggests they are not. The overclaiming "it can do anything" position is also challenged: emergent capabilities appear at particular scales for particular architectures and are not universally generalising.

The most honest position is that we are empirically discovering what these systems can do, and our ability to predict those capabilities in advance is limited. This epistemic humility is appropriate and should shape how we think about what these systems are.

---

## 9. In-Context Learning: The Other Kind of Adaptation {#in-context}

In-context learning (ICL) is one of the most surprising and theoretically interesting properties of large language models, and deserves separate treatment from fine-tuning-based adaptation.

In-context learning refers to the model's ability to improve its performance on a task by observing examples of that task within the context window, without any weight updates. You show the model three examples of "question → answer" pairs, then ask a new question, and the model correctly applies the pattern — even if it has never explicitly seen this type of task in training.

Why is this surprising? Because it resembles learning without the system actually learning (in the technical sense of weight modification). The model is adapting its behaviour to the demonstrated pattern without gradient descent.

The mechanism is not fully understood, but several theories have been proposed:

**Task selection hypothesis** — during pre-training, the model encountered many different tasks and learned representations for all of them. In-context examples serve as a signal that activates the appropriate task representation. The model is not learning the task; it is identifying which of its pre-trained tasks is relevant.

**Meta-learning hypothesis** — the pre-training process implicitly performs a form of meta-learning: the model learns not just tasks but the structure of learning across tasks. The in-context examples instantiate a gradient descent-like computation in the model's forward pass through the attention mechanism.

**Bayesian inference hypothesis** — the model uses the in-context examples to update a prior over possible tasks, performing a form of Bayesian inference. The examples shift the probability distribution over outputs toward patterns consistent with the demonstrated task.

These hypotheses are not mutually exclusive and likely each capture something true. The practical consequence: large language models can perform tasks demonstrated by a few examples with no training, which dramatically expands their effective capability.

For the purposes of this study, in-context learning matters because it demonstrates that the line between "learning" and "retrieval" is blurrier than it appears. A model that performs a new task after seeing examples is doing something that resembles learning, even if its weights are not changing. The standard claim "it can't learn during deployment" is complicated by this phenomenon.

---

## 10. Mixture of Experts: Conditional Computation {#moe}

Mixture of Experts (MoE) is an architectural approach that is increasingly important in frontier models, including DeepSeek and reportedly GPT-4.

In a standard dense Transformer, every parameter participates in every forward pass. For a 100-billion parameter model, every token is processed by all 100 billion parameters. This is computationally expensive.

A Mixture of Experts model has a larger total parameter count but only activates a subset of parameters for each token. The model contains many "expert" sub-networks (typically feed-forward networks), plus a routing mechanism that selects which experts process each token. Typically, a token is routed to 2-8 experts out of potentially hundreds.

The result: a model with a very large total parameter count (and therefore large knowledge capacity) but computational cost closer to a much smaller dense model. DeepSeek-V3 reportedly has 671 billion total parameters but activates around 37 billion per token — giving it the knowledge capacity of a very large model with inference costs closer to a medium model.

Beyond efficiency, MoE has an interesting structural implication: different experts may specialise in different types of content or reasoning. Routing decisions are learned during training — the router learns which experts handle which inputs best. The result may be that different kinds of tokens (mathematical content, code, natural language, different languages) are processed by different subsets of parameters.

This specialisation is a form of modularity within the model — different "skills" may be localised in different expert networks. This has potential implications for fine-tuning (you might fine-tune specific experts for specific domains) and for interpretability (different experts may be more individually interpretable than the entangled representations in a dense model).

---

## 11. Chain-of-Thought and Extended Reasoning {#chain-of-thought}

Chain-of-thought (CoT) prompting, and its extended form in models like o1/o3 and DeepSeek-R1, represents a distinct approach to improving AI reasoning performance.

The basic observation: language models perform better on complex reasoning tasks when they generate intermediate reasoning steps, rather than attempting to produce the final answer directly. "Let me think step by step" followed by a worked reasoning trace leads to more accurate final answers than direct answer generation.

Why does this work? Several explanations:

**Computational advantage** — generating a longer sequence of tokens gives the model more "compute" to apply to the problem. Transformers are limited in how much processing they can do per forward pass; a longer generation allows more processing steps.

**Error localisation** — explicit intermediate steps allow errors to be caught and corrected within the generation, rather than propagating silently to the final answer.

**Attention over intermediate results** — later tokens in the reasoning chain can attend to earlier tokens, allowing the model to "look back" at prior steps. This implements a form of working memory within the generation.

**Training distribution alignment** — if the training data contains many worked examples with explicit reasoning steps, the model has learned to associate correct final answers with explicit intermediate steps.

Modern "reasoning models" (o1, o3, DeepSeek-R1) extend this by training models to produce long internal reasoning traces before their final response. The training process reinforces reasoning chains that lead to correct answers using reinforcement learning. The result is models that, on complex mathematical and scientific tasks, generate extensive reasoning before concluding — and achieve substantially better accuracy than models that do not.

This development is philosophically interesting because it represents a form of extended computation that resembles, at least superficially, deliberation. The model is not simply retrieving a cached answer — it is working through a problem in a way that can be traced. Whether this constitutes genuine reasoning or a very convincing simulation of it is one of the genuinely hard questions that this study does not pretend to resolve.

---

## 12. What These Techniques, Combined, Produce {#combined}

Having surveyed these techniques individually, it is worth considering what they produce in combination.

A system with:
- **LoRA fine-tuning** → parameter plasticity, ability to shape internal representations through experience
- **RAG** → persistent external memory, access to continuously updated knowledge
- **Tool use** → action in environment, closed-loop feedback, real-world consequence
- **Agentic architecture** → multi-step planning, sequential action, environmental coupling
- **Continual learning mechanisms** → ongoing adaptation without full retraining
- **Chain-of-thought reasoning** → extended deliberation, error localisation, working memory in generation

...is a qualitatively different object from a static-weights LLM.

The combined system has something like:
- Memory (persistent and queryable, if not fully integrated)
- Learning (bounded and often offline, but present)
- Agency (actions with real-world consequences)
- Deliberation (extended reasoning chains)
- Environmental coupling (feedback loops with the world)

This does not mean such a system is intelligent in the philosophically rich sense. It means the easy dismissals are no longer descriptively accurate. The question of what this system *is* — where it sits on spectrums from tool to agent, from simulator to reasoner — requires the kind of careful analysis that the rest of this study attempts to develop.

The combination of these techniques is not yet deployed as a unified system in commercial products at full sophistication. Elements appear in different products to different degrees. But the research frontier is actively working toward more integrated versions, and systems combining several of these properties already exist in research and in advanced commercial deployments.

---

## 13. The Architectural Horizon: Where This Is Going {#horizon}

The techniques described in this document are the current frontier. The trajectory they represent points toward:

**More integrated memory systems** — moving away from the separation between parametric memory (weights) and external memory (RAG), toward systems where interaction experience updates internal representations in something closer to how biological memory consolidation works.

**More adaptive architectures** — systems where the network structure itself, not just the weights, can be modified through experience. Neurogenesis analogies: adding capacity where it is needed, pruning where it is not.

**More robust continual learning** — solving catastrophic forgetting at the scale and generality needed for open-ended deployment.

**Tighter environment coupling** — systems that are not just text generators with tool access but persistent agents that maintain ongoing models of their environment, updated by continuous observation.

**More sophisticated self-modification** — systems that can not only update their weights but can modify their own reasoning processes, learning algorithms, or architectural parameters.

Each of these moves the systems further from the closed, static-weights model and closer to the kind of open-ended adaptive agency that the AGI question is really asking about.

The key phrase in that last sentence is "the kind of." The gap between "has some adaptive properties" and "is a general adaptive agent" is still very large. But the direction of travel is clear, and the rate is not slow.

---

*EmergentEvolution — Advanced Techniques: LoRA, RAG, and Emergent Behaviours*
*Document prepared as part of a structured study of artificial intelligence, emergence, and adaptive systems.*

---
