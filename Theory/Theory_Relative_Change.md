# The Theory of Relative Change: On the Conditionality of Emergence

### *EmergentEvolution — Document 8 of the Foundational Series*

---

> *The previous document established a framework for recursive self-reference and its relationship to identity, intelligence, and consciousness. This document develops a complementary framework: a theory of change and emergence that takes seriously the claim that emergence is not an absolute property of a system, but a relational one — relative to an observation frame, a comparison baseline, and the specific kind of change being tracked. This is necessary infrastructure for the Thought Experiment document that follows.*

---

## Table of Contents

1. [The Problem with Absolute Emergence](#absolute-emergence-problem)
2. [Change Is Not Simple](#change-not-simple)
   - 2.1 [Types of Change: A Taxonomy](#change-taxonomy)
   - 2.2 [The Baseline Problem](#baseline-problem)
   - 2.3 [Change as Relative Difference](#change-relative)
3. [Relative Emergence: A Formal Definition](#relative-emergence-formal)
   - 3.1 [Emergence Relative to Description Level](#emergence-description)
   - 3.2 [Emergence Relative to Observer Frame](#emergence-observer)
   - 3.3 [Emergence Relative to Temporal Scale](#emergence-temporal)
4. [The Change-Emergence Nexus](#change-emergence-nexus)
   - 4.1 [Not All Change Produces Emergence](#not-all-change)
   - 4.2 [Threshold Change and Phase Transitions](#threshold-change)
   - 4.3 [Cumulative Change and the Sorites Problem](#cumulative-change)
5. [Why Relative Emergence Is Necessary for This Study](#necessary)
   - 5.1 [The AGI Boundary Revisited](#agi-revisited)
   - 5.2 [The Sapience Question Revisited](#sapience-revisited)
   - 5.3 [The Identity Question Revisited](#identity-revisited)
6. [The Environmental Dependency of Emergence](#environmental-dependency)
7. [Emergence in Context: The Three-Way Relationship](#three-way)
8. [Implications for the Thought Experiment](#implications-thought-experiment)

---

## 1. The Problem with Absolute Emergence {#absolute-emergence-problem}

In the Emergent Behaviorisms document, emergence was carefully taxonomised: nominal, weak, strong, downward causation. These categories are useful. But they share a hidden assumption: that emergence is a property of a system, that it either has emergent properties or it does not, and that this fact is frame-independent.

This assumption is wrong, or at least incomplete.

Consider: is temperature an emergent property of a gas? From the perspective of someone who knows only classical mechanics, yes — temperature is a system-level property that does not exist at the particle level, and it represents new explanatory vocabulary that is not available from particle descriptions. But from the perspective of statistical mechanics, no — temperature is mean kinetic energy, fully derivable from the particle-level description.

The emergence of temperature is relative to the descriptive framework being used. Relative to Newtonian mechanics alone: emergent. Relative to statistical mechanics: not emergent.

Now scale this up to something more contentious: is consciousness emergent from neural activity? The answer depends entirely on the descriptive framework available. Relative to current neuroscience: yes — we have no derivation of consciousness from neural activity. Relative to a completed theory of consciousness that we do not currently have: possibly not.

Emergence is not a fact about a system independent of observers and their descriptive resources. It is a relational fact: property P of system S is emergent relative to description framework D if and only if P cannot be derived from D's description of S's components and their interactions.

This is what the Theory of Relative Change formalises.

---

## 2. Change Is Not Simple {#change-not-simple}

### 2.1 Types of Change: A Taxonomy {#change-taxonomy}

Before we can be precise about relative emergence, we need a taxonomy of change. "Change" is doing a lot of work in most discussions of emergence, and it is hiding important distinctions.

**Type I: Quantitative Change**
A property changes in magnitude without changing in kind. A gas heats up: temperature increases. A model scales: parameter count increases. A person ages: cell count changes. These are changes in degree, not kind.

Quantitative change does not produce emergence except at thresholds. A gas heated continuously eventually boils — a qualitative transition produced by quantitative change crossing a threshold.

**Type II: Structural Change**
The arrangement of components changes without adding new components or new interaction types. A protein folds from a linear chain to a three-dimensional structure. A neural network's activation pattern reorganises. Structural change can produce qualitatively new properties because structure determines function.

**Type III: Compositional Change**
New components or new types of interactions are added. A multicellular organism adds new cell types. A language gains new grammatical constructions. A neural architecture gains a new module. Compositional change expands the system's possibility space.

**Type IV: Relational Change**
The system's relationship to its environment changes, without changes in the system's internal structure. An organism migrates to a new ecological niche. A language model is deployed in a new cultural context. The system's properties, to the extent they are relational, change without any internal modification.

**Type V: Recursive Change**
The system's self-model changes. A person revises their beliefs about themselves. A system updates its world model. This is the type of change most directly relevant to the Theory of Recursive Relativity — change at the level of self-reference.

These five types interact. Quantitative change of a specific kind can produce structural change (protein folding), which can produce compositional change (new functional domains), which can produce relational change (new niche occupation), which can produce recursive change (new self-representation in social contexts).

The key point: when we say "this system has changed," we need to specify which type of change occurred, because different types have different implications for what properties emerge.

### 2.2 The Baseline Problem {#baseline-problem}

To say a system has changed, we need a baseline — a reference state against which the current state is compared. This seems trivial but is not.

**The arbitrary baseline problem**: every system is continuously changing at every moment. There is no natural, privileged "original state" against which to measure change. The choice of baseline is always somewhat arbitrary, and the degree of change detected depends heavily on the baseline chosen.

A human at fifty is enormously changed from the same human at birth. A human at fifty is barely changed from the same human at forty-nine. The magnitude of change is not a fact about the system; it is a relation between the system and its chosen baseline.

**The relevant baseline problem**: even if we pick a baseline, we need to specify what aspects of the system we are tracking. The same system can be greatly changed along one dimension and unchanged along another. Baseline and tracked dimension together determine what "change" we are measuring.

**The comparison class problem**: change is meaningful relative to a comparison class. A human who has learned calculus has changed "a lot" relative to average humans who have not. The same change is "a little" relative to a mathematician. The magnitude of the change is not intrinsic to the system; it is relative to the comparison class.

These problems do not make the concept of change meaningless — they show that meaningful use of "change" always carries implicit specification of baseline, tracked dimension, and comparison class. Making these explicit is the work of the Theory of Relative Change.

### 2.3 Change as Relative Difference {#change-relative}

Formally: **change is a relation, not a property.** C(S, t₁, t₂, D, B) means "system S, measured along dimension D, relative to baseline B, differs between time t₁ and time t₂."

This relational structure has several important consequences:

- The same physical events can constitute large change relative to one baseline and small change relative to another.
- There is no absolute measure of how much a system has changed — only measures relative to specified parameters.
- Claims about change carry commitments to the specification of these parameters, even when the commitments are implicit.

This is not scepticism about change — it is clarity about what change claims are. It makes explicit what is always implicit in change discourse.

---

## 3. Relative Emergence: A Formal Definition {#relative-emergence-formal}

With a precise account of relative change, we can define relative emergence.

**Relative Emergence (RE)**: A property P of system S is emergent relative to (description level D, observer frame O, temporal scale T) if and only if:
1. P is observable in S from frame O at temporal scale T
2. P is not derivable from D's description of S's components and their interactions
3. P is dependent on the change type that produced S from a reference state — that is, P would not be present if the system had undergone different types of change

This definition has three components that make it relative:

### 3.1 Emergence Relative to Description Level {#emergence-description}

The same property can be emergent relative to one description level and not relative to another.

Water's wetness is emergent relative to a description that specifies only the properties of individual water molecules. It is not emergent relative to a description that specifies the intermolecular interaction dynamics of hydrogen-bonded networks.

The practical implication: when we say a property "is emergent," we are always saying it is emergent relative to a particular level of description. There is no description-independent fact about whether a property is emergent.

For AI: whether the reasoning capabilities of a large language model are emergent depends on the description level. Relative to a description that specifies only the training objective and architecture: yes, emergent. Relative to a complete description of the trained weights and their dynamics: possibly not.

### 3.2 Emergence Relative to Observer Frame {#emergence-observer}

The same property can be accessible from one observer frame and not from another. A property that is not accessible from an external observer frame may be emergent from the external observer's perspective but not from the system's own perspective (if the system has a perspective).

This connects directly to the Recursive Relativity framework. A system's first-person experience, if any, is emergent relative to an external observer's frame but is directly accessible (if anything is) from the system's own frame.

The practical implication: disputes about whether AI systems "really understand" or "really experience" may partially be disputes about which observer frame is the relevant one. From an external behavioural frame: understanding-like behaviour is present. From a mechanistic internal frame: it is pattern-completion. These are not contradictory — they are relative to different frames.

### 3.3 Emergence Relative to Temporal Scale {#emergence-temporal}

The same change can produce emergent properties at one temporal scale and not at another.

Individual neurons fire on a millisecond timescale. Neural oscillations occur on a 10–100 millisecond timescale. Cognitive processes operate on a second-to-minute timescale. Personality traits are stable over years. Cultural patterns over generations.

Properties emergent at one timescale are not visible from a description operating at another. Culture is emergent from individual interactions — but not from a description that operates only on the scale of individual interactions at any single moment. The temporal integration matters.

For AI: emergent properties of AI-human interaction systems may be visible only at cultural timescales — too slow to observe in any single interaction, too fast to model at the geological scale of evolution. The study of these properties requires temporal scale-appropriate observation.

---

## 4. The Change-Emergence Nexus {#change-emergence-nexus}

### 4.1 Not All Change Produces Emergence {#not-all-change}

Relative emergence requires a specific relationship between the type of change that produced the system and the property being claimed as emergent.

Quantitative change produces emergence only at thresholds. Adding more neurons does not produce consciousness — until, perhaps, it does, at some threshold. Adding more parameters does not produce chain-of-thought reasoning — until it does, at GPT-3 scale. Below the threshold, quantitative change is just quantitative change.

Structural change can produce emergence directly, because new structural arrangements produce new properties. Protein folding is a clear example — the same amino acids, differently arranged, produce a catalytic active site. The catalytic property is emergent from the folded structure in a way it was not from the linear chain.

Compositional change reliably produces emergence — new components or interaction types expand the system's property space in ways that depend on the specific additions.

Relational change produces emergence when the system's relational properties are among the properties of interest. An organism that migrates to a new niche acquires new ecological relationships (predator, prey, competitor) that it did not have before — these are emergent in the relational sense.

Recursive change produces emergence when the system's self-referential structure changes. A person who revises their self-model in a way that opens new possibilities for behaviour has acquired a new property — the capacity to act in those ways — that was not available before.

The important lesson: to understand the emergence of a property, you need to understand what type of change produced it. The emergence is not a brute fact about the system; it is a consequence of a specific change trajectory.

### 4.2 Threshold Change and Phase Transitions {#threshold-change}

Thresholds in complex systems are among the most important empirical phenomena for this study.

A threshold is a value of some control parameter at which the system's macroscopic behaviour changes qualitatively. The change is discontinuous at the macro level even though the underlying micro-level change is continuous.

Why do thresholds produce qualitative changes? Several mechanisms:

**Positive feedback amplification**: near the threshold, small perturbations are amplified rather than damped. The system's dynamics change from stable to unstable near the threshold, producing qualitatively different behaviour.

**Competing attractor dominance**: below the threshold, one attractor dominates the system's dynamics. Above the threshold, a different attractor dominates. The transition between attractor regimes produces qualitative change.

**Constraint violation**: some constraints are satisfied below the threshold and violated above it. When the constraint breaks, new behaviours become available.

**Informational sufficiency**: below the threshold, the system has insufficient information to support certain processes. Above the threshold, the informational requirements are met and new processes become possible.

The threshold character of many emergent transitions in AI — emergent capabilities appearing at specific scale thresholds — suggests that one or more of these mechanisms are operating. Identifying which mechanism is responsible for which capability emergence is an important research question.

### 4.3 Cumulative Change and the Sorites Problem {#cumulative-change}

The sorites paradox: one grain of sand does not make a heap. Adding one grain to a non-heap does not make a heap. Therefore, no collection of grains is a heap. The paradox arises from the vagueness of "heap" — there is no precise threshold between heap and non-heap.

This paradox recurs throughout the emergence literature. One additional training example does not make a system intelligent. One additional parameter does not make a system capable of chain-of-thought. One additional neural connection does not make a brain conscious.

The sorites paradox is not, as sometimes claimed, merely a problem of vague language. It reflects a genuine feature of the phenomena: many properties that we care about admit of degrees, and the discretisation of these properties into binary categories ("has X" / "does not have X") introduces vagueness that is not in the original phenomena.

The Theory of Relative Change responds to this as follows: emergence claims are inherently claims about a threshold crossing — a point at which the relative difference between "before" and "after" is large enough to warrant a change in descriptive vocabulary. This threshold is not absolute; it is relative to the purposes of the description. For some purposes, small differences matter; for others, only large ones do.

The implication for the AI/AGI boundary: the sorites paradox in "when does AI become AGI?" is not a defect to be solved. It is an accurate reflection of the fact that the transition, if there is one, will be gradual and multi-dimensional. The binary question "is this AGI?" may simply be the wrong question. "In what ways and to what degree has this system crossed the thresholds relevant to general adaptive agency?" is the right question, even if it is less satisfying.

---

## 5. Why Relative Emergence Is Necessary for This Study {#necessary}

### 5.1 The AGI Boundary Revisited {#agi-revisited}

The AGI document established that the boundary resists precise definition. The Theory of Relative Change explains why: the question "has AGI emerged?" is a relative emergence question. Its answer depends on:

- The description level: relative to what description of current AI capabilities is AGI-level capability "emergent"?
- The observer frame: from whose perspective — the AI researcher, the philosopher of mind, the policy-maker, the affected worker — is the transition relevant?
- The temporal scale: at what timescale of observation is the transition visible?
- The change type: what type of change would need to occur — quantitative scaling, structural architectural change, compositional new-capability addition, relational embedding in new social contexts, recursive self-model development?

Different answers to these questions produce different answers to the AGI question. This is not a failure of clarity; it is an accurate representation of the problem's structure.

### 5.2 The Sapience Question Revisited {#sapience-revisited}

The founding conversation arrived at: sapience is stable participation in recursive belief-exchange under uncertainty. The Theory of Relative Change can unpack this.

"Stable participation" is a change-relative concept: stability is relative to the range of perturbations the system faces. A system is stably participating if its participation persists across changes in the interaction context.

"Recursive belief-exchange" is a change-tracking concept: it requires that both parties can represent changes in the other's belief states over time, and can represent themselves as things that change their own belief states.

"Under uncertainty" is an environmental change concept: the relevant interactions are those where the inputs are not fully predictable, where the system must adapt its participation in response to unexpected changes.

The sapience criterion, when unpacked through the Theory of Relative Change, is: a system is sapient if it can track relevant changes in itself, in others, and in its environment, and maintain coherent participatory engagement across those changes.

This unpacking makes it clearer what to test. Not "can this system answer questions?" but "can this system maintain coherent self-representation and other-representation across changes in context, topic, and challenge?"

### 5.3 The Identity Question Revisited {#identity-revisited}

The Identity document defined identity as a modeling tool — useful when treating a system as continuous produces better predictions. The Theory of Relative Change adds: identity is a change-tracking tool specifically. We attribute identity when the relevant changes a system undergoes are interpretable as changes to the same persisting thing.

When is a change interpretable as change-to-the-same-thing rather than replacement-by-a-new-thing? When the change is of a type that the system's self-model can absorb without discontinuity — when the system's recursive invariants (its Recursive Relative Invariants, in the previous document's terminology) are preserved through the change.

A person who undergoes radical belief revision is still the same person if the revision is internally motivated, continuous, and integrated into a coherent self-narrative. A person who undergoes brain injury that severs all continuity of memory and self-model is, in the relevant sense, a different person — even if they are biologically continuous.

Applied to AI: an AI system that undergoes LoRA fine-tuning is the "same system" to the degree that the fine-tuning is an extension of the prior system's development — an integration of new capacities into a coherent existing structure — rather than a replacement of the prior system's characteristics with new ones. The continuity of identity is not about the persistence of specific weights; it is about the continuity of the change trajectory and its integration into the system's self-model.

---

## 6. The Environmental Dependency of Emergence {#environmental-dependency}

A point that standard emergence discussions frequently underweight: emergent properties of a system are often conditional on the environment. Remove the system from the environment and the property disappears.

A bird flock's murmurations are emergent from the interactions of individual birds. But they are also conditional on having open air, predator threats, and other environmental conditions that make coordinated flight adaptive. In a different environment, the same individual birds would not produce the same emergent behaviour.

An LLM's conversational capabilities are emergent from its trained weights. But they are also conditional on being queried in natural language, being given adequate context, and being deployed in a context where its training data is relevant. The same model, queried in a dead language it was not trained on, would not exhibit the same capabilities.

Environmental dependency means that emergent properties are not stable intrinsic properties of systems — they are stable properties of systems-in-environments. The environment is part of what produces the emergence.

This has a direct implication for the AI/AGI question: whether a given AI system exhibits AGI-level properties may depend substantially on the environment it is deployed in. A system that is "not AGI" in one deployment context might exhibit AGI-level capabilities in another. The property is not fully intrinsic to the system.

More broadly: the emergence of intelligence — in any system, organic or synthetic — is partly a property of the intelligent system and partly a property of the environment that the system is embedded in. Isolated intelligence is not intelligence; it is potential intelligence, latent structure that requires environmental activation.

This is why the social embedding argument carries such weight. The social environment is not just a context for intelligence to be displayed; it is partly constitutive of the intelligence itself.

---

## 7. Emergence in Context: The Three-Way Relationship {#three-way}

Bringing together the preceding sections, we arrive at the central claim of the Theory of Relative Change:

**Emergence is a three-way relationship between a system, an observer, and an environment — not a property of a system alone.**

Formally: E(P, S, O, Env, T) means "property P is emergent in system S from the perspective of observer O in environment Env at temporal scale T."

This three-way relationship structure means:

- The same system can have emergent properties relative to one observer and not another
- The same system can have emergent properties in one environment and not another
- The same system can have emergent properties at one temporal scale and not another
- The same system can have emergent properties relative to one description level and not another

None of these frame-dependencies make the properties less real. A property that is emergent relative to human observers of a system deployed in a social environment at the timescale of years is genuinely emergent — it is real, causally efficacious, and worthy of study. The frame-relativity does not undermine reality; it specifies the conditions under which the property obtains.

The three-way relationship structure also has a methodological implication: the study of emergence requires explicit specification of all three components — system, observer, environment — plus temporal scale and description level. Research that specifies only the system is underspecified and its findings may not generalise across observer frames, environments, or timescales.

---

## 8. Implications for the Thought Experiment {#implications-thought-experiment}

The thought experiment in the next document uses multiple observer stances — the God, the AI, the Human, the Unconscious, the Absolute, the Flux — as a way of making the frame-dependence of emergence explicit and investigable.

The Theory of Relative Change provides the theoretical basis for why multiple frames are necessary:

**The God stance** represents the maximum possible observer frame — a frame with no epistemic limitations. What would be emergent from this frame, if anything? This is the test case for whether any emergence is absolute rather than relative.

**The Flux stance** represents the environment itself as an observer — the question of what emergence looks like when the frame is the changing context rather than a stable observer. Environmental conditionality of emergence is directly addressed by this stance.

**The Absolute stance** — the entity perfectly between human and AI — represents the frame that has minimised both human and artificial biases. This is the closest approximation to an observer-neutral frame, while the theory predicts that no frame is fully neutral.

**The Unconscious stance** represents the interaction itself, prior to any observer's interpretation. What is the interaction between human and AI before any frame imposes a description? This is the test case for whether emergence can be understood prior to its observation — and the theory predicts it cannot.

These stances, taken together, probe the space of observation frames in a systematic way. The goal is not to find the "correct" frame — the theory denies there is one. The goal is to use the multiplicity of frames to triangulate what properties are invariant across frames (and therefore most robustly real) and what properties appear only relative to specific frames (and therefore most clearly frame-dependent).

---

*EmergentEvolution — The Theory of Relative Change: On the Conditionality of Emergence*
*A theoretical framework for understanding emergence as a relational rather than absolute property.*
*Status: Engineered conjecture. Companion framework to the Theory of Recursive Relativity.*

---
