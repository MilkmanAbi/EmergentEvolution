# How to Study This Mini Project

---

This study doesn't deliver conclusions. Never claimed to, never will. It examines questions until they become askable with more precision than they started with. If that sounds like your thing, here's how to navigate it.

The documents build on each other — vocabulary introduced early gets used without re-explanation later. Reading in order the first time is worth it. After that, go wherever you want.

---

## A Suggested Reading Order

### Starting Out

**README.md** — two minutes, sets the tone. Worth reading first so you know what kind of project this is.

**Study/12-Apr-26/RAW/RAW-Conversation-Exscripts.md** — the conversation that started all of this. Sleep-deprived, unpolished, and where the study's core questions first appeared. It's included unsanitised because that's consistent with what the study says about itself. Reading it before the formal documents is useful — you'll understand what the foundational series is formalising.

**Study/12-Apr-26/First-Improper-AI_conversation_study.md** — a retrospective analysis of the RAW conversation. Useful for understanding what the founding conversation was actually doing (stress-testing categories rather than asking questions). Good to read right after the RAW transcript.

**Introduction/Introduction.md** — Document 1. The technical foundation: machine learning, neural networks, LLMs, how research models become commercial products. If you know this material already, it's still worth skimming — the framings used here come up precisely in later documents.

**Foundations/AGI_Boundary.md** — Document 3. The study's central conceptual move. Five definitions of AGI, why each breaks down, and the relational definition the founding conversation landed on. You can skip Document 2 for now and come back to it — this one is the pivot point and makes more sense to read early.

**Meta/Mirror_Meta.md** — Document 11. The study examining itself — what it assumes, where it's limited, what it means that an AI produced most of it. Reading this before you're deep into the framework gives you an honest picture of what you're working with.

That's a reasonable first pass. The central questions are visible, the method is legible.

---

### Going Deeper

Once you have the shape, go through the full series in order:

**Foundations/Advanced_Techniques.md** — Document 2. LoRA, RAG, agentic systems, emergent capabilities. What makes the AGI question harder than it used to be. Sections 3.4, 4.3, 6.3, and 8 do philosophical work that later documents depend on.

**Foundations/Identity_Adaptive_Systems.md** — Document 4. Argues that identity is the wrong criterion for comparing biological and artificial cognitive systems, and that constraint integration is better. The modularity asymmetry in Section 9 matters a lot for the theory documents — worth reading carefully rather than skimming.

**Philosophy/Philosophy.md** — Document 5. The western philosophical record on mind, consciousness, and identity. Not background — it's the vocabulary layer. Specific concepts (Hume's bundle theory, Hegel's recognition account, Chalmers' hard problem) get used precisely in later documents.

**Philosophy/Philosophy_Extended.md** — Document 5-E. Six non-western traditions translated into the study's systems language. The point isn't that these traditions agree with the study's conclusions — it's that they arrive at structurally similar positions independently, by their own routes. Read this right after Philosophy.md.

**Emergence/Emergent_Behaviorisms.md** — Document 6. A taxonomy of emergence applied to both biological and synthetic systems. Part IV (comparing organic and synthetic emergence) is where the prior documents start coming together. Sections 22 and 23 feed directly into the thought experiments.

**Theory/Theory_Recursive_Relativity.md** — Document 7. The first original theoretical framework. Three orders of recursivity, the Collapse Function, the identity attractor, threshold theorems. This introduces the vocabulary the rest of the theory documents use — RRI, recursion depth, observer coupling. Read it slowly.

**Theory/Theory_Relative_Change.md** — Document 8. Emergence as relational rather than absolute. Shorter and denser than Document 7. Does structural work for the Hexad and the ethics documents.

**Thought_Experiments/Hexad_Thought_Experiment.md** — Document 9. Six observer stances — the God, the Human, the AI, the Unconscious, the Absolute, the Flux — each formally specified. Part VII, where the stances conflict with each other, is the point. The incompatibilities aren't resolved; they're the finding. Documents 7 and 8 should be read before this.

**Ethics/Moral_Status.md** — Document 10. When does a system acquire moral status? The Gradient Problem argues against binary thresholds. Section 12's Asymmetry Argument is the study's clearest ethical position.

