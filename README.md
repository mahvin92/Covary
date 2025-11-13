<img width="200" height="200" alt="Covary-vertical" src="https://github.com/user-attachments/assets/53c15c6a-d6f6-45c4-ab55-1cc22619618b" />

# Covary
Covary is a computational framework designed for large-scale biological sequence analysis, powered by [TIPs-VF](https://doi.org/10.1101/2025.02.15.637782). It leverages alignment-free, translation-aware embeddings to compare, cluster, and analyze genetic sequences, enabling insights into phylogenetic relationships, functional divergence, and taxonomic resolution.

## Features
1. Alignment-free analysis: Circumvents computationally expensive multiple sequence alignments (MSA), enabling scalable analyses for large datasets.
2. Translation-aware embeddings: Incorporates codon-bound information for biologically meaningful sequence comparison, works both in coding and non-coding sequences.
3. Distance-based clustering: Computes embeddings and distance matrices for downstream clustering and visualization.
4. Taxonomic resolution: Capable of resolving sequences at multiple taxonomic levels, including species, genus, family and order.
5. Flexible input formats: Supports multi-FASTA file from a variety of organisms.
6. Visualization support: Generate distance heatmaps, cluster trees, and embedding projections.

## Current release
v2.1 (For information about version changes, please see [releases](https://github.com/mahvin92/Covary/releases))

## Performing an analysis
Note that Covary was tested and benchmarked on Google Colab. While Covary is compatible with Colab, Google retains ownership of the platform.
You may use Covary within your own Colab environment subject to Google’s Terms of Service.

### 1. Prepare your multi-FASTA file
Sample format:
```
>NR_181868.1 Thermus brevis strain SYSU G05001 16S ribosomal RNA, partial sequence
GACATGCAAGTCGAGCGGGGCGGGTTTATACCTGCCCAGCGGCGGACGGGTGAGTAACGC
GTGGGTGACCTACCTGGAAGAGGCGGACAACCTGGGGAAACCCAGGCTAATCCGCCATGT
GGTCCTGTCCTGTGGGGCAGGACTAAAGGGTGGATAGCCCGCTTCCGGATGGGCCCGCGT
CCCATCAGCTAGTTGGTGGGGTAAGAGCCCACCAAGGCGACGACGGGTAGCCGGTCTGAG

>NR_181790.1 Thermus brevis strain SYSU G05001 16S ribosomal RNA, partial sequence
GACATGCAAGTCGAGCGGGGCGGGTTTATACCTGCCCAGCGGCGGACGGGTGAGTAACGC
GTGGGTGACCTACCTGGAAGAGGCGGACAACCTGGGGAAACCCAGGCTAATCCGCCATGT
GGTCCTGTCCTGTGGGGCAGGACTAAAGGGTGGATAGCCCGCTTCCGGATGGGCCCGCGT
CCCATCAGCTAGTTGGTGGGGTAAGAGCCCACCAAGGCGACGACGGGTAGCCGGTCTGAG

>NR_180714.1 Thermus sediminis strain L198 16S ribosomal RNA, partial sequence
GACATGCAAGTCGTGCGGGCCGTGGGGTTTCTCACGGCTAGCGGCGGACGGGTGAGTAAC
GCGTGGGTGACCTACCCGGAAGAGGGGGACAACCTGGGGAAACCCAGGCTAATCCCCCAT
GTGGACGCATCCTGTGGGGTGCGTTCAAAGGGCGTTGCCCGCTTCCGGATGGGCCCGCGT
CCCATCAGCCAGTTGGTGGGGTAAAGGCCCACCAAGGCGACGACGGGTAGCCGGTCTGAG
```

### 2. Load/import Covary on Colab or open the shared notebook link
- [View Covary notebooks here](https://github.com/mahvin92/Covary/tree/main/notebook)
- [Load Covary v2.1 on Colab here](https://colab.research.google.com/drive/1wZ0hmDZzAlQkHALUbrN0txkUVCJssReZ)

*Note: Ensure that you are using the most recent version of Covary by checking the releases [here](https://github.com/mahvin92/Covary/releases) or on the [website](https://covary.chordexbio.com/covary-releases)*

Alternatively, you can programatically load Covary from Colab. For example, you can open v2.1 using:
```
from IPython.display import HTML

notebook = "Covary_v2_1.ipynb" # -> change the version here
repo = "mahvin92/Covary"
folder = "notebook"

colab_url = f"https://colab.research.google.com/github/{repo}/blob/main/{folder}/{notebook}"
HTML(f'<a href="{colab_url}" target="_blank">Open {notebook} in Google Colab</a>')

```

### 3. Run Covary
- Covary can be executed using default parameters directly by clicking ```Runtime``` -> ```Run all```
- Fields marked with '⚠️' may require your attention or input, please don't collapse them while running Covary.
- **Upload your multi-FASTA file in ```Step 2```**
- Fine-tune the run by modifying Covary parameters in ```Step 1. Set parameters```

### 4. View results
Results are automatically generated after the run. If download does not start, manually download the results from the Files browser ```/content/covary_results```

The result zip file contains:
1. Vector embeddings: Numerical data in .tsv format for PCA, t-SNE, and UMAP.
2. Vector embedding plots: Scatter plots of Dim-1 vs. Dim-2, labeled by sequence entry.
3. Heatmap (pairwise distance plot): Euclidean pairwise distance plots, provided alongside each reduction analysis.
4. Dendrogram linkages: Numerical data in .tsv format for linkage analyses (Ward, Average, Complete, Single) across PCA, t-SNE, and UMAP.
5. Dendrogram plots: Visualizations showing distances (x-axis) and sequence indices (y-axis) across different linkage methods and reduction analyses.

## Use cases
**Classification:** Involves grouping sequences into defined categories or taxonomic ranks. Covary classifies genetic samples by comparing their embeddings against established or reference clades, enabling rapid placement into evolutionary lineages. *For example, researchers can classify newly sequenced bacterial strains to determine whether they belong to existing species or represent novel taxa.*

**Identification:** Focuses on recognizing the origin or species of a genetic sequence. Covary can accurately identify unknown samples by matching them to the closest evolutionary signatures in its reference set, provided uniform sequences are used. *For example, identification can be applied in pathogen surveillance to pinpoint the source of an emerging viral outbreak.*

**Relationship:** Seeks to determine evolutionary connections between sequences. Covary reconstructs phylogenetic trees that reveal lineage divergence, ancestry, and clonal evolution, providing a map of how organisms or mutations are connected. *For example, this can be used to trace tumor clonal evolution and understand how different subclone genotypes may emerge during cancer progression.*

**Prediction:** Estimates potential evolutionary outcomes or mutational trajectories. Covary can forecast likely future variants or clonal progressions, supporting applications in epidemiology and cancer research. *For example, predictive workflows can model how viral genomes might evolve anti-viral resistance or how tumor mutations may drive treatment relapse.*

## FAQs

## Troubleshooting
1. Check that the runtime type is set to GPU at "Runtime" -> "Change runtime type".
2. Try to restart the session "Runtime" -> "Factory reset runtime".
3. Check your input sequence for the presence of invalid sequence characters or white spaces. Note that Covary-encoder can only represent A, T, C, G, N sequences to reduce ambiguity factors that may influence the deep learning results. Limit the use of non-conventional DNA sequences, as much as possible, and resolve sequence data using a reference assembly. Newer versions of Covary (e.g., v.2.0 and above) have added QC check step that removes whitespaces and filter param that is set to ignore/remove data/sequence entry containing invalid sequences prior to representation; see ```Steps 1 and 4```.
4. Pre-process your data, when needed. Most problems with non-ATCGN in Covary encoder can be fixed by running your data first in the 'clean_seq.py' that can be downloaded from [TIPs-VF GitHub](https://github.com/mahvin92/TIPs-VF). Newer versions of Covary (e.g., v.2.0 and above) have incorporated this workflow; see ```Steps 1 and 4```.
5. If download failed to start, rerun ```Step 8```.

## Reporting
Comments and suggestions to improve Covary are welcome. If you find any bug or problem, please open an [issue](https://github.com/mahvin92/Covary/issues/new).

## License notice
Please see updated license [here](https://github.com/mahvin92/Covary/blob/main/LICENSE)

## Acknowledgement
Covary is powered by [TIPs](https://tips.chordexbio.com/), [ChordexBio](https://chordexbio.com/), [Covary encoder](https://github.com/mahvin92/Covary-encoder) and [CodeEnigma](https://github.com/KrishnanSG/codeenigma), made with Python, and tested using Google Colab ❤️

