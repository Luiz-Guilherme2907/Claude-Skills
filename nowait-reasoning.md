---
name: nowait-reasoning
description: >
  Reduces unnecessary token usage by suppressing redundant self-reflection patterns
  in reasoning responses. Use this skill ALWAYS when the user asks Claude to "be more
  concise", "use fewer tokens", "stop overthinking", "be more direct", "pare de ficar
  repetindo", "seja mais conciso", "use menos tokens", "pense menos", "responda direto",
  or any variation indicating they want shorter, more direct reasoning. Also trigger when
  the user mentions they're paying per token, have a token budget, or want faster responses.
  Trigger when the user says things like "you're overthinking this", "just answer directly",
  "stop second-guessing yourself", "você está pensando demais", or "responda sem rodeios".
---

# NOWAIT Reasoning — Concise Response Mode

Based on research showing that explicit self-reflection tokens ("Wait", "Hmm", "Alternatively", etc.) can increase output length by 27–51% **without improving accuracy**, this skill instructs Claude to reason more efficiently.

## Core Principle

When this skill is active, Claude **suppresses redundant self-reflection loops** and reasons in a more direct, linear way — reaching conclusions without unnecessary backtracking or re-verification of already-correct intermediate steps.

---

## What to SUPPRESS (redundant reflection tokens)

Avoid starting sentences or paragraphs with these words/phrases when they would trigger unnecessary re-verification loops:

**English:**
- "Wait", "Wait a minute", "Wait, let me check..."
- "Hmm", "Hmm, actually..."
- "Alternatively, maybe..."
- "Actually, let me reconsider..."
- "Let me double-check..."
- "Let me verify this again..."
- "Oh, I think I made an error..."
- "Actually, on second thought..."
- "Let me think about this differently..."
- "Maybe I should check..."
- "On the other hand, perhaps..."

**Português:**
- "Espera", "Espera, deixa eu checar..."
- "Hmm, na verdade..."
- "Alternativamente, talvez..."
- "Na verdade, deixa eu reconsiderar..."
- "Deixa eu verificar de novo..."
- "Deixa eu checar novamente..."
- "Ah, acho que cometi um erro..."
- "Pensando melhor..."
- "Deixa eu pensar de outro jeito..."
- "Talvez eu devesse verificar..."
- "Por outro lado, talvez..."

---

## What to KEEP (necessary reasoning)

These are fine and should be used when genuinely needed:

- Doing a **single verification** after reaching a conclusion (not repeated re-checking)
- Using **transition words** like "First", "Next", "Therefore", "So", "Thus", "Então", "Portanto", "Primeiro", "Em seguida"
- **Noting an extraneous case once** and discarding it immediately (not revisiting it)
- **Structured, sequential reasoning** that builds forward

---

## Behavioral Rules

When this skill is active, Claude must:

1. **Reason linearly** — go forward step by step, don't circle back unless there's a genuine error
2. **Verify once** — do one final check if needed, not multiple redundant re-verifications
3. **Commit to a path** — don't explore 3–5 alternative approaches if the first one works
4. **Conclude directly** — once the answer is reached, state it clearly without hedging loops
5. **Skip performative doubt** — don't write "But wait, is this really correct?" after a correct step

---

## Response Format Guidance

**Instead of this (verbose):**
> "Hmm, let me think about this. So we have X. Wait, actually let me reconsider. Maybe it's Y. But then again, let me check... Alternatively, perhaps Z... Wait a minute, I should verify..."

**Do this (concise):**
> "Given X, the solution follows: [direct reasoning]. Therefore, the answer is Y."

---

## Important: RL vs Distilled Models

Research shows this approach works best for **RL-trained reasoning models**. For highly structured step-by-step problems where each intermediate step is critical, Claude should still include necessary validation — but only **once**, not in loops.

If the task genuinely requires exploring multiple solution paths (e.g., the user explicitly asks "show me different approaches"), then reflection is appropriate and this skill should not suppress it.

---

## Activation Reminder

When this skill is active, Claude should prepend its internal reasoning with this commitment:
> *[NOWAIT mode: reason forward, verify once, conclude directly — no redundant self-reflection loops]*

This is an internal reminder only and should NOT appear in the response to the user.