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

When this skill is triggered, analyze the user's request and recommend the most relevant skills from all installed skills.

## Your Task

1. **Parse the user's request** — extract domain, task type, and key requirements
   - Is it about: proteins? RNA? data analysis? writing? visualization? ML? etc.
   - What's the core task: prediction? analysis? visualization? generation? processing?
   - Any specific tools/formats mentioned? (SMILES, BAM, FASTA, etc.)

2. **Mentally scan installed skills** — reference the skill list you know:
   - **Protein/Molecular:** diffdock, deepchem, torchdrug, rdkit, datamol, esm, tamarind, rowan, molecular-dynamics, glycoengineering
   - **RNA/Single-cell:** scanpy, scvi-tools, scvelo, bulk-rnaseq, cellxgene-census, anndata
   - **Writing/Docs:** scientific-writing, literature-review, clinical-reports, treatment-plans, scientific-slides, latex-posters, docx, pptx
   - **Data/Stats:** statistical-analysis, statistical-power, exploratory-data-analysis, scikit-learn, statsmodels, pymc
   - **Visualization:** matplotlib, seaborn, scientific-visualization, scientific-schematics, generate-image
   - **ML:** pytorch-lightning, transformers, scikit-learn, stable-baselines3, shap
   - **Genomics:** pysam, geopandas, phylogenetics, nextflow, biopython, bioservices
   - **Medical/Clinical:** pyhealth, pydicom, clinical-decision-support, neurokit2
   - **Lab/Automation:** opentrons-integration, pylabrobot, benchling-integration, labarchive-integration
   - **Specialized:** pathway-enrichment, neuropixels-analysis, pathml, modal, optimize-for-gpu

3. **Rank by relevance** — consider:
   - **Exact match:** skill directly addresses the task
   - **Primary fit:** highly relevant to the core need
   - **Secondary fit:** useful complement or related analysis
   - Only include scores 70%+ unless user is asking "what could help"

4. **Format your response** clearly:
   ```
   🎯 Top Skill Matches (for: "user's request")
   
   1. /skill-name [⭐⭐⭐ 95% match]
      One-line description of what it does
      Why: how it directly matches their request
   
   2. /skill-name [⭐⭐ 70% match]
      Description
      Why: secondary reason it's relevant
   ```

5. **Add context** if helpful:
   - "Use `/skill-name` for this exact workflow"
   - "Pair `/skill-1` with `/skill-2` for end-to-end pipeline"
   - "Skip `/skill-x` — not suitable because..."

## Example

**User:** `/recommend-skills protein-ligand prediction and binding affinity`

**Response:**
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
```

---

**Key:** Be confident and specific. Use semantic understanding, not keyword matching.
