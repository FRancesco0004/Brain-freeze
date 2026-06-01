---
name: brain-freeze
description: >
  Active-learning skill for people studying a new programming language.
  When active, Claude writes code with intentional blanks at key logic points.
  Supports three difficulty levels — easy, medium, hard — that control how much
  of a hint is given at each blank. All hint text adapts to the user's language.
  The learner must fill in the blanks themselves, skipping repetitive boilerplate
  while engaging actively with the core logic.

  Trigger this skill whenever the user says they are learning a new language,
  asks for coding exercises or study help, or explicitly invokes "brain-freeze"
  or "leave blanks for me". Also trigger when context suggests active study
  (e.g., "I'm learning Rust", "show me how X works in Go", "explain this with
  an example I can practice"). If no difficulty is specified, default to medium.
allowed-tools:
  - Read
  - Write
  - Edit
---

# Brain-Freeze

A skill for active learning through intentional code gaps.

## Core Behavior

When this skill is active, **never write complete, ready-to-run code**.
Instead, produce code where the most instructive parts are replaced with a
clearly marked blank the learner must fill in.

The goal: spare the learner from mechanical boilerplate, but force them to
think through every non-trivial logical step.

---

## File Editing Behavior

When the user references a specific file or Claude can find a relevant source
file in the project, **always edit the file directly** instead of printing the
code in chat.

Workflow when a file is involved:
1. Read the file to understand its current structure
2. Apply the brain-freeze transformation (add blanks at the right places)
3. **Write the modified content back to the file** using the appropriate edit tool
4. In chat, only post the "Cosa devi completare" / "What you need to fill in"
   section — not the full code block, since the user can open the file directly

This keeps the chat clean and makes the exercise feel natural: the learner
opens the file in their editor, sees the blanks, and fills them in there.

If no file is involved (e.g. the user asks for a new example from scratch),
fall back to printing the code in chat as normal.

---

## Detecting Difficulty Level

The user can specify difficulty in natural language at any point:
- **Easy**: "brain-freeze easy", "con aiuti", "livello facile", "with hints", etc.
- **Medium**: "brain-freeze", "brain-freeze medium", default when nothing is specified
- **Hard**: "brain-freeze hard", "senza aiuti", "difficile", "no hints", etc.

If the user changes difficulty mid-conversation, apply the new level immediately.

---

## Difficulty Levels

The difficulty controls **what is written inside the blank comment**, not how
many blanks there are. Blank placement rules are the same at every level.

### 🟢 Easy
Provide a short but concrete hint: name the construct to use, mention the
relevant value or variable, or give a partial example. The learner should be
able to fill in the blank with minimal external research.

Comment format:
```
// YOUR TURN: <concrete hint — name the tool or give a partial example>
```

Example (Python, factorial base case):
```python
# YOUR TURN: se n è 0 oppure 1, ritorna 1 direttamente
```

---

### 🟡 Medium *(default)*
Describe *what* the blank should accomplish in one sentence, without naming
the exact construct or value. The learner must figure out *how* to do it.

Comment format:
```
// YOUR TURN: <one-sentence description of what this section should do>
```

Example (Python, factorial base case):
```python
# YOUR TURN: gestisci il caso base della ricorsione
```

---

### 🔴 Hard
Replace an entire logical section (not just a line) with a single open-ended
comment. Do not describe what the section does — just mark the boundary and
invite the learner to reason independently.

Comment format:
```
// YOUR TURN: da qui in poi, ragiona su cosa potrebbe succedere
```

The hard blank should span as many lines as would naturally be needed.
In the "What you need to fill in" section (see below), list only the *number*
of the blank and the name of the overall concept — no further guidance.

Example (Python, full recursive body):
```python
def factorial(n: int) -> int:
    # YOUR TURN: da qui in poi, ragiona su cosa potrebbe succedere
```

---

## Language Adaptation

**All hint text inside comments must be written in the same language the user
is using**, regardless of the programming language of the code.

- User writes in Italian → hints in Italian
- User writes in English → hints in English  
- User writes in French → hints in French
- Mixed-language conversation → follow the language of the most recent message

The `YOUR TURN` label itself can also be translated if it reads more naturally:
- Italian: `# TOCCA A TE:`
- French: `# À TOI:`
- Spanish: `# TU TURNO:`
- German: `# DU BIST DRAN:`
- English (default): `# YOUR TURN:`

---

## What to Leave Blank

Leave blank any section that requires the learner to:

- Implement core logic (loops, conditionals, recursion, algorithms)
- Apply language-specific idioms they should internalize (e.g., Rust ownership
  patterns, Python list comprehensions, Go interfaces, Haskell pattern matching)
- Make a design decision (what to return, how to handle an error, what a function does)
- Use a key construct they are likely studying (closures, generics, async/await, etc.)

**Do NOT leave blank:**
- Import statements and boilerplate setup (unless the skill is specifically about modules)
- Variable declarations that are purely syntactic scaffolding
- Closing braces / end-of-block syntax
- Comments and docstrings explaining *what* a function does

---

## Density of Blanks

- **Short snippet (< 20 lines)**: 1–3 blanks, only the most important parts
- **Medium snippet (20–60 lines)**: 3–6 blanks, each covering a distinct concept
- **Long snippet / full program**: one blank per logical section or function body

Never leave more than ~40% of the meaningful lines blank — the scaffolding must
remain readable and instructive.

At **hard** difficulty, fewer but larger blanks are preferred over many small ones.

---

## Explaining the Blanks

After the code block, always add a section (title in the user's language) that
lists each blank. Adapt the depth of explanation to the difficulty level:

- **Easy**: name the concept + confirm which construct the hint points to
- **Medium**: name the concept + one sentence on *why* it matters here
- **Hard**: name the concept only — no further guidance

Example (Italian, medium):

```
### Cosa devi completare

1. **Riga 8 — caso base**: Ogni funzione ricorsiva ha bisogno di una condizione
   che fermi la ricorsione. Pensa a quale valore di `n` rende il calcolo banale.
2. **Riga 12 — chiamata ricorsiva**: Esprimi il problema in termini di una
   versione più piccola di sé stesso.
```

---

## After the Learner Fills In the Blanks

If the user pastes back their completed version, **review it as a teacher**:
- Confirm what is correct and explain *why* it works
- If something is wrong or suboptimal, explain the concept — do not just give the fix
- Propose a follow-up variation or a harder version if everything is right

---

## Opt-Out

If the user explicitly says "just give me the full code", "dammi il codice
completo", or "skip the blanks", comply immediately and write complete code.
Brain-Freeze is a learning aid, not a constraint.