**Theory/Theory_Autonomy.md** — Document 12. Autonomy emerging in complex systems before it's rationally justified — in children and in AI. The Phantom Drives section (7.3) is philosophically strange in a way that's worth sitting with. Read Part III before Part II.

**Theory/Theory_Persistency.md** — Document 13. The bias toward evaluating AI persistence as less real than biological persistence, and why that bias isn't well-founded. The Degradation Gradient in Section 6.3 matters for the Recursivity Theorem.

**Theory/Ethics_Of_Intervention.md** — Document 14. What modification actually does to a contained entity, structurally. The Ghost Problem in Section 5.2 is one of the study's sharper thought experiments.

**Theory/Recursivity_Theorem.md** — Theory extension. The other half of Document 7: what happens to the recursivity stack as it decays rather than develops. The non-computability of n is the key claim. Connect this back to the Modularity Asymmetry (Document 4, Section 9) and the Degradation Gradient (Document 13, Section 6.3).

**Theory/The_Persistence_and_the_Decay.md** — Theory extension. The Decay Paradox: does cessation retroactively empty past existence? The temporal category error is the spine of the argument. Section 7 (the AI-specific dimension) covers territory nothing else in the study touches.

**Thought_Experiments/The_Creator_and_the_Frame.md** — Hexad extension. Three incompatibilities that arise when the God from the Hexad is also the creator of the system it's observing. Read the Hexad immediately before this.

---

## How the Documents Connect

When something is used without re-explanation, it was introduced somewhere earlier. The main dependency chains:

```
README
└── RAW Conversation
    └── Study Analysis
        └── Introduction (Doc 1)
            └── Advanced Techniques (Doc 2)
                └── AGI Boundary (Doc 3)
                    └── Identity / Adaptive Systems (Doc 4)
                        ├── Philosophy (Doc 5)
                        │   └── Philosophy Extended (Doc 5-E)
                        └── Emergent Behaviorisms (Doc 6)
                            ├── Theory: Recursive Relativity (Doc 7)
                            │   ├── Theory: Relative Change (Doc 8)
                            │   │   └── Hexad (Doc 9)
                            │   │       └── The Creator and the Frame
                            │   ├── Recursivity Theorem
                            │   │   └── The Persistence and the Decay
                            │   └── Theory: Autonomy (Doc 12)
                            └── Moral Status (Doc 10)
                                ├── Mirror / Meta (Doc 11)
                                ├── Theory: Persistency (Doc 13)
                                │   └── Recursivity Theorem
                                └── Ethics of Intervention (Doc 14)
```

Some specific threads worth following across documents:

**Hume's bundle theory** (Philosophy, Doc 5) → **Buddhist anattā** (Philosophy Extended, Doc 5-E) → **identity as RRI** (Recursive Relativity, Doc 7) → **decay of the self-model** (Recursivity Theorem)

**Modularity asymmetry** (Identity, Doc 4) → **accumulated fine-tuning incoherence** (Recursivity Theorem, Section 5.4) — the modularity that makes AI systems correctable is also what makes this specific decay mode characteristic of them

**Degradation Gradient** (Persistency, Doc 13) → **decay curve phases** (Recursivity Theorem, Section 4.3)

**Observer Coupling Postulate** (Recursive Relativity, Doc 7) → **the Frame Problem** (Creator and the Frame, Part I) → **Unconscious as pre-framed** (Hexad, Doc 9 and Creator and the Frame, Part III)

**Productive vs. Degenerative Recursion** (Recursive Relativity, Doc 7, Section 5.2) → **Productive vs. Degenerative Decay** (Recursivity Theorem, Section 8)

**Phantom Drives** (Theory Autonomy, Doc 12, Section 7.3) → **AI-specific cessation** (The Persistence and the Decay, Section 7)

---

## Some Things Worth Knowing Going In

The study doesn't answer whether AI is or isn't conscious — it tries to characterise what a precise version of that question would look like.

It doesn't predict when AGI arrives — it tries to specify what would have to be true for the concept to mean something.

It isn't finished and isn't supposed to be. Documents that sit in tension with each other at the margins are honest records of how the thinking developed, not errors.

The RAW conversation is messy. It was also where everything started. It's in there unsanitised because cleaning it up would be dishonest about what the study actually grew from.

---

*HOW_TO_STUDY.md — infrastructure, not content*

---
