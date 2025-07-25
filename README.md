# Fluorophore-design
Deep learning-based de novo molecular design of fluorescent molecules with target photophysical properties.

---

## Table of Contents
- Description
- project overview
- Molecular Generation Results
  - Predicted photophysical properties Evaluation
  - Evaluation of Synthesizability
  - Structural Complexity Analysis
- Dependencies
- citation
  
---
## Description
 We present a fluorescence-oriented molecular design strategy that integrates multiple generative models within a chemically constrained and photophysically relevant subspace. Rather than relying on large-scale datasets or model-specific tuning, our approach builds on a curated training set constructed exclusively from atom-in-SMILES (AIS) fragments spanning chromophore-like molecules.The pipeline accommodates reinforcement learning–based ReLeaSE, which employs AIS-based tokenization, MolDQN, which utilizes a graph-based molecular representation, and the combinatorial optimization–based MolFinder, which operates on SMILES strings—each guided by a semi-heuristic objective function targeting excitation energy, oscillator strength, and fluorophore similarity. Despite the compact training corpus, the pipeline yields structurally novel and optically active molecules, validated via QM calculations at the sTDA/CAM-B3LYP level. Our findings demonstrate that strategic data curation and property-driven integration can enable general-purpose models to succeed in specialized discovery tasks such as de novo fluorophore design.

---
## Project Overview
![Project overview](images/overview.png)
This figure outlines the overall pipeline:  
- **Data source**: Molecules were curated from **ZINC** and **PubChemQC** databases.  
- **Generative models**:  
  - **ReLeaSE** uses AIS-tokenized SMILES and combines a generator with a property predictor.  
  - **MolDQN** applies deep Q-learning on SMILES graphs to optimize properties.  
  - **MolFinder** uses the CSA algorithm to evolve SMILES strings toward desired profiles.  
- **Predictive models**:  
  - A **Random Forest (RF)** and **multi-task loss MLP** predict molecular properties.  
  - All models utilize **AIS-based binary fingerprinting** for optimized molecular representation and analysis.

---
## Molecular Generation Results
### Predicted photophysical properties Evaluation
![KDE subfig](results/kde_subfigs_legends_insideGH_1.png)
Kernel density estimates (KDEs) of excitation energy (in eV) and oscillator strength distribu-  tions generated by various molecule design models, compared against the PubChemQC-500K baseline  
- **MolDQN-RF** and **MolFinder-RF** models produce molecules with significantly higher oscillator strengths, clustering around **f ≈ 1.0**, which is favorable for fluorophore design.
- **MLP-based models** (e.g., MolFinder-MLP) exhibit slightly lower strengths (**f ≈ 0.6**), while **ReLeaSE-MLP** aligns more closely with the distribution.
- **ReLeaSE-RF** underperforms, generating molecules with low oscillator strengths (**f ≈ 0.2**) despite high excitation energies.

---
### Evaluation of Synthesizability  
![Synthetic Accessibility](results/synthetic_accessibility_boxplot_tunedz.png)
Compares the **normalized synthesizability scores** across six generative models using diverse metrics (SAScore, SCScore, RAScore, SYBA, and RCScore).  
- **ReLeaSE-RF** shows **the best overall synthesizability**, with high medians and low variance—especially in SCScore, RAScore, and SYBA.  
- **ReLeaSE-MLP** also performs strongly, particularly in SAScore and RAScore.  
- **MolDQN** are moderate performers but show greater variability and lower SYBA scores, suggesting more chemically complex structures.  
- **MolFinder** rank lowest, especially in SYBA, RCScore and RAScore, indicating lower retrosynthetic plausibility.
---
### Structural Complexity Analysis
![Complexity metric](results/complexity_metrics_boxplot_1to1000z.png)
Distributions of **normalized molecular complexity scores** across four metrics: Bertz, Barone, Böttcher, and spatial complexity.
- **MolFinder** generates molecules with substantially higher complexity, showing elevated medians in both 2D and 3D metrics.  
  These molecules often exhibit polycyclic, heavily branched, and stereochemically rich structures, navigating deeper regions of chemical space.
- **MolDQN** and **ReLeaSE** models tend to generate simpler molecules, favoring linear or lightly branched scaffolds with fewer rings and stereocenters.  
  This reflects the known behavior of reinforcement learning models, which prioritize accessible transformations unless explicitly guided toward more complex topologies.
---
## Dependencies

---
## citation

---
