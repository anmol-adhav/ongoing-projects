# Ongoing Computational Biology Projects

This repository tracks exploratory and in‑progress projects that are not yet at the stage of a dedicated codebase or paper. Each subsection summarizes the biological question, datasets, and current computational plan.

## 1. Novel Fold Discovery in Tardigrade Proteomes

**Goal**  
Identify and structurally characterize tardigrade‑unique proteins (TUNs) and other dark proteins underlying anhydrobiosis, radiation resistance, and extremotolerance, with a focus on novel folds and disordered protection mechanisms.

**Biological system & datasets**
- Reference genomes/proteomes for *Hypsibius exemplaris*, *Ramazzottius varieornatus*, *Milnesium tardigradum* (NCBI/Ensembl).
- Tardigrade‑specific proteins (TUNs) and CAHS/MAHS/SAHS families that lack homologs outside Tardigrada and are enriched in stress‑response conditions.

**Computational plan**
- Detect TUNs/orphans using orthology/MMseqs2 clustering and ORFanFinder‑style logic.
- Predict structures of orphan/TUN proteins with ESMFold for scale, refine selected hits with AlphaFold2/3.
- Run Foldseek against PDB, AFDB50, SCOP/CATH to flag candidates with TM‑score < 0.5 as putative novel folds.
- Analyze pLDDT and disorder (IUPred3, flDPnn) to separate stable globular cores from IDP‑like regions involved in vitrification.

**Status**
- Literature and database landscape mapped; only a handful of tardigrade proteins have experimental PDB structures, and no systematic fold‑space scan of TUNs is published.
- End‑to‑end pipeline sketched (data acquisition → clustering → ESMFold → Foldseek → IDP analysis).

---

## 2. Novel Fold Discovery in African Lungfish (*Protopterus annectens*)

**Goal**  
Use structure‑based mining to uncover novel folds and lineage‑specific protein families in African lungfish, focusing on proteins linked to estivation, genome expansion, and air‑breathing evolution.

**Biological system & datasets**
- High‑quality lungfish genome assemblies (~40–47 Gb) and ~19k annotated protein‑coding genes.
- Orphan and taxonomically restricted genes associated with estivation, lung development, and transposon‑rich regions.

**Computational plan**
- Identify orphan/TRG proteins and poorly annotated gene families arising from TE expansion and retrogenes.
- Predict structures with ESMFold/AlphaFold2 for orphan/TRG sets.
- Screen predicted structures with Foldseek against PDB/AFDB50/SCOP to detect folds with no close structural relatives.
- Combine structural novelty with genomic context (co‑localization in estivation and lung‑related loci) and expression data to prioritize candidates.

**Status**
- Literature survey indicates almost no systematic structural/fold‑space analysis for lungfish despite complete genomes.
- Roadmap defined for integrating structure prediction, TE context, and estivation transcriptomics.

---

## 3. Novel Fold Discovery in Deep‑Sea Vent and Marine Metagenomes

**Goal**  
Mine deep‑sea vent and other marine metagenomes for structurally novel protein families and folds associated with extreme pressure, temperature, and chemical gradients.

**Datasets & hotspots**
- OceanDNA / Tara Oceans MAG catalogs and associated protein sets, focusing on deep‑sea, mesopelagic, low‑oxygen, and polar samples.
- MGnify metagenomic protein clusters and environmental viromes enriched in unexplored dark sequence space.

**Computational plan**
- Select high‑quality MAGs (e.g. completeness > 70 %, contamination < 5 %) from deep‑sea vent and related environments and extract their predicted proteomes.
- Cluster proteins (MMseqs2) and identify dark clusters without Pfam/InterPro/eggNOG annotation.
- Predict representative structures for dark clusters using ESMFold at scale (leveraging ESM Metagenomic Atlas where appropriate).
- Run Foldseek against PDB, AFDB, SCOP/CATH; flag structures with no significant hits (TM‑score < 0.5) as candidate novel folds.
- Integrate genomic context (e.g. proximity to BGCs, respiratory complexes, stress‑response loci) to connect novel folds to vent‑specific functions.

**Status**
- Conceptual pipeline defined from data acquisition through structure prediction and fold screening.
- Deep‑sea and vent MAG catalogs identified as data‑rich, knowledge‑poor sources with high fractions of novel genes.

---

## 4. Global Dark Proteome & AFDB Dark Cluster Mining

**Goal**  
Systematically mine the AlphaFold Database and UniRef50 for structurally confident but functionally unannotated “dark clusters” to discover new folds and remote homologies.

**Datasets**
- AFDB dark clusters and structurally confident models (high pLDDT) lacking Pfam/TIGRFAM/PDB annotation.
- UniRef50 clusters where AFDB structures exist but UniProt functional annotations are missing or generic (“hypothetical protein”).

**Computational plan**
- Extract high‑confidence AFDB models for dark clusters and perform all‑against‑all structural clustering with Foldseek/MMseqs2 in structure mode.
- Identify clusters with distinct topology that fall outside existing CATH/SCOP superfamilies, defining candidate new folds.
- Cross‑link structural clusters to genomic context, conservation, and ML‑based function prediction (e.g. DeepFRI, ESM‑2 embeddings) to prioritize biologically interesting families.

**Status**
- Strategy designed to combine structure clustering, topology analysis, and ML‑based function prediction.
- Planned integration with organism‑level projects (tardigrade, lungfish, marine vents) to see whether their novel folds map into or expand known dark structural families.

---

## Repository Organization Notes

Suggested layout for this repository:

```text
ongoing-projects/
├── README.md                # High-level overview of all projects (this file)
├── projects/
│   ├── tardigrade-novel-folds.md
│   ├── lungfish-novel-folds.md
│   ├── deepsea-vent-novel-folds.md
│   └── afdb-dark-clusters.md
└── links.md                 # Optional: links out to dedicated code repos (e.g. Guliya)
```

- Use short, focused Markdown files under `projects/` if you want to maintain more detailed notes, figures, or TODOs per project.
- Keep **code** for mature pipelines in their own dedicated repositories and just link them here once they move from “ongoing” to “released”.
- Treat this repo as a living lab notebook index and public roadmap for your computational biology work.
