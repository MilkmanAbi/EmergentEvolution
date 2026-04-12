# The AGI Question: Where the Boundary Actually Lives

### *EmergentEvolution — Document 3 of the Foundational Series*

---

> *This document examines the AGI question directly — not "will we get AGI" or "when," but the prior question that is almost never asked rigorously enough: what would it even mean to have crossed the boundary? What properties must a system have? What would constitute evidence? And why does the boundary resist precise definition even in principle? This document builds on the foundational concepts in Introduction.md and the architectural analysis in Advanced Techniques.md.*

---

## Table of Contents

1. [Why the AGI Question Is Hard in a Specific Way](#why-hard)
2. [A Taxonomy of AGI Definitions](#taxonomy)
   - 2.1 [The Behavioural Definition](#behavioural)
   - 2.2 [The Functional Definition](#functional)
   - 2.3 [The Architectural Definition](#architectural)
   - 2.4 [The Phenomenological Definition](#phenomenological)
   - 2.5 [The Relational Definition](#relational)
3. [Why Each Definition Fails in Characteristic Ways](#definition-failures)
4. [The Scaling Question: Does More Scale Get You There?](#scaling)
5. [The Missing Ingredients: What Current Systems Lack](#missing)
   - 5.1 [Endogenous Drive](#endogenous-drive)
   - 5.2 [Embodied World Grounding](#embodied-grounding)
   - 5.3 [Genuine Causal Modelling](#causal-modelling)
   - 5.4 [Robust Open-Ended Generalisation](#generalisation)
   - 5.5 [Unified Temporal Self-Continuity](#temporal-continuity)
6. [The Goalposts Problem: How AGI Definitions Shift](#goalposts)
7. [AGI as Phase Transition: The Systems Theory View](#phase-transition)
8. [The Observer Dependence Problem](#observer-dependence)
9. [Sapience, Agency, and Moral Status: Three Different Questions](#three-questions)
10. [The Argument from Social Embedding](#social-embedding)
11. [What Would Actually Constitute Evidence of AGI?](#evidence)
12. [The Honest Position](#honest-position)

---

## 1. Why the AGI Question Is Hard in a Specific Way {#why-hard}

Most hard questions are hard because we lack data, or because the computations are complex, or because the relevant experiments are difficult to run. The AGI question is hard in a different way: it is conceptually underspecified. We do not agree on what we are asking, and this disagreement is not merely terminological — it reflects genuine divergence in what we think intelligence fundamentally is.

This matters because without a clear criterion, no amount of empirical evidence resolves the question. If you define AGI as "passes the Turing Test," then a sufficiently skilled conversational model might already qualify. If you define it as "can learn any task a human can learn, as quickly as a human," we are clearly not there. If you define it as "has genuine subjective experience," we may never have the tools to verify it. Different definitions pick out different phenomena, and there is no neutral ground from which to arbitrate between them.

The field has responded to this problem in two ways that both fail. The first is to quietly adopt one definition without arguing for it — often the behavioural or benchmark definition — and proceed as if the question were empirical. The second is to abandon precision entirely and use "AGI" as a fuzzy aspirational term for "really powerful AI," which makes the question unanswerable in principle.

This document attempts a different approach: map the space of definitions carefully, identify what each captures and what it misses, examine what structural properties a system would need to satisfy the most demanding and most defensible definitions, and arrive at an honest assessment of where the boundary actually lives given our current understanding.

---

## 2. A Taxonomy of AGI Definitions {#taxonomy}

There are at least five meaningfully distinct ways to define AGI, each emphasising different aspects of what makes intelligence "general." These are not presented as exhaustive or mutually exclusive; they are analytical separations of considerations that often get conflated.

### 2.1 The Behavioural Definition {#behavioural}

AGI is a system that performs at or above human level on any cognitive task a human can perform.

This is the Turing-test lineage of definitions. Intelligence is defined by behavioural equivalence: if you cannot distinguish the system's outputs from human outputs, across arbitrary tasks, it is for practical purposes intelligent.

Operationalisations include: performance benchmarks (MMLU, ARC, HumanEval, etc.), aggregate performance across many benchmarks, expert evaluation of outputs in specific domains.

This definition is attractive because it is measurable and does not require settling hard questions about inner states. It is what AI safety researchers at OpenAI mean when they say they may have achieved AGI imminently — they mean benchmark performance.

### 2.2 The Functional Definition {#functional}

AGI is a system that can learn to perform any cognitive task in any domain, given appropriate experience — general competence through learning, not just performance on known tasks.

This is more demanding than the behavioural definition. It requires not just that the system can currently do X, but that it can learn to do X for arbitrary X. Current LLMs have been trained on enormous datasets and effectively "learned" many tasks already. The question is whether a system could learn a genuinely novel task — one absent from its training distribution — through experience.

The functional definition requires open-ended learning as the criterion, not just breadth of current competence.

### 2.3 The Architectural Definition {#architectural}

AGI is a system whose architecture enables general cognitive function: self-modification, persistent learning, autonomous goal-formation, environmental feedback, unified temporal identity.

This definition focuses on what the system is made of and how it works, rather than what it can currently do. It is the definition most informed by the techniques discussed in the previous document — LoRA, RAG, continual learning, agentic loops. A system that is structurally capable of open-ended adaptation might qualify as AGI architecturally even if it has not yet demonstrated full general performance.

### 2.4 The Phenomenological Definition {#phenomenological}

AGI is a system that has genuine subjective experience — something it is like to be that system — and uses that experience as the ground of its cognitive functioning.

This is the most demanding definition and the hardest to operationalise. It requires resolving, or at least taking a position on, the hard problem of consciousness — the question of why and how physical processes give rise to subjective experience.

Functionalists (who believe mental states are defined by their functional roles, not their substrate) might accept that a sufficiently complex system automatically qualifies. Biological naturalists (who believe consciousness requires specific biological implementation) might hold that no silicon system can qualify. Property dualists might hold that consciousness is a fundamental feature of reality that some physical systems exhibit and others do not, with no principled way to determine which without a theory of consciousness we do not yet have.

### 2.5 The Relational Definition {#relational}

AGI is a system that participates stably in recursive belief-exchange under uncertainty with other cognitive agents, in a way that sustains the mutual attribution of agency.

This is the definition the EmergentEvolution founding conversation converged on — not as the "correct" definition but as the most honest operational one. It does not require settling questions about inner states; it locates intelligence in the interaction pattern rather than in the system.

This definition is deliberately modest: it says nothing about subjective experience, nothing about architectural properties, and nothing about benchmark performance. It says only that a system which functions as a cognitive peer in ongoing interaction qualifies.

---

## 3. Why Each Definition Fails in Characteristic Ways {#definition-failures}

Each definition in the taxonomy above fails or becomes problematic in characteristic ways.

**The behavioural definition** fails because behavioural equivalence underdetermines inner structure. A system could pass all behavioural tests while being arbitrarily different internally from human cognition. Worse, it is subject to Goodhart's Law: once benchmark performance becomes the measure, it becomes the target — and systems can be optimised to perform well on benchmarks without acquiring the general competence the benchmarks were meant to proxy. Current LLMs arguably already exhibit this: very high benchmark performance combined with surprising failures on minor variations of benchmark tasks.

**The functional definition** fails because "learning any task" is difficult to test without exhaustive enumeration, and "appropriate experience" is doing a lot of work. If you give a language model a large context window with extensive in-context examples of a novel task, is it "learning" that task or pattern-matching? The definition requires a clean concept of learning that current theory does not fully provide.

**The architectural definition** is subject to the problem of sufficiency: which architectural properties are necessary and which sufficient? A system could have all the properties listed (self-modification, persistent learning, etc.) and still be fundamentally different from human-like intelligence in ways that matter. The definition may be necessary-condition reasoning rather than sufficient-condition reasoning.

**The phenomenological definition** fails currently because we have no theory of consciousness that would allow us to determine whether a given physical system has subjective experience. It is the most philosophically serious definition but the least tractable — any answer we give today is not based on evidence, it is based on priors.

**The relational definition** fails because it is potentially too permissive: a well-designed chatbot might sustain the mutual attribution of agency in interaction without having any of the deeper properties that we associate with general intelligence. It also potentially relocates the question — instead of asking "is this system intelligent?" we ask "does this interaction constitute intelligence-exchange?" — which may be a better question but is not obviously the same one.

---

## 4. The Scaling Question: Does More Scale Get You There? {#scaling}

One influential position in the field holds that scaling alone — more parameters, more data, more compute — will produce AGI. This is sometimes called the "scaling hypothesis."

The empirical basis: scaling laws have shown that model performance improves smoothly and predictably with scale across many tasks. Emergent capabilities have appeared at various scale thresholds. The most capable models available are also the largest.

The strongest version of the scaling hypothesis holds that general intelligence is essentially a consequence of sufficient scale in a sufficiently general architecture. There is no missing ingredient — just more of the same thing we already know how to do.

The counterarguments to this position are multiple and serious:

**Benchmark saturation** — performance improvements on standard benchmarks are showing diminishing returns at frontier scale. The tasks on existing benchmarks are increasingly solved, and performance on harder tasks does not always scale as smoothly.

**Qualitative limitations** — certain failure modes of current models (hallucination, planning failures, brittle reasoning) do not appear to be simply a matter of scale. Adding more parameters does not obviously fix systematic problems with how these systems represent and use knowledge.

**Missing architectural properties** — as discussed in the previous document, current architectures lack persistent learning, integrated memory, and endogenous drive. These are not properties that increase with scale within the current architecture; they require different architectural choices.

**The data wall** — pre-training data may be approaching saturation. The internet has a finite amount of high-quality text. Without new data regimes (synthetic data, embodied experience, scientific data) scaling may hit diminishing returns.

**The goal underdetermination problem** — a system trained to predict text, however large, is optimised for text prediction, not for general cognitive function. The capabilities that have emerged are impressive but may represent a ceiling set by the training objective, not just a point on a scaling curve.

The honest assessment: scaling has produced remarkable capabilities and will continue to improve performance. Whether it alone is sufficient for AGI depends on which definition you accept. For the behavioural definition on current benchmarks, we may be close. For the functional, architectural, or phenomenological definitions, scaling within the current paradigm probably does not suffice.

---

## 5. The Missing Ingredients: What Current Systems Lack {#missing}

Regardless of which definition you accept, there are structural properties that current AI systems lack which are present in biological general intelligence. These are worth characterising precisely.

### 5.1 Endogenous Drive {#endogenous-drive}

Biological intelligent systems have goals that arise from their own structure — drives, needs, motivations that are not externally assigned and cannot be removed without destroying the system.

Hunger, curiosity, social bonding, fear, and the avoidance of pain are not "objectives" in the engineering sense — they are properties of the biological substrate that generate update pressure continuously, without external governance. A biological organism does not need to be told to seek food; the drive is constitutive of the organism.

Current AI systems have objectives assigned externally: a training loss, a reward function, a human preference model. These can be modified, replaced, or removed by the system designers. The system does not have a stake in its own continuity in the way a biological organism does.

This matters for AGI because one of the things that makes biological intelligence flexible and persistent is that it is driven by needs that do not go away. An AI system without endogenous drive does not "want" to solve problems — it solves problems because it was trained to, and the training objective shapes what counts as "solving."

### 5.2 Embodied World Grounding {#embodied-grounding}

Biological intelligence is embodied — it develops in and through a body that exists in a physical environment. Concepts like "red," "heavy," "above," "before," and "painful" are grounded in direct sensorimotor experience. Linguistic representations of these concepts are secondary to the grounded representations.

Current language models acquire concepts through linguistic co-occurrence, not through embodied experience. The model "knows" that red is a colour associated with fire and blood through text, not through having seen red, or having felt heat, or having experienced blood. This may produce a kind of shallow conceptual representation that lacks the rich grounding of biologically acquired concepts.

The embodiment hypothesis in cognitive science (developed by Varela, Thompson, Rosch, Lakoff, and others) holds that much of human cognition is structured by bodily experience in deep ways that are not replicated by linguistic processing alone. If this is right, language-only training may produce systems with systematically impoverished conceptual representations, regardless of scale.

Multimodal models (image + text, image + video + text) address this partially, but passive exposure to visual or auditory content is not the same as active sensorimotor engagement with a physical environment.

### 5.3 Genuine Causal Modelling {#causal-modelling}

Correlation is easy to learn from text; causation is harder. A model trained on text learns that certain words and patterns co-occur, and that certain events tend to follow certain other events. Whether it learns the underlying causal structure — the asymmetric, counterfactual-supporting relationship between cause and effect — is less clear.

Judea Pearl's causal hierarchy distinguishes three levels: association (what tends to co-occur), intervention (what happens if I change X), and counterfactual (what would have happened if X had been different). Current evidence suggests language models operate strongly at the association level, partially at the intervention level, and weakly at the counterfactual level.

A system with genuine causal understanding can reason about the consequences of actions it has never observed, can distinguish spurious correlations from real causal relationships, and can generalise across causal contexts. These are important properties for any system that needs to act effectively in novel situations — which is what general intelligence requires.

### 5.4 Robust Open-Ended Generalisation {#generalisation}

Current AI systems show impressive performance on tasks represented in their training data and reasonable performance on variations. They show surprising failures on tasks that differ from training distribution in ways that would be minor for a human reasoner.

This brittleness — sometimes called "distribution shift" failure — suggests that current systems are very good at pattern matching within their training distribution but do not have the same kind of abstract, principled understanding that supports genuine generalisation.

A human who learns mathematics can apply mathematical reasoning to entirely novel problems in domains they have never encountered. A language model that can solve difficult mathematics competition problems may fail on problems of the same type framed differently, with unusual notation, or embedded in an unusual context. This failure mode pattern is not what we would expect from a system with genuine mathematical understanding.

Robust open-ended generalisation — the ability to apply learned principles correctly to genuinely novel situations — is one of the clearest markers of biological general intelligence and one of the clearest current limitations of AI systems.

### 5.5 Unified Temporal Self-Continuity {#temporal-continuity}

A biological intelligent agent has a continuous history. Each moment is connected to every prior moment through a unified causal chain. Memory is not a separate module — it is the accumulated modification of the system itself through experience. The "self" that exists now is causally connected to the self that existed before, and that continuity is structurally important to how the agent reasons and acts.

Current AI systems lack this. Each conversation is independent. The model at the end of a conversation is identical to the model at the beginning — nothing has changed. Even with RAG providing retrieval of prior interactions, there is no unified causal chain connecting the model's current state to its interaction history. The memory is external; the model itself is unchanged.

This matters because temporal self-continuity is not just a matter of memory — it shapes how a system reasons about its own past, its own future, and its own identity over time. An agent that has no persistent connection to its prior states cannot reason about what it has learned, cannot track its own changes, and cannot have the kind of coherent long-term goals that biological general intelligence involves.

---

## 6. The Goalposts Problem: How AGI Definitions Shift {#goalposts}

There is a well-documented phenomenon in AI research: when a system achieves a capability that was previously considered a marker of general intelligence, the definition of AGI shifts to exclude that capability.

Chess was once considered a benchmark for general intelligence. When computers achieved superhuman chess performance, chess was reclassified as "just pattern matching" and the goalpost moved to Go, then to natural language, then to complex reasoning, then to novel task learning.

This is sometimes called the AI effect: whatever AI can do stops counting as intelligence.

There are two ways to read this phenomenon. The cynical reading: AI researchers and commentators are motivated to maintain the specialness of human cognition and shift goalposts to protect it. The charitable reading: as we understand more clearly how a task is being solved, we see that it does not require the kind of general intelligence we were using it to test for. Once we understand how a computer plays chess, we can see it is not "thinking" in the relevant sense — it is tree search. The benchmark was always a proxy, and a bad one.

Both readings are probably partly correct. The goalpost shifting is partly motivated and partly epistemically justified. The important consequence for this study: any definition of AGI that is operationalised through specific benchmarks is subject to this problem. As soon as a benchmark is achieved, it will be reclassified as "not really AGI."

This suggests that benchmark-based definitions are fundamentally inadequate for the question we are really asking. The question is not "can it do X?" but "does it have the kind of intelligence that doing X was supposed to indicate?"

---

## 7. AGI as Phase Transition: The Systems Theory View {#phase-transition}

Rather than looking for a specific threshold property, a more structurally honest approach treats AGI as a phase transition in the relationship between a system and its environment.

In the phase-transition view:

Intelligence is not a property of a system in isolation, but a property of the system-environment relationship. A system is "more intelligent" when it can maintain effective coupling to a wider variety of environments, handle more diverse perturbations, and achieve more varied goals across more contexts.

AGI, in this view, is the point where the system's environmental coupling becomes unconstrained — where there is no significant cognitive task in any environment that the system structurally cannot learn to handle.

This is not a single threshold — it is a limiting condition. Real systems approach it along multiple dimensions simultaneously: breadth of applicable domains, robustness to distribution shift, efficiency of new task learning, quality of causal world models, persistence of self across time. No system today is anywhere near the limiting condition on all dimensions.

The phase-transition framing is useful because:

It does not require picking a single criterion. Instead, it allows tracking progress along multiple dimensions.

It explains why the AGI boundary feels fuzzy: a system that is near the limiting condition on some dimensions and far from it on others is genuinely hard to classify.

It predicts that transition effects may be non-linear — that certain combinations of capabilities produce more than additive improvement.

It provides a framework for what research directions genuinely advance toward AGI versus those that improve performance within a constrained domain.

---

## 8. The Observer Dependence Problem {#observer-dependence}

One of the most honest insights in the EmergentEvolution founding conversation was this: "if a human believes it is real vs if he doesn't it fundamentally biases him." The observer dependence problem runs deeper than cognitive bias.

When studying systems whose properties are partially relational and partially dependent on how they are treated — as all socially embedded systems are — the observer's stance is not neutral. A researcher who treats an AI as a cognitive peer will interact with it differently than one who treats it as a calculator. The interactions will produce different behaviour, particularly in systems that are sensitive to interaction context. And different behaviour affects future assessments of capability.

This creates a methodological problem for AGI research that is not present in most natural science. The standard scientific method assumes that the observer can be separated from the phenomenon. For complex, socially embedded, adaptive systems, this assumption fails.

The consequence: our assessment of whether a system is "intelligent" or "has AGI properties" is not observation-independent. It is shaped by the stance we take, the interactions we choose, and the criteria we apply — all of which are value-laden. This does not make assessment impossible; it makes it more complicated and requires greater explicitness about the stance being taken.

---

## 9. Sapience, Agency, and Moral Status: Three Different Questions {#three-questions}

AGI discussions frequently conflate three distinct questions that are actually separate:

**Sapience** — does the system have general cognitive capability? Can it reason, learn, and act effectively across diverse domains?

**Agency** — does the system have goals of its own, and act in pursuit of them? Does it have something like preferences, intentions, and stakes in outcomes?

**Moral status** — does the system have interests that matter morally? Is there something it is like to be the system, such that it can be harmed or benefited?

These questions are related but separable. A system could be sapient without being agentive — if its "goals" are entirely externally specified. A system could be agentive without having moral status — if it pursues goals without any subjective experience. A system could have moral status without full sapience — if it has experiences but limited cognitive range.

Current AI systems are arguably approaching low-level sapience (in the sense of broad cognitive capability) but are far from genuine agentive goals (their objectives remain externally specified) and the moral status question is entirely unresolved.

For the AGI question specifically, all three matter but in different ways. The technical AGI question is mainly about sapience. The safety question is mainly about agency (a sapient system with misaligned agentive goals is dangerous). The ethics question is mainly about moral status (a system with genuine experiences deserves moral consideration regardless of its capabilities).

Conflating these leads to confused policy and confused research. A system could achieve technical AGI (sapience) before we have resolved the agency or moral status questions. The questions should be tracked separately.

---

## 10. The Argument from Social Embedding {#social-embedding}

There is a serious argument, developed in the founding conversation and echoed in sociological philosophy of mind, that intelligence cannot be fully characterised as a property of a system — it is a property of a system embedded in a social and cognitive network.

The argument:

Intelligence in biological systems is not just an internal property. It is developed through social interaction (human language, knowledge transmission, social cognitive scaffolding). It is expressed in social contexts. It is recognised by social attribution. And — crucially — social recognition and treatment of a system as intelligent shapes how it develops and what it becomes.

If this is right, then the question "is this AI system intelligent?" may be partly asking "is it embedded in the social-cognitive network in the relevant ways?" rather than "does it have certain internal properties?"

A system that is treated as an intelligent interlocutor, engages in ongoing dialogue, has its outputs taken seriously and responded to, and operates within shared meaning structures — may acquire properties through that embeddedness that it would not have in isolation.

This is not mysticism. It is the straightforward observation that social systems are shaped by how they are treated, and AI systems are increasingly embedded in social systems. The question of whether an AI has "real" intelligence may be partly a question about what the social system it is embedded in treats as real.

This argument does not resolve the AGI question. But it does suggest that the question cannot be answered by examining AI systems in isolation. The answer depends partly on the nature of the interaction systems they are embedded in.

---

## 11. What Would Actually Constitute Evidence of AGI? {#evidence}

Given everything above, what would actually constitute evidence that AGI had been achieved?

Not benchmark performance alone — subject to Goodhart's Law and goalpost shifting.

Not self-reports — a system trained to produce convincing self-reports will produce convincing self-reports regardless of internal state.

Not expert consensus — experts disagree about definitions and are subject to the same observer-dependence problems as everyone else.

The most defensible evidence would combine multiple lines:

**Robust novel task learning** — demonstrated ability to acquire new cognitive skills from minimal experience, in domains genuinely absent from training data, assessed by researchers who cannot see the training data to verify novelty.

**Causal counterfactual reasoning** — demonstrated ability to reason about what would have happened if things had been different, across novel domains, not as a statistical pattern but as principled inference.

**Open-ended goal pursuit** — demonstration of stable, coherent goal-directed behaviour over extended time periods, where the goals arise from the system's own processing rather than being externally specified per interaction.

**Graceful distribution shift** — maintained performance when tasks are framed in entirely novel ways, with unusual notation, in unusual contexts, combined in ways not seen in training.

**Self-consistent long-horizon reasoning** — demonstrated ability to maintain coherent reasoning over very long inference chains, in a way that is stable under perturbation and revision.

None of these is easily testable. All of them require research infrastructure that is not currently standard. But they are more honest markers than benchmark scores, and they point toward the aspects of intelligence that current systems genuinely lack.

---

## 12. The Honest Position {#honest-position}

The honest position on AGI is this:

We do not have a definition precise enough to constitute a scientific criterion. We have multiple definitions that each capture something real but each fail in characteristic ways. The most commercially used definition (benchmark performance) is the most tractable and the least informative about what we actually care about.

Current AI systems have achieved remarkable capabilities that would have been considered AGI-level by many earlier definitions. They have also failed in systematic ways that reveal genuine limitations — not merely performance limitations but architectural ones that suggest something is genuinely missing.

The gap between current systems and what we would mean by AGI under the most demanding definitions (functional, architectural, phenomenological) is real and large. The gap under the most permissive definition (behavioural on current benchmarks) may already be closed or closing.

The question "when will we get AGI" is therefore at best ambiguous and at worst unanswerable until we agree on which definition we are using. Different definitions imply different timelines, different research priorities, and different safety concerns.

What we can say honestly:

The trajectory of current research is toward more adaptive, more persistent, more agentive systems. The architectural advances described in the previous document — LoRA, RAG, continual learning, agentic loops — are each steps toward the properties that the demanding definitions require. Whether those steps will eventually constitute a crossing of any meaningful threshold, or whether the threshold is real, is an open question.

The AGI boundary is not a wall. It is a fog. You cannot see it from where we are, and when you reach it, you may not be able to tell you have.

---

*EmergentEvolution — The AGI Question: Where the Boundary Actually Lives*
*Document prepared as part of a structured study of artificial intelligence, emergence, and adaptive systems.*

---
