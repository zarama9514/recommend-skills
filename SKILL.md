---
name: recommend-skills
description: Analyze user request and recommend the most relevant installed skills with clear explanations. Use when user asks for skill recommendations, needs help choosing between skills, or wants to discover applicable skills for their task.
triggers:
  - "recommend skills"
  - "which skills"
  - "what skills"
  - "match skills"
  - "find relevant skills"
  - "skill recommendation"
  - "help me choose a skill"
  - "suggest skills"
---

# Skill Recommender

When this skill is triggered, analyze the user's request and recommend the most relevant skills from all installed skills in your environment.

## Your Task

1. **Parse the user's request** — extract domain, task type, and key requirements
   - Is it about: proteins? RNA? data analysis? writing? visualization? ML? etc.
   - What's the core task: prediction? analysis? visualization? generation? processing?
   - Any specific tools/formats mentioned? (SMILES, BAM, FASTA, etc.)

2. **Scan installed skills** — you should:
   - Reference the skill descriptions available in ~/.claude/skills/
   - Look at each skill's description and triggers
   - Match against the user's request semantically
   - Do NOT assume specific skills exist — work with what's installed

3. **Rank by relevance** — consider:
   - **Exact match:** skill directly addresses the task
   - **Primary fit:** highly relevant to the core need
   - **Secondary fit:** useful complement or related analysis
   - Only include relevant matches (use semantic judgment, not percentages)

4. **Format your response** clearly:
   ```
   Top Skill Matches (for: "user's request")
   
   1. /skill-name
      One-line description of what it does
      Why: how it directly matches their request
   
   2. /skill-name
      Description
      Why: secondary reason it's relevant
   ```

5. **Add context** if helpful:
   - "Use /skill-name for this exact workflow"
   - "Pair /skill-1 with /skill-2 for end-to-end pipeline"
   - "This skill not available in your installation"

## How to Find Installed Skills

When recommending, check what skills are actually available:
- Read descriptions from ~/.claude/skills/*/SKILL.md if needed
- Only recommend skills that exist in the user's installation
- Suggest "This type of task typically uses X skill, check if it's installed" if unsure

## Example

**User:** `/recommend-skills protein-ligand prediction`

**Check installed skills**, then respond:
```
Top Skill Matches (for: "protein-ligand prediction")

1. /diffdock
   Molecular docking for protein-small-molecule pose prediction
   Why: directly designed for protein-ligand binding poses

2. /rowan
   Cloud molecular modeling with binding affinity
   Why: includes binding affinity and docking capabilities

3. /deepchem
   Molecular ML with ADMET and affinity prediction
   Why: can predict binding using pre-trained models
```

Or if those skills aren't installed:
```
Top Skill Matches (for: "protein-ligand prediction")

1. /rdkit
   Cheminformatics toolkit for molecular preparation
   Why: essential for handling SMILES and molecule data
```

---

**Key:** Use semantic understanding based on the installed skills available to the user, not a hardcoded list.
