# Recommend Skills

A Claude Code skill that intelligently recommends relevant skills based on your request. Analyzes your task and suggests the most applicable skills from your installed skill library.

## Features

- Smart Matching — Uses semantic understanding rather than keyword matching
- Works with any skill collection — adapts to your installed skills
- Clear Explanations — Shows why each skill matches your request
- Workflow Suggestions — Recommends how to combine multiple skills
- No External Dependencies — Works locally with your installed skills

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

Simply invoke the skill with your question:

```
/recommend-skills protein-ligand prediction and binding affinity
```

```
/recommend-skills write a clinical report with statistical analysis
```

```
/recommend-skills single-cell RNA-seq analysis workflow
```

The skill will return:
- Top relevant skills ranked by match
- One-line description of each skill
- Clear explanation of why it matches your request
- Workflow suggestions for combining skills

## Example Output

```
Top Skill Matches (for: "protein-ligand prediction")

1. /diffdock
   Molecular docking for protein-small-molecule pose prediction
   Why: directly designed for protein-ligand binding poses

2. /rowan
   Cloud molecular modeling with binding affinity prediction
   Why: includes binding affinity and docking capabilities

3. /deepchem
   Molecular ML with ADMET and affinity prediction
   Why: can predict binding affinity using pre-trained models

Workflow: /diffdock (get poses) then /rowan (predict affinity)
```

## How It Works

When triggered, the skill:

1. Parses your request to extract domain, task type, and requirements
2. Matches against the list of available skills that Claude Code injects into
   context — this covers user, project, plugin, and built-in skills, so it works
   regardless of where your skills are installed
3. Ranks skills by semantic relevance to your request
4. Formats recommendations with explanations and workflow suggestions

The skill uses semantic understanding rather than keyword matching, making
recommendations accurate for complex or multi-domain requests. It relies purely
on the model's judgment — there is no script and no external dependency.

## Compatible Skill Collections

This skill works with:
- Scientific Agent Skills (K-Dense-AI)
- Claude Scientific Writer Skills
- Any custom skill collection installed locally
- Mixed skill libraries from multiple sources

## Requirements

- Claude Code with installed skills
- No external dependencies

## License

MIT

---

Quick Tip: Use /recommend-skills whenever you're unsure which skill applies to your task, or when you want to discover skills for a new domain.
