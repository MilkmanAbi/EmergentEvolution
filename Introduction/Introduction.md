# Introduction: What Is AI, Actually?

### *EmergentEvolution — Document 1 of the Foundational Series*

---

> *This document is the starting point of the EmergentEvolution study. Its goal is simple and specific: to establish what artificial intelligence actually is — not in the marketing sense, not in the science-fiction sense, but in the technical, theoretical, and conceptual sense. This means separating the underlying science from the products built on it, separating what the field claims from what it has actually achieved, and building a foundation precise enough to support everything that comes after.*

---

## Table of Contents

1. [Why This Document Exists](#why)
2. [The Word "Intelligence" Is Doing Too Much Work](#intelligence-word)
3. [What Intelligence Actually Means in a Technical Context](#intelligence-technical)
4. [The Conceptual Foundation: What Is Machine Learning?](#ml-foundation)
   - 4.1 [Learning as Optimisation](#learning-optimisation)
   - 4.2 [The Three Paradigms of Learning](#three-paradigms)
   - 4.3 [What a Model Actually Is](#what-is-model)
   - 4.4 [What Training Actually Is](#what-is-training)
5. [The Architecture That Changed Everything: Neural Networks](#neural-networks)
   - 5.1 [The Biological Metaphor and Why It Is Misleading](#bio-metaphor)
   - 5.2 [Layers, Weights, and Activations](#layers-weights)
   - 5.3 [Backpropagation: How Networks Actually Learn](#backprop)
   - 5.4 [Deep Learning: When Depth Matters](#deep-learning)
6. [The Transformer: The Architecture Behind Modern AI](#transformer)
   - 6.1 [The Attention Mechanism](#attention)
   - 6.2 [Why Transformers Dominate](#why-transformers)
   - 6.3 [What a Large Language Model Is, Precisely](#llm-precise)
7. [Theory vs. Product: The Gap That Matters](#theory-vs-product)
   - 7.1 [The Research Lineage](#research-lineage)
   - 7.2 [What Commercialisation Does to a Model](#commercialisation)
   - 7.3 [RLHF: Aligning to Human Preference](#rlhf)
   - 7.4 [The Safety and Compliance Layer](#safety-layer)
8. [The Major Commercial Systems: What They Actually Are](#commercial-systems)
   - 8.1 [ChatGPT / GPT Series (OpenAI)](#chatgpt)
   - 8.2 [Claude (Anthropic)](#claude)
   - 8.3 [Gemini (Google DeepMind)](#gemini)
   - 8.4 [DeepSeek](#deepseek)
   - 8.5 [What They Have in Common](#commonalities)
9. [What Current AI Cannot Do](#cannot-do)
10. [Terminology Reference: Words That Get Misused](#terminology)
11. [Where This Study Goes From Here](#where-next)

---

## 1. Why This Document Exists {#why}

Artificial intelligence is simultaneously one of the most discussed and most misunderstood topics in public discourse. The misunderstanding runs in two opposite directions at the same time.

On one side: overclaiming. AI systems are routinely described as "thinking," "understanding," "knowing," and "reasoning" in ways that attribute internal properties which have not been established and may not exist. Marketing language, science fiction, and breathless journalism have created a folk theory of AI that is substantially disconnected from what these systems actually do.

On the other side: dismissive reductionism. The counter-reaction, often from technically informed people, collapses in the opposite direction: "it's just statistics," "it's just autocomplete," "it's just pattern matching." These descriptions are not wrong exactly, but they are at the wrong level of abstraction — like describing a symphony as "just air pressure waves" or a human decision as "just electrochemical signals." Technically accurate, explanatorily useless.

Neither the overclaiming nor the reductionist position gives you the tools to think clearly about what is actually happening in these systems, what their capabilities and limits are, and what questions about them are philosophically live. This document attempts to give you those tools.

The approach taken here is layered: start with the conceptual foundations of machine learning, build up through neural network architecture to the specific structures behind modern large language models, then examine what commercialisation does to research models, and finally situate the major commercial systems in that framework.

By the end of this document, you should be able to distinguish clearly between what the underlying science claims, what commercial products are built to do, and where the genuinely hard questions live.

---

## 2. The Word "Intelligence" Is Doing Too Much Work {#intelligence-word}

Before going further, it is worth pausing on the word "intelligence" itself, because it is causing most of the confusion.

In ordinary language, "intelligence" means something like: the capacity to understand, reason, learn, and solve problems in flexible and general ways. It implies an inner life — something that grasps meaning, not just processes symbols. When we call a person intelligent, we are attributing to them not just behavioural competence but a mental capacity behind that competence.

When engineers and researchers use "intelligence" in "artificial intelligence," they are using the word differently — or they should be. In the technical literature, intelligence is defined operationally and behaviourally. A system is "intelligent" if it produces outputs that, when produced by a human, would be taken to indicate intelligence. This is the spirit of the Turing Test: intelligence is defined by behavioural equivalence, not by inner similarity.

This gap between ordinary and technical usage is not just semantic. It is the source of most AI hype and most AI dismissal. When a marketer says "our AI understands your request," they are using the ordinary-language meaning. When a researcher says "the model achieves human-level performance on benchmark X," they are using the technical meaning. These are different claims, and conflating them produces nonsense.

There is a third usage, which is the one that creates the most philosophical trouble: the implied-meaning usage. When an AI system is described as "knowing" something, or "believing" something, or "deciding" something, the language implies the ordinary meaning without stating it. The system "knows" that Paris is the capital of France in the sense that it reliably produces that output — but the word "knows" carries connotations of genuine epistemic states that have not been established.

Throughout this study, we will be specific about which sense of these terms we are using. Where a system exhibits a behaviour that resembles intelligence, we will describe the behaviour. Where we are making claims about internal states, we will flag that these are claims and examine what evidence supports them.

---

## 3. What Intelligence Actually Means in a Technical Context {#intelligence-technical}

The field of artificial intelligence has never settled on a single definition of intelligence, and this is not an accident or oversight. It reflects a genuine theoretical problem: intelligence is not a single thing.

What we call "intelligence" is a cluster of distinct competencies:

**Perception** — the ability to extract structured information from raw sensory data. Recognising a face in an image, parsing speech from audio, reading text from a photograph.

**Memory** — the ability to store information and retrieve it reliably under varying conditions.

**Reasoning** — the ability to draw inferences from available information, including deductive inference (if A then B, A, therefore B), inductive generalisation (this pattern holds in many cases, probably holds in general), and abductive reasoning (what is the most likely explanation for these observations).

**Planning** — the ability to sequence actions toward a goal, including anticipating consequences and adapting when outcomes differ from predictions.

**Learning** — the ability to improve performance on a task based on experience, without explicit reprogramming.

**Generalisation** — the ability to apply knowledge or skills learned in one context to novel contexts.

**Communication** — the ability to express internal states and intentions in forms interpretable by other agents.

Human intelligence involves all of these, deeply integrated. What is called "artificial intelligence" is not a single unified system — it is a collection of approaches to building systems that exhibit one or more of these competencies, to varying degrees, in various domains.

Current AI systems, including the most advanced large language models, excel at some of these competencies and are dramatically limited in others. They show remarkable performance on perception (image recognition, speech parsing), strong apparent reasoning in many domains, and impressive communication. They struggle with robust planning, reliable generalisation outside training distribution, and certain kinds of multi-step logical inference.

The "intelligence" label is therefore doing enormous compression. Saying "this is an AI system" says almost nothing about what the system can actually do, or how it does it. This is part of why precise description matters.

---

## 4. The Conceptual Foundation: What Is Machine Learning? {#ml-foundation}

Machine learning is the subfield of AI concerned with building systems that learn from data rather than being explicitly programmed with rules.

The distinction matters. Classical rule-based AI (sometimes called "Good Old-Fashioned AI" or GOFAI) works by encoding knowledge as explicit rules: if the input matches pattern X, produce output Y. This works well for narrow, well-defined problems where the rules can be specified completely and correctly. It fails badly when the problem is too complex for rules to be enumerated, when the rules cannot be known in advance, or when the relevant patterns are too subtle or high-dimensional for human specification.

Machine learning takes a different approach: instead of specifying the rules, specify the goal and provide examples. The system figures out the rules by itself, by finding patterns in the examples that correlate with the goal.

This is a fundamental paradigm shift. It means the behaviour of a machine learning system is not fully determined by what the programmer wrote — it is substantially determined by the data the system was trained on. The programmer designs the learning process; the data shapes what is learned.

### 4.1 Learning as Optimisation {#learning-optimisation}

The core idea of machine learning is that learning is optimisation.

A machine learning system has parameters — adjustable numerical values that determine its behaviour. A loss function (also called an objective function or cost function) measures how far the system's current outputs are from the desired outputs on a given set of examples. Training is the process of adjusting the parameters to reduce the loss.

This is optimisation in the mathematical sense: finding the parameter values that minimise (or maximise) some objective. The field of machine learning is largely concerned with how to define good objectives, how to optimise them efficiently, and how to ensure that doing well on the training examples transfers to doing well on new examples.

The transfer question — can the system generalise beyond its training data? — is the central challenge of machine learning. A system that merely memorises its training examples has not learned anything useful. What we want is a system that has extracted patterns general enough to apply to new cases.

This is what "generalisation" means technically: performance on data not seen during training. A model that generalises well has learned something about the structure of the problem, not just the specific examples.

### 4.2 The Three Paradigms of Learning {#three-paradigms}

Machine learning is divided into three major paradigms based on what kind of feedback the learning process uses.

**Supervised Learning**

The system is trained on labelled examples: input-output pairs where the correct output is known. The system learns to map inputs to outputs by adjusting its parameters to produce outputs close to the labels. Classification (is this image a cat or a dog?), regression (what is the likely price of this house?), and translation (what is the English equivalent of this French sentence?) are all supervised learning problems.

The quality of supervised learning is directly limited by the quality and quantity of labelled data. Labelling data is expensive and time-consuming. The model can only learn patterns that are present in the labels — if the labels are biased or incomplete, the model's outputs will be too.

**Unsupervised Learning**

The system is trained on unlabelled data. There are no explicit correct outputs. Instead, the system is tasked with finding structure in the data: clustering similar examples, compressing data into lower-dimensional representations, generating new examples consistent with the training distribution.

Unsupervised learning is more general but also harder to evaluate — without labels, it is not always clear what "learning something useful" means. In practice, unsupervised learning is often used to pre-train representations that are then fine-tuned on labelled data.

**Reinforcement Learning**

The system (called an agent) learns by interacting with an environment and receiving reward signals. The agent takes actions, the environment produces outcomes, and the agent receives a reward (positive or negative) based on those outcomes. The agent learns to select actions that maximise cumulative reward over time.

Reinforcement learning is the paradigm closest to how we intuitively imagine learning from consequences. It is used in game-playing systems (AlphaGo, OpenAI Five), robotics, and — critically for modern language models — aligning model outputs to human preferences (RLHF, discussed later).

### 4.3 What a Model Actually Is {#what-is-model}

The word "model" in machine learning has a specific technical meaning that is worth establishing clearly.

A model is a parameterised mathematical function: a mapping from inputs to outputs whose behaviour is determined by a set of numerical parameters (usually called weights). Given an input, the model computes an output by applying the function with its current parameter values.

The function itself — its structure, how it processes inputs, what kinds of representations it can build — is the architecture. The parameter values are learned during training. The architecture is designed by engineers; the parameters are found by the optimisation process.

An important consequence: two identical architectures trained on different data will behave differently. The same architecture trained twice on the same data (with different random initialisations) may also behave differently. The model is not just the architecture — it is the architecture plus the trained parameters.

When people say "the model" in practice, they often mean the combination of architecture and trained weights. This combination is what gets deployed, what users interact with, and what exhibits the behaviours we are studying.

### 4.4 What Training Actually Is {#what-is-training}

Training is the process of finding parameter values that make the model perform well on the training objective. In practice, this means running an optimisation algorithm — almost always some variant of gradient descent — on a very large dataset.

Gradient descent works as follows. The loss function assigns a scalar value to the model's current parameters, measuring how poorly the model performs. The gradient of the loss function with respect to the parameters is a vector pointing in the direction of steepest increase. Moving in the opposite direction — gradient descent — reduces the loss.

In practice, computing the gradient over the entire dataset is computationally prohibitive for large datasets. Instead, stochastic gradient descent uses a small random sample (a minibatch) to estimate the gradient at each step. This estimate is noisy but computationally tractable, and averaging over many steps tends to converge to a good solution.

Training a large modern model involves running this process billions of times, over trillions of tokens of text or other data, on thousands of specialised processors running in parallel for weeks or months. The resulting parameter values encode whatever patterns the optimisation process found useful for reducing the training loss.

What is encoded in those parameters is not human-readable rules. It is a distributed representation — patterns spread across billions of numerical values in ways that do not correspond to any explicit concept or rule. This is what makes modern AI models both powerful and opaque.

---

## 5. The Architecture That Changed Everything: Neural Networks {#neural-networks}

Modern machine learning is dominated by one family of architectures: artificial neural networks. To understand current AI systems, you need to understand what these are and how they work.

### 5.1 The Biological Metaphor and Why It Is Misleading {#bio-metaphor}

Artificial neural networks were inspired by, and named after, biological neural networks — the networks of neurons in animal brains. This historical connection is real but has become more misleading than helpful.

The inspiration: biological neurons receive signals from other neurons via dendrites, sum those signals, and if the sum exceeds a threshold, fire an electrical pulse that travels via the axon to other neurons. Learning in biological systems involves changes in the strength of connections (synapses) between neurons — this is the basis of synaptic plasticity.

Artificial neurons loosely mirror this: they receive numerical inputs, compute a weighted sum, apply a nonlinear function (activation function), and pass the result to subsequent neurons. Artificial networks are arranged in layers and trained by adjusting the connection weights.

The metaphor breaks down in almost every detail beyond this loose analogy. Biological neurons are enormously complex electrochemical devices, not simple weighted sums. The brain is not organised into the neat feedforward layers typical of artificial networks. Biological learning involves dozens of cellular mechanisms that have no artificial counterpart. The timescales, energy budgets, and architectural principles are completely different.

More importantly: the fact that artificial neural networks were inspired by biological ones does not mean they work the same way, learn the same way, or implement anything like the same computations. Airplanes were inspired by birds, but they do not fly by flapping their wings.

The biological metaphor is useful for historical context and as a loose intuition pump. It should not be taken as a serious account of what artificial neural networks are doing.

### 5.2 Layers, Weights, and Activations {#layers-weights}

A neural network consists of layers of artificial neurons (also called units or nodes). Each neuron in a layer receives inputs from the previous layer, computes a weighted sum of those inputs plus a bias term, applies an activation function to the result, and passes the output to the next layer.

The weights are the parameters that are learned during training. A weight on a connection from neuron i to neuron j determines how much neuron i's output contributes to neuron j's input. High positive weights mean neuron i's activation strongly activates neuron j. Weights near zero mean the connection is weak. Negative weights mean neuron i suppresses neuron j.

The activation function introduces non-linearity into the computation. Without it, a deep stack of linear operations would collapse to a single linear function — depth would provide no expressive benefit. Activation functions like ReLU (Rectified Linear Unit), sigmoid, and tanh allow the network to represent non-linear functions of arbitrary complexity.

The input layer receives the raw data. The output layer produces the network's prediction or generation. The layers in between are called hidden layers — "hidden" because their outputs are not directly observed.

A network with many hidden layers is called a deep neural network. "Deep learning" refers to the use of such deep networks, and it is deep learning that is responsible for essentially all of the major advances in AI over the past decade.

### 5.3 Backpropagation: How Networks Actually Learn {#backprop}

The algorithm that makes training deep networks possible is backpropagation. Understanding it conceptually (even without the mathematics) is important for understanding what training actually does.

The problem: to update the weights using gradient descent, you need to know the gradient of the loss with respect to every weight in the network. For a network with millions or billions of weights, computing this naively is intractable.

Backpropagation solves this using the chain rule of calculus. The computation of the network — from input through all hidden layers to output — defines a composed function. The derivative of a composed function can be computed by multiplying the derivatives of its components (the chain rule). Backpropagation efficiently computes all the required derivatives in a single backward pass through the network, by propagating the error signal from the output back toward the input.

The result is that for every weight in the network, you have an exact computation of how much changing that weight would increase or decrease the loss. Gradient descent then adjusts all the weights slightly in the direction that reduces the loss.

Repeated over billions of examples, this process shapes the network's weights so that it becomes progressively better at the training task. The weights that emerge are not designed — they are found. The optimisation process discovered that these particular numerical values, among all possible parameter configurations, produce outputs close to the training targets.

### 5.4 Deep Learning: When Depth Matters {#deep-learning}

The key insight that reignited AI research in the early 2010s was that depth — using many hidden layers — dramatically increases what a neural network can learn from data, particularly for perceptual and linguistic tasks.

Why does depth help? The intuitive answer is that deep networks can build hierarchical representations. In image recognition, lower layers might learn to detect edges and textures. Middle layers might learn to combine those into parts (eyes, wheels, windows). Higher layers might learn to combine parts into objects. Each layer builds on the representations of the layer below, progressively abstracting from raw pixels toward conceptual categories.

This compositional structure — lower-level features combined into higher-level features — matches the structure of many real-world problems. Language has such structure: letters form words, words form phrases, phrases form sentences, sentences form arguments. Hierarchical representations are naturally suited to learning from hierarchically structured data.

The practical challenge of training deep networks — the vanishing gradient problem, where gradient signals degrade as they propagate back through many layers — was addressed by a combination of better activation functions, better initialisation strategies, batch normalisation, and eventually residual connections (skip connections that allow gradient flow to bypass deep stacks of layers).

By the mid-2010s, deep learning had achieved decisive performance improvements over all prior approaches in image recognition, speech recognition, and natural language processing. The field of AI was restructured around it.

---

## 6. The Transformer: The Architecture Behind Modern AI {#transformer}

The specific architecture behind all major current language models — GPT, Claude, Gemini, DeepSeek, and others — is the Transformer, introduced in the 2017 paper "Attention Is All You Need" by Vaswani et al.

### 6.1 The Attention Mechanism {#attention}

The central innovation of the Transformer is the self-attention mechanism. To understand why it matters, we need the context of what came before.

Prior to Transformers, sequential data like language was typically processed with recurrent neural networks (RNNs) or LSTMs. These architectures processed sequences element by element — one word at a time — maintaining a hidden state that accumulated information from all previous elements. This was natural for sequential data but had two major problems: it was slow to train (sequential computation cannot be parallelised) and it struggled to maintain information over long sequences (information from early in the sequence tended to be lost by the time the model processed later parts).

Attention mechanisms were originally introduced as an add-on to recurrent models to help them access relevant earlier parts of the sequence. The Transformer replaced the recurrence entirely with attention.

Self-attention works as follows. Given a sequence of tokens (words or word-pieces), the model computes for each token a weighted combination of all other tokens in the sequence. The weights are determined by learned relevance scores: how relevant is each other token to the current token, given the current context?

For example, when processing the word "it" in "the animal was tired because it had been running," the model should assign high attention weight to "animal" — that is the referent of "it." Self-attention provides a mechanism for each token to directly access information from every other token in the sequence, regardless of distance.

The computation uses three learned projections of each token's representation: Query, Key, and Value. The attention weight between two tokens is computed as the similarity between one token's Query and the other's Key. The output for each token is then a weighted sum of the Values of all tokens, using the attention weights. Multiple attention "heads" run in parallel, each attending to different aspects of the relationships between tokens.

### 6.2 Why Transformers Dominate {#why-transformers}

Transformers became dominant for several compounding reasons:

**Parallelisability.** Unlike recurrent networks, Transformers process all positions in a sequence simultaneously. This means training can be massively parallelised across many processors, enabling training on much larger datasets in practical timeframes.

**Scalability.** Transformer performance scales smoothly with model size (number of parameters) and dataset size. As you add more parameters and more data, performance improves reliably — a property that does not hold for all architectures. This scaling behaviour, empirically discovered and partially theorised, is what made the "large language model" approach viable.

**Expressiveness.** The self-attention mechanism can capture complex, long-range dependencies in sequences that earlier architectures struggled with.

**Flexibility.** The same basic architecture works well for text, images (Vision Transformers), audio, video, protein sequences, and multimodal combinations. This generality made Transformers a unified foundation for multiple domains.

The consequence: essentially all frontier AI models today are Transformers or close derivatives. The architecture is not perfect — it has known limitations, particularly with very long context and with precise numerical computation — but its scalability and flexibility have made it the default choice.

### 6.3 What a Large Language Model Is, Precisely {#llm-precise}

A large language model (LLM) is a Transformer-based neural network trained to model the probability distribution of text. Concretely, this means: given a sequence of tokens, predict the probability distribution over what token comes next.

This is called the language modelling objective. The training data is simply text — no labels required. The model is trained to predict the next word (or subword token) given the preceding context. Over trillions of tokens, it learns to assign high probability to sequences that are coherent, factually consistent with its training data, grammatically well-formed, and stylistically appropriate to context.

To generate text, an LLM samples from its learned probability distributions sequentially: predict the next token, add it to the context, predict the next token given the extended context, and so on. What appears to be "thinking" or "composing" is this sampling process, shaped by a probability distribution learned over an enormous corpus.

This framing is important because it clarifies what the model is optimised to do: predict likely continuations of text, based on patterns in its training data. It is not optimised to be truthful, to reason correctly, or to represent the world accurately — at least not directly. To the extent that it does these things, it is because truth-telling, correct reasoning, and accurate world-representation were patterns statistically prevalent in the training data, and predicting text well required learning those patterns.

The "large" in large language model refers to the number of parameters. GPT-3 (2020) had 175 billion parameters. Current frontier models are estimated to be in the range of hundreds of billions to over a trillion parameters (exact figures are not always disclosed). The scale matters because larger models, trained on more data, have consistently shown better performance across a wide range of tasks — a trend sometimes called the scaling law.

---

## 7. Theory vs. Product: The Gap That Matters {#theory-vs-product}

There is a significant gap between what machine learning researchers study and what commercial AI products are. Understanding this gap is essential for evaluating claims about AI systems accurately.

### 7.1 The Research Lineage {#research-lineage}

The academic and research lineage behind current AI runs through decades of work in statistics, linear algebra, optimisation, cognitive science, and computer science. The specific technical lineage of large language models includes:

- Neural language models (Bengio et al., 2003) — first demonstration that neural networks could learn useful word representations from text
- Word2Vec (Mikolov et al., 2013) — efficient training of dense word embeddings
- Sequence-to-sequence models with attention (Bahdanau et al., 2014; Sutskever et al., 2014) — attention mechanisms for machine translation
- The Transformer (Vaswani et al., 2017) — the foundational architecture
- GPT (Radford et al., 2018) — applying Transformer language modelling at scale
- BERT (Devlin et al., 2018) — bidirectional Transformer pre-training for downstream tasks
- Scaling laws (Kaplan et al., 2020) — empirical discovery that performance scales predictably with model size and data
- GPT-3 (Brown et al., 2020) — demonstration of few-shot in-context learning at scale

Each of these papers contributed to understanding how to build systems that learn from text. The researchers involved were asking questions about learning, representation, generalisation, and architecture. They were largely not thinking about consumer products.

### 7.2 What Commercialisation Does to a Model {#commercialisation}

Taking a research language model and turning it into a commercial product involves several additional steps that significantly change the system's behaviour.

A raw language model trained on internet text is not useful as a product. It will: complete text in ways that are statistically plausible but often incoherent or offensive; follow no consistent persona or conversational convention; have no concept of being an "assistant"; reproduce racist, toxic, and harmful content if that content was statistically common in its training data; and generate text that sounds confident regardless of accuracy.

The transformation from research artefact to commercial product typically involves:

**Instruction fine-tuning** — additional training on examples of instructions paired with desired responses. This teaches the model to interpret prompts as instructions and respond helpfully, rather than simply continuing text.

**RLHF (Reinforcement Learning from Human Feedback)** — a process where human raters evaluate model outputs, their preferences are used to train a reward model, and the language model is then fine-tuned using reinforcement learning to produce outputs the reward model rates highly. This is the primary mechanism for making models coherent, helpful, and aligned to user preferences.

**Safety fine-tuning** — additional training to reduce harmful outputs, refusals on dangerous requests, and compliance with policies. This involves both additional labelled examples and techniques to reduce model susceptibility to adversarial prompting.

**System prompts** — persistent instructions provided at the beginning of every conversation that establish the model's persona, capabilities, limitations, and guidelines. Most commercial deployments use extensive system prompts that the user does not see.

**Infrastructure** — retrieval systems, tool access, memory management, rate limiting, moderation layers. The "product" the user interacts with is not just the model; it is the model plus an extensive surrounding infrastructure.

The result is a system whose behaviour is shaped by at least three different forces: the patterns in the pre-training data, the preferences of the human raters used in RLHF, and the policy decisions of the organisation deploying it.

### 7.3 RLHF: Aligning to Human Preference {#rlhf}

Reinforcement Learning from Human Feedback deserves more detailed examination because it is the primary mechanism through which commercial AI systems are shaped, and because it has important implications for what these systems are.

The basic process:

1. The pre-trained language model is used to generate multiple responses to a set of prompts.
2. Human raters compare these responses and indicate preferences — which response is better, and in what ways.
3. These preferences are used to train a separate model: the reward model. The reward model learns to predict human preferences — to assign high scores to outputs raters would prefer.
4. The language model is then further trained using reinforcement learning (typically Proximal Policy Optimisation or similar), with the reward model providing the reward signal. The language model learns to generate outputs that receive high scores from the reward model.

This process effectively encodes the preferences of the human rater population into the model's behaviour. If raters prefer confident-sounding responses, the model will tend toward confidence. If raters prefer certain formats or styles, the model will adopt them. If raters penalise hedging, the model will hedge less — regardless of whether hedging is epistemically appropriate.

This has a critical implication: the model's output style and content reflect not just the world as represented in training data, but the preferences of a specific human rater population, filtered through the design decisions of the research team that set up the rating process.

It also means the model is not optimising for truth or accuracy directly. It is optimising for human-rated preference. These often coincide — humans generally prefer accurate responses — but they do not always. A model that has learned to appear confident and helpful may be more likely to generate plausible-sounding but incorrect information than a model that has learned to be calibrated in its uncertainty, if raters have inadvertently penalised uncertainty.

### 7.4 The Safety and Compliance Layer {#safety-layer}

All major commercial AI systems have additional layers of safety training and content policy enforcement. This includes:

**Constitutional AI (Anthropic)** — a technique where the model is trained to critique and revise its own outputs according to a set of principles, reducing reliance on human labelling for safety-relevant behaviours.

**Red-teaming** — systematic adversarial testing where teams attempt to elicit harmful outputs, with the results used to improve safety training.

**Content classifiers** — separate models that evaluate inputs and outputs for policy violations, running in parallel with the main model.

**Hard refusal training** — explicit training to refuse certain categories of requests, combined with adversarial examples to make these refusals robust to prompt injection and jailbreaking.

The safety layer is not merely an ethical addition — it is commercially necessary. A deployed AI system that readily generates harmful content creates legal, reputational, and regulatory risks for the deploying organisation. The safety training is partly idealistic and partly a business requirement.

The consequence for users: the model's refusals and safety behaviours are not properties of the underlying language model as a research artefact. They are properties of the commercial product that has been built on top of it. Different organisations make different decisions about where to draw these lines, resulting in systems with different capabilities and different restrictions.

---

## 8. The Major Commercial Systems: What They Actually Are {#commercial-systems}

With this foundation established, we can give honest characterisations of the major commercial AI systems.

### 8.1 ChatGPT / GPT Series (OpenAI) {#chatgpt}

OpenAI's GPT series represents the direct commercial lineage of the original scaling-law research. GPT-3 (2020) was the first model to demonstrate convincingly that scale alone — more parameters, more data, more compute — could produce remarkable general-purpose language capabilities without task-specific fine-tuning.

GPT-3.5 and GPT-4 (the models behind ChatGPT) added instruction fine-tuning and RLHF on top of the GPT pre-training approach. ChatGPT (launched November 2022) wrapped this in a conversational interface and became the fastest consumer product to reach 100 million users in history.

GPT-4 introduced multimodal capability (accepting both text and images as input) and showed substantially improved reasoning performance over GPT-3.5, particularly on structured reasoning tasks, coding, and professional-domain questions.

The GPT-4o and subsequent models further improved multimodal capability, latency, and conversational naturalness. OpenAI's o1/o3 series introduced extended "chain-of-thought" reasoning — the model generates a longer internal reasoning trace before producing an answer, improving performance on complex multi-step problems.

OpenAI's approach is characterised by: aggressive scaling as the primary performance driver, commercial deployment as a priority alongside research, and relatively closed disclosure (model details are not published). The organisation's structure — a capped-profit company with an unusual governance arrangement — has been a source of ongoing controversy and internal conflict.

### 8.2 Claude (Anthropic) {#claude}

Anthropic was founded in 2021 by former OpenAI researchers, including Dario and Daniela Amodei, in part due to disagreements about safety priorities and organisational direction. Claude is the company's commercial AI system.

The distinctive technical contribution associated with Anthropic is Constitutional AI (CAI), an approach to safety training where the model is guided by a set of written principles rather than purely by human preference ratings. The claimed advantage is greater consistency and interpretability in safety-related behaviours.

Claude models (Claude 1 through the current Claude series) are characterised by: emphasis on careful, nuanced reasoning; a tendency toward hedging and epistemic caution; strong performance on long-document analysis (large context windows); and a safety profile that is among the more conservative in the commercial field.

Anthropic publishes more research than some competitors and has made notable contributions to interpretability — the technical study of what is happening inside neural networks. The company's stated mission is the responsible development of AI for long-term benefit, and it frames safety research as central rather than adjunct to its work.

### 8.3 Gemini (Google DeepMind) {#gemini}

Google DeepMind emerged from the merger of Google Brain and DeepMind in 2023. Gemini is the product of this combined organisation, representing Google's frontier AI offering.

Google's AI lineage is substantial: the Transformer architecture itself came from Google Brain. BERT, which dominated NLP benchmarks for years, was a Google product. DeepMind produced AlphaGo, AlphaFold, and a string of technically significant research contributions.

The Gemini models are designed as natively multimodal from the ground up — trained on text, images, audio, and video simultaneously — rather than having modalities added to a text-based core. This is a claimed architectural advantage for tasks requiring reasoning across modalities.

Gemini Ultra (the largest Gemini model) showed competitive performance with GPT-4 on benchmarks at release. Google's competitive position is complicated by its dual role: it is both a frontier AI developer and a company whose core search advertising business may be threatened by AI-powered search alternatives.

### 8.4 DeepSeek {#deepseek}

DeepSeek is a Chinese AI laboratory that attracted significant international attention in early 2025 with the release of DeepSeek-R1 and DeepSeek-V3, models that showed frontier-level performance at a claimed fraction of the compute cost of comparable US models.

The technical contributions associated with DeepSeek include: mixture-of-experts architecture at scale (MoE — where only a subset of the model's parameters are active for any given input, reducing inference cost); aggressive efficiency optimisation in training; and a chain-of-thought reasoning approach for their R1 model similar in concept to OpenAI's o1.

DeepSeek's significance is both technical and geopolitical. The technical significance: demonstrating that frontier performance may be achievable with less compute than previously assumed challenges the premise that scale advantage alone is decisive. The geopolitical significance: the emergence of a Chinese laboratory producing models competitive with US frontier models, despite export restrictions on advanced semiconductors, raised substantial questions about the efficacy of those restrictions.

DeepSeek releases its models as open weights, making them downloadable and locally runnable — a contrast with OpenAI and Anthropic's closed approaches.

### 8.5 What They Have in Common {#commonalities}

Despite their differences, all major commercial AI systems share a common structure:

They are all large Transformer-based language models. The architectural differences are real but relatively incremental compared to the shared foundation.

They are all trained on enormous corpora of internet text plus curated datasets. The training data overlap is substantial.

They are all shaped by RLHF or equivalent preference-learning processes. The specific rater populations and rating criteria differ, but the basic mechanism is the same.

They all have safety and content policy layers that significantly shape their behaviour in deployment.

They all produce outputs that can be impressive, surprising, and useful alongside outputs that are confidently wrong, internally inconsistent, or subtly biased.

None of them have persistent memory across conversations by default. Each conversation begins with no knowledge of prior interactions.

None of them are "thinking" in real time in the way that phrase usually implies. Text generation is a forward pass through a very large neural network — fast, but not deliberative in the human sense.

---

## 9. What Current AI Cannot Do {#cannot-do}

It is as important to characterise limitations accurately as capabilities. The following are genuine, well-documented limitations of current AI systems, not speculative concerns.

**Reliable factual accuracy.** Language models generate plausible text. Plausible text is often accurate, because accuracy and plausibility correlate strongly in training data. But the model has no mechanism for verifying its outputs against ground truth before generating them. Confident, fluent, incorrect outputs — hallucinations — are a systematic feature of these systems, not a bug that will be easily fixed.

**Robust logical reasoning.** Performance on multi-step logical inference is highly variable. Models can solve some problems that appear to require complex reasoning and fail on simpler problems of the same type. The failure modes are often non-intuitive and do not resemble how humans fail at reasoning tasks.

**Genuine generalisation outside training distribution.** Models can struggle significantly with tasks that differ in form from what was common in training data, even when the underlying reasoning required is straightforward. Novel framings of familiar problems can cause surprising failures.

**Understanding vs. pattern matching.** Whether language models "understand" their inputs in any meaningful sense — whether they have semantic representations, not just syntactic patterns — remains genuinely contested in the research community. The practical consequence: models can produce outputs that appear semantically appropriate while failing on simple modifications that would be trivial for a system with genuine understanding.

**Persistent world models.** Current models do not maintain or update a model of the world across interactions. They have no concept of the passage of time, no ability to learn from experience in deployment, and no persistent beliefs. Each generation is computed from the current context window with no access to history outside that window.

**Causal reasoning.** Correlation is easier to learn from text than causation. Models often produce outputs consistent with known correlations that imply causal relationships — but whether the model has genuinely learned the underlying causal structure is typically unclear.

**Physical intuition.** Despite the existence of multimodal models, genuine understanding of physical dynamics — the kind of intuitive physics that even young children have — is not robustly present in current systems.

---

## 10. Terminology Reference: Words That Get Misused {#terminology}

A concise reference for the most commonly misused terms in public AI discourse.

**Thinking** — in ordinary use, implies deliberate, effortful cognitive processing. Current AI does not have an equivalent of this. Text generation is a forward pass, not deliberation. Models that do "chain-of-thought" generation are producing text that resembles reasoning, which often improves output quality, but the mechanism is not the same as human deliberative thought.

**Understanding** — implies semantic grasp, not just syntactic competence. Whether language models understand is technically unresolved. Using the word unreservedly is an overclaim.

**Knowing** — similar to understanding. A model "knows" Paris is the capital of France in the sense that its weights produce that output reliably. Whether this constitutes knowledge in any philosophically robust sense is contested.

**Believing** — implies a mental state that is held, updated, and used in inference. Models do not have persistent mental states. Using "believes" to describe a model's outputs is a metaphor, not a description of internal architecture.

**Intelligence** — see Section 2. Without specifying which of the multiple competencies you mean, the word is too vague to be useful.

**AGI (Artificial General Intelligence)** — a contested term with at least three common definitions: (1) performance at or above human level on all or most cognitive tasks; (2) general competence across diverse domains; (3) open-ended adaptive agency with self-modifying cognition. These definitions pick out different things and are achieved by different kinds of systems.

**Consciousness** — the most contested term in philosophy of mind. Whether any current AI system is conscious depends entirely on which theory of consciousness you accept, and there is no consensus. The honest answer to "is this AI conscious?" is "we do not know, and we disagree about what would constitute evidence."

**Learning** — in the ML sense, learning happens during training, not during deployment (with exceptions for systems with explicit memory or fine-tuning loops). A deployed model does not learn from conversations in real time. Using "learning" to describe a model appearing to adapt within a conversation (via context) is a metaphor.

**Hallucination** — the production of confident, fluent, incorrect outputs. A known and studied failure mode of language models, not a random error but a systematic one arising from how these systems generate text.

**Parameters / Weights** — the numerical values that encode everything a model learned during training. Often described as what the model "knows." More precisely: what patterns the optimisation process found useful for minimising the training loss.

---

## 11. Where This Study Goes From Here {#where-next}

This document has established the foundational concepts: what machine learning is, how neural networks work, what the Transformer architecture is and why it matters, how research models become commercial products, what the major commercial systems actually are, and what current AI genuinely cannot do.

The documents that follow in this study build directly on this foundation:

**Advanced Techniques: LoRA, RAG, and Emergent Behaviours** — a technical and conceptual examination of the approaches that are pushing AI systems beyond the static-weights LLM model toward more adaptive, persistent, and complex systems. This is where the architecture starts to get philosophically interesting.

**The AGI Question: Where the Boundary Actually Lives** — a serious examination of the AGI boundary problem, drawing on the conceptual tools from the EmergentEvolution founding conversation. The question is not "will we get AGI" but "what would it even mean to have gotten there."

**The Identity Problem in Adaptive Systems** — a deep examination of identity, continuity, and selfhood in systems that change over time, applied equally to biological and artificial cognitive systems. Based in part on the original founding conversation's analysis.

**Social Cognition and Relational Intelligence** — examination of the insight that intelligence may not be a property of systems but a property of interactions between systems. What this implies for how we study, build, and regulate AI.

**The Observation Problem: How Studying AI Changes AI** — on the recursive, self-referential nature of AI research, and why standard scientific methodology struggles with systems that are shaped by the act of studying them.

Each document stands alone but accumulates into a coherent study of what intelligence is, what current AI is and is not, and where the genuinely hard questions live. The goal of the whole is not to resolve these questions — they cannot currently be resolved — but to characterise them with precision.

---

*EmergentEvolution — Introduction.md*
*Document prepared as part of a structured study of artificial intelligence, emergence, and adaptive systems.*

---
