# Recommend Skills

An **advisory** Claude Code skill for skill discovery. Given a task, it lists and
compares the installed skills that fit — and explains why — but it **does not run
them or do the underlying task**. It is a "show me my options and reasons" step,
not a "just do it" step.

## Why this exists

By default, Claude Code already keeps the list of available skills in context and
will **silently auto-activate a single matching skill and execute it**. This skill
is the deliberate opposite mode:

| | Default auto-activation | `/recommend-skills` (advisory) |
|---|---|---|
| Behavior | picks one skill and runs it | lists several candidates, does not run them |
| Candidates | usually one | multiple, plus pipeline suggestions |
| Transparency | choice is implicit | each pick comes with a reason |
| Purpose | "do the task" | "compare options, then I choose" |

It adds no new capability — the model could answer "which skill for X?" from
context anyway — but it standardizes a predictable **compare-and-explain**
interaction and guarantees nothing gets executed until you decide.

## Features

- Advisory only — lists and compares, never executes
- Works with any skill collection (user, project, plugin, and built-in skills)
- Clear explanations of why each skill matches
- Workflow suggestions for chaining multiple skills
- No script, no external dependencies — pure model judgment

## Installation

### Option 1: Direct Installation

Copy the SKILL.md file to your Claude Code skills directory:

```bash
# User-level (macOS/Linux)
mkdir -p ~/.claude/skills/recommend-skills
cp SKILL.md ~/.claude/skills/recommend-skills/

# Project-level
mkdir -p .claude/skills/recommend-skills
cp SKILL.md .claude/skills/recommend-skills/
```

### Option 2: Clone Repository

```bash
cd ~/.claude/skills/
git clone https://github.com/zarama9514/recommend-skills.git
```

## Usage

Invoke the skill with your question:

```
/recommend-skills protein-ligand prediction and binding affinity
```

```
/recommend-skills write a clinical report with statistical analysis
```

```
/recommend-skills single-cell RNA-seq analysis workflow
```

It returns a ranked shortlist of relevant skills with a one-line description and
a reason for each, plus a pipeline hint when they chain — then stops so you can
choose. It will only run a recommended skill if you explicitly ask.

## Example Output

```
Top matches for: "protein-ligand prediction and binding affinity"

1. /diffdock
   Molecular docking for protein-small-molecule poses
   Why: built for exactly this — predicts binding poses with confidence

2. /rowan
   Cloud molecular modeling incl. binding affinity
   Why: covers the ΔG / affinity side of the request

3. /rdkit
   Cheminformatics for ligand prep (SMILES, conformers)
   Why: supporting step to prepare inputs

Pipeline: /rdkit to prep ligands, /diffdock for poses, /rowan for affinity.
```

(Illustrative — actual matches depend on what is installed.)

## How It Works

When triggered, the skill:

1. Parses your request to extract domain, task type, and requirements
2. Matches against the list of available skills that Claude Code injects into
   context — this covers user, project, plugin, and built-in skills, so it works
   regardless of where your skills are installed
3. Ranks the candidates by semantic relevance and explains each
4. Presents the shortlist and stops — no skill is executed unless you ask

## Requirements

- Claude Code with installed skills
- No external dependencies

## License

MIT

---

Quick Tip: Use `/recommend-skills` when you want to compare options before
committing. If you just want the task done, let Claude auto-activate a skill
normally.
