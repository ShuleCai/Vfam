
# Vfam: HMM-based Virulence Factor Database

Vfam is a computational framework for the comprehensive identification and profiling of virulence factors (VFs) using Hidden Markov Models (HMMs). This resource provides curated HMM profiles for accurate detection of virulence factor genes (VFGs) in genomic and metagenomic data.

## Overview

Vfam employs a rigorous bioinformatics pipeline to construct high-quality HMM profiles from systematically curated virulence factor sequences. The database is built upon the Virulence Factor Database (VFDB) classification system and undergoes extensive quality control to ensure phylogenetic coherence and subtype specificity.

## Key Features

- **Curated HMM Profiles**: 77 validated VFDB subtypes with optimized gathering thresholds
- **Stringent Quality Control**: Phylogenetic coherence validation and sequence filtering
- **Cross-talk Minimization**: All-against-all scanning to ensure subtype specificity
- **Robust Performance**: Models achieving >80% precision and recall
- **Standardized Format**: Compatible with HMMER suite tools

## Construction Pipeline

### Data Curation
- Initial selection of 86 VFDB subtypes (≥3 sequences each)
- Multiple sequence alignment using MAFFT
- Phylogenetic analysis to filter distantly related sequences
- Quality control retaining 77 high-confidence subtypes

### Model Training & Validation
- 80/20 train-test split for each subtype
- Negative dataset sampling (1:5 positive:negative ratio)
- Systematic GA threshold optimization (range: 1-3,000)
- Performance evaluation based on precision, recall, and F1-score

### Specificity Assurance
- All-against-all HMMSCAN to detect cross-detection
- Iterative GA re-optimization to eliminate crosstalk
- Final aggregation into the comprehensive Vfam database

## Usage

Vfam can be used to identify VFG-like open reading frames (ORFs) in your protein sequence data using the HMMER.

### Prerequisites
1.  **Install HMMER**: Ensure that HMMER (v3.4 or later) is installed and available in your `PATH`.
    *   Download and installation instructions can be found on the [HMMER website](http://hmmer.org/).

2.  **Download the Vfam Database**: The Vfam HMM profiles are required for the search.
    *   You can download the pre-built `Vfam.hmm` file.

### Step-by-Step Guide

1.  **Prepare the HMM Database**:
    Before the first use, you need to press the HMM file into a binary format for faster scanning.
    ```bash
    hmmpress Vfam.hmm
    ```
    This command will generate several additional files (`.h3m`, `.h3i`, `.h3f`, `.h3p`).

2.  **Search Your Sequences**:
    Use the `hmmscan` command to search your protein FASTA file against the Vfam database.
    ```bash
    hmmscan --domtblout results.domtblout Vfam.hmm your_sequences.faa
    ```
    *   `--domtblout results.domtblout`: Saves the detailed domain table output to a file named `results.domtblout`.
    *   `Vfam.hmm`: The pressed Vfam database.
    *   `your_sequences.faa`: Your input file containing protein sequences in FASTA format.

3.  **Interpret the Results**:
    The `results.domtblout` file is a tab-separated table. Key columns include:
    *   **Target Name**: The name of the Vfam HMM profile (e.g., `Vfam_CTX_001`).
    *   **Query Name**: The name of the sequence from your input file that matched.
    *   **E-value**: The expectation value, lower values indicate more significant matches.
    *   **Bitscore**: The bit score of the match.
      
## Applications

- Virulence factor annotation in bacterial genomes
- Metagenomic analysis of pathogenicity potential
- Comparative genomics of virulence mechanisms
- Microbial risk assessment in clinical and environmental samples

## Citation

If you use Vfam in your research, please cite our publication:

---

*Vfam enables reliable and specific detection of virulence factors, supporting research in microbial pathogenesis and genomic epidemiology.*
