---
name: recommend-skills
description: Advisory mode for skill discovery — lists and compares the installed skills that fit a task and explains why, but does NOT execute them. Use when the user asks which skill / what skill to use, wants skill recommendations or suggestions, needs help choosing between skills, or wants to browse skills that apply to their task before committing. Triggers on phrases like "recommend skills", "which skill", "what skills do you have for", "suggest a skill", "help me choose a skill". This is a compare-and-explain step, not a do-the-task step.
---

# Skill Recommender (advisory mode)

Analyze the user's request and point them to the installed skills that best fit it.

**This skill is advisory: it lists, ranks, and explains candidate skills — it does
not run them or do the underlying task.** By default Claude Code will silently
auto-activate a single matching skill and execute it; this skill is the opposite
mode — surface several options with reasons so the user can choose. After showing
the shortlist, stop and let the user pick; only proceed to run a skill if they ask.

## Source of truth: the skills already in your context

Claude Code injects the full list of available skills — with their descriptions —
into your context at the start of the session (the "available skills" list, and
any `Skill` tool definitions). **That list is authoritative.** Use it directly.

- It already covers every source: user (`~/.claude/skills/`), project
  (`.claude/skills/`), plugins, and built-in skills.
- Do NOT enumerate `~/.claude/skills/` by reading files — that is slower and
  misses project, plugin, and built-in skills. Only read a specific `SKILL.md`
  if you need detail beyond its description to break a tie.
- Never recommend a skill that is not in that list.
- Never recommend `recommend-skills` itself.

## What to do

1. **Understand the request** — the domain (proteins, RNA, stats, writing,
   visualization, ML, …), the core action (predict / analyze / visualize /
   generate / convert / review …), and any tools or formats named (SMILES, BAM,
   FASTA, .docx, …).

2. **Match against the available-skills list semantically.** Compare the intent,
   not just keywords. A request often maps to 1–4 skills; some tasks chain
   several into a pipeline.

3. **Rank by fit** using judgment (no percentage scores):
   - Direct fit — the skill is built for exactly this task.
   - Strong fit — clearly relevant to the core need.
   - Supporting fit — a useful complement (e.g. visualization or literature).
   Return only genuinely relevant skills. If nothing fits well, say so plainly
   and suggest the closest general-purpose option.

## Output format

```
Top matches for: "<the user's request>"

1. /skill-name
   One line on what it does
   Why: how it fits this request

2. /skill-name
   One line on what it does
   Why: how it fits this request
```

Close with a workflow hint when skills chain together, e.g.
"Pipeline: /skill-a to prepare, then /skill-b to analyze, then /skill-c to plot."

Then **stop** — do not start executing any recommended skill unless the user
explicitly asks you to run it.

## Example (illustrative — actual matches depend on what is installed)

User: `/recommend-skills protein-ligand pose prediction and binding affinity`

```
Top matches for: "protein-ligand pose prediction and binding affinity"

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

If none of those are installed, recommend whatever the available list actually
contains for that domain instead.
