# Recommend Skills

A Claude Code skill that intelligently recommends relevant skills based on your request. Analyzes your task and suggests the most applicable skills from your installed skill library.

## Features

- 🎯 **Smart Matching** — Uses semantic understanding rather than keyword matching
- 📚 **Full Coverage** — Knows about 150+ scientific and technical skills
- 💡 **Clear Explanations** — Shows why each skill matches your request
- 🔗 **Workflow Suggestions** — Recommends how to combine multiple skills
- ⚡ **Fast Recommendations** — Instant analysis without external APIs

## Installation

### Option 1: Direct Installation

Copy the `SKILL.md` file to your Claude Code skills directory:

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
git clone https://github.com/yourusername/recommend-skills.git
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
- Top 5 relevant skills ranked by match percentage
- One-line description of each skill
- Clear explanation of why it matches your request
- Workflow suggestions for combining skills

## Example Output

```
🎯 Top Skill Matches (for: "protein-ligand prediction and binding affinity")

1. /diffdock [⭐⭐⭐ 98% match]
   Molecular docking for protein-small-molecule pose prediction
   Why: directly designed for protein-ligand binding poses

2. /rowan [⭐⭐⭐ 95% match]
   Cloud molecular modeling with binding affinity prediction
   Why: includes explicit ΔG binding affinity prediction

3. /deepchem [⭐⭐ 82% match]
   Molecular ML with ADMET and affinity prediction models
   Why: can predict binding affinity using pre-trained models

💡 Workflow: /diffdock (get poses) → /rowan (predict ΔG)
```

## How It Works

When triggered, the skill:
1. Parses your request to extract domain, task type, and requirements
2. References the comprehensive skill catalog (150+ scientific and technical skills)
3. Ranks skills by semantic relevance
4. Formats recommendations with explanations and workflow suggestions

The skill uses **semantic understanding** rather than simple keyword matching, making recommendations more accurate for complex or multi-domain requests.

## Supported Domains

- **Protein/Molecular:** Docking, structure prediction, binding affinity, design
- **RNA/Single-cell:** Sequencing analysis, transcript processing, cell analysis
- **Data/Statistics:** Statistical analysis, machine learning, visualization
- **Genomics:** Variant analysis, alignment, genome assembly
- **Writing/Docs:** Scientific manuscripts, reports, presentations
- **Medical/Clinical:** EHR analysis, clinical decision support
- **Lab/Automation:** Lab equipment control, protocol management
- And 150+ more specialized skills

## Requirements

- Claude Code with installed skills library
- No external dependencies

## License

MIT

## Contributing

Suggestions for improvement welcome. The skill maintains a mental catalog of available skills and can be updated as new skills are installed.

---

**Quick Tip:** Use `/recommend-skills` whenever you're unsure which skill applies to your task, or when you want to discover skills for a new domain.
