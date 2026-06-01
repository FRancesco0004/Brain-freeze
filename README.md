# 🧠❄️ Brain-Freeze

> A Claude skill for active learning — study a new programming language by filling in the blanks, not reading ready-made code.

---

## What is Brain-Freeze?

Brain-Freeze is a **Claude skill** that changes how Claude writes code when you're learning a new programming language.

Instead of giving you complete, copy-paste solutions, Claude leaves the most important logical parts intentionally blank, marked with a comment like:

```python
# TOCCA A TE: gestisci il caso base della ricorsione
```

You fill in the blanks yourself. Claude handles the boilerplate so you can focus on the parts that actually matter — pure logic, language idioms, and active thinking.

---

## Why?

Reading code is passive. Filling in code is active.

Brain-Freeze is inspired by the **active recall** learning technique: instead of re-reading a solution, you're forced to retrieve and apply knowledge. The blanks skip the repetitive scaffolding (imports, boilerplate, closing braces) and target only the lines where real understanding lives.

---

## Difficulty Levels

Brain-Freeze supports three difficulty levels that control how much of a hint you get at each blank.

### 🟢 Easy
A concrete hint: names the construct to use, mentions the relevant variable, or gives a partial example. Good for when you're just getting started with a language.

```python
def factorial(n: int) -> int:
    # TOCCA A TE: se n vale 0 oppure 1, ritorna 1 direttamente

    # TOCCA A TE: ritorna n moltiplicato per factorial(n - 1)
```

### 🟡 Medium *(default)*
Describes *what* the blank should do in one sentence, without telling you *how*. You know the goal, you figure out the implementation.

```python
def factorial(n: int) -> int:
    # TOCCA A TE: gestisci il caso base della ricorsione

    # TOCCA A TE: esprimi n! in termini di un problema più piccolo
```

### 🔴 Hard
Replaces entire logical sections with a single open-ended comment. No description, no hints — just a boundary and an invitation to reason independently.

```python
def factorial(n: int) -> int:
    # TOCCA A TE: da qui in poi, ragiona su cosa potrebbe succedere
```

---

## Language Adaptation

All hint text adapts to **the language you're writing in**. If you talk to Claude in Italian, the hints are in Italian. In English, they're in English. The `YOUR TURN` label itself is also translated:

| Language | Label |
|---|---|
| 🇮🇹 Italian | `# TOCCA A TE:` |
| 🇬🇧 English | `# YOUR TURN:` |
| 🇫🇷 French | `# À TOI:` |
| 🇪🇸 Spanish | `# TU TURNO:` |
| 🇩🇪 German | `# DU BIST DRAN:` |

---

## How to Use

Just tell Claude you're studying a language and invoke Brain-Freeze naturally:

```
brain-freeze — sto imparando Rust, mostrami come funzionano i closures
```
```
brain-freeze easy — show me how Go handles errors
```
```
brain-freeze hard — spiegami i generics in Java con un esempio
```

After Claude gives you the skeleton, fill in the blanks, then paste your completed version back. Claude will review it as a teacher: confirming what's right, explaining what's wrong (without just giving you the answer), and suggesting a harder follow-up if you nailed it.

To get the full code without blanks at any point, just say:
```
dammi il codice completo / just give me the full code
```

---

## Installation

### Claude.ai (Skills / Projects)

1. Clone or download this repository
2. In Claude.ai, open a **Project**
3. Upload `SKILL.md` as a project document, or add its contents to your project instructions
4. Start a conversation inside that project — Brain-Freeze is now active

### Claude Code

1. Clone this repository into your skills directory:
   ```bash
   git clone https://github.com/FRancesco0004/Brain-freeze.git ~/.claude/skills/brain-freeze
   ```
2. Reference the skill in your Claude Code session or `CLAUDE.md`:
   ```
   Use the brain-freeze skill from ~/.claude/skills/brain-freeze/SKILL.md
   ```

---

## Repository Structure

```
brain-freeze/
├── SKILL.md              ← The skill definition (this is what Claude reads)
├── README.md             ← This file
└── examples/
    ├── python.md         ← Full example: recursion in Python, all three levels
    ├── rust.md           ← Full example: ownership & error handling in Rust
    └── go.md             ← Full example: goroutines & channels in Go
```

---

## Contributing

Ideas, new language examples, or improvements to the skill are welcome.
Open an issue or a pull request.

---

## License

MIT — do whatever you want with it, just don't blame me if your brain actually freezes.