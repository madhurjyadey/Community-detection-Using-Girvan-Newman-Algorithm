# Community Detection using Girvan-Newman Algorithm

> **An Experiential Analysis of Community Detection by applying Girvan-Newman Algorithm**

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![NetworkX](https://img.shields.io/badge/NetworkX-Graph%20Library-orange)](https://networkx.org/)
[![Gephi](https://img.shields.io/badge/Gephi-Visualization-purple)](https://gephi.org/)
[![License](https://img.shields.io/badge/License-Academic-green)]()

---

## Authors

| Name | Affiliation |
|------|-------------|
| Madhurjya Dey | Dept. of CSE, Royal School of Engineering and Technology, The Assam Royal Global University, Guwahati |
| Chinmoy Hazarika | Dept. of CSE, Royal School of Engineering and Technology, The Assam Royal Global University, Guwahati |
| Nichol Das | Dept. of CSE, Royal School of Engineering and Technology, The Assam Royal Global University, Guwahati |
| Dr. Deepjyoti Choudhury *(Corresponding Author)* | Dept. of CSE, Royal School of Engineering and Technology, The Assam Royal Global University, Guwahati |
| Surendra Solanki | Dept. of AIML, School of CSE, Manipal University Jaipur |

---

## Abstract

Community detection is a method that divides networks into meaningful clusters, revealing hidden structural patterns useful for real-world network analysis. This paper applies the **Girvan-Newman algorithm** — an edge betweenness-based community splitting technique — to five real-world benchmark datasets using the **NetworkX** library. Performance is evaluated using Accuracy, Precision, Recall, F1-Score, NMI, ARI, and Modularity. Network visualizations are produced using **Gephi** to clearly distinguish identified communities.

---

## Table of Contents

- [Introduction](#introduction)
- [Methodology](#methodology)
  - [Performance Metrics](#performance-metrics)
  - [Algorithm Overview](#algorithm-overview)
  - [Datasets](#datasets)
  - [Experimental Setup](#experimental-setup)
- [Results](#results)
- [Conclusion](#conclusion)
- [References](#references)

---

## Introduction

Community detection refers to the clustering or grouping of nodes within a network to reveal important patterns or relationships. This task is harder in dynamic networks than static ones due to multi-graph structures and evolving node relationships.

This work applies the Girvan-Newman algorithm to well-known benchmark graph datasets available in the NetworkX library. The algorithm iteratively removes edges with the highest betweenness centrality, progressively uncovering tightly-knit community structures — representable as a dendrogram.

---

## Methodology

### Performance Metrics

| Metric | Description |
|--------|-------------|
| **Accuracy** | Ratio of correct predictions to total predictions: `(TP + TN) / (TP + TN + FP + FN)` |
| **Precision** | Fraction of predicted community memberships that are correct: `TP / (TP + FP)` |
| **Recall** | Fraction of true community members correctly identified: `TP / (TP + FN)` |
| **F1-Score** | Harmonic mean of Precision and Recall: `2 × (Precision × Recall) / (Precision + Recall)` |
| **NMI** | Normalized Mutual Information — measures information shared between detected and ground truth communities (0 = unrelated, 1 = perfect match) |
| **ARI** | Adjusted Rand Index — stricter pairwise comparison of detected vs. true communities (0 = random, 1 = perfect) |
| **Modularity (Q)** | Graph-internal measure; high Q indicates strong community structure without requiring ground truth |

### Algorithm Overview

The **Girvan-Newman Algorithm** identifies communities through iterative edge removal:

1. Compute betweenness centrality for all edges in the network.
2. Remove the edge with the **highest betweenness centrality**.
3. Recalculate betweenness centrality for all remaining edges.
4. Repeat steps 2–3 until all edges are removed or only one node remains.

Edges bridging communities naturally have high betweenness centrality, so removing them progressively exposes the underlying cluster structure.

### Datasets

All five datasets are sourced from the **NetworkX** library and come with ground truth community labels, making evaluation straightforward.

| # | Dataset | Nodes | Edges | Communities (Ground Truth) |
|---|---------|-------|-------|---------------------------|
| 1 | Zachary Karate Club | 34 | 78 | 2 |
| 2 | American College Football Network | 115 | 613 | 12 |
| 3 | Bottlenose Dolphin Network | 62 | 159 | 3 |
| 4 | Florentine Families | 16 | 20 | 4 |
| 5 | Napoleon Russian Campaign | 20 | 19 | 5 |

All datasets are **undirected and unweighted**.

**Dataset descriptions:**

- **Zachary Karate Club** — Models social interactions among 34 club members; famously split into two communities following a dispute between the instructor and president.
- **American College Football Network** — Encodes regular-season games among Division IA college football teams.
- **Bottlenose Dolphin Network** — Captures long-lasting social associations among dolphins in Doubtful Sound, New Zealand.
- **Florentine Families** — Represents social, business, and marriage ties among prominent Renaissance Florence families (14th–15th century).
- **Napoleon Russian Campaign** — Represents diplomatic and military alliances among European states during the 1812 Russian invasion.

### Experimental Setup

- **Language:** Python
- **Hardware:** AMD Ryzen 7 6800H, 16 GB RAM
- **Key Libraries:** NetworkX, Gephi (visualization)

---

## Results

### Performance Summary

| # | Dataset | Precision | Recall | Accuracy | F1-Score | NMI | ARI | Modularity |
|---|---------|-----------|--------|----------|----------|-----|-----|------------|
| 1 | Zachary Karate Club | 89.4 | 100.0 | 94.1 | 94.4 | 73.2 | 77.1 | 34.7 |
| 2 | American College Football Network | 89.4 | 100.0 | 94.1 | 94.4 | 92.3 | 89.5 | 59.3 |
| 3 | Bottlenose Dolphin Network | 93.7 | 96.7 | 96.7 | 95.2 | 90.8 | 91.7 | 37.8 |
| 4 | Florentine Families | 75.6 | 73.3 | 73.3 | 73.0 | 57.8 | 36.0 | 39.7 |
| 5 | Napoleon Russian Campaign | 75.0 | 100.0 | 84.0 | 85.7 | 49.4 | 45.2 | 35.3 |

### Community Predictions vs. Ground Truth

| Dataset | Predicted Communities | Ground Truth Communities | Modularity |
|---------|-----------------------|--------------------------|------------|
| Zachary Karate Club | 5 | 2 | 34.7 |
| American College Football Network | 10 | 12 | 59.3 |
| Bottlenose Dolphin Network | 5 | 3 | 37.8 |
| Florentine Families | 4 | 4 | 39.7 |
| Napoleon Russian Campaign | 6 | 5 | 35.3 |

### Key Observations

- **High-performing datasets** (Zachary Karate Club, American College Football, Bottlenose Dolphins) exhibit well-defined community structures with moderate density and minimal community overlap.
- **Lower-performing datasets** (Florentine Families, Napoleon Russian Campaign) suffer from sparse connectivity, irregular degree distributions, and overlapping communities, which hinder the algorithm's ability to clearly distinguish clusters.
- The American College Football Network achieved outstanding ROC-AUC scores (mean AUC = 99.5, per-class AUC = 100), demonstrating near-perfect classification on structured data.
- The Napoleon Russian Campaign dataset showed the weakest AUC (43.7), below the random classifier baseline, indicating very weak underlying community structure.

---

## Conclusion

The Girvan-Newman algorithm effectively detects communities in small-to-medium-sized networks by iteratively removing high-betweenness edges and producing interpretable hierarchical splits. However, its `O(m²n)` time complexity makes it computationally expensive for large-scale networks.

Scalable alternatives such as **Louvain**, **Leiden**, **Label Propagation**, and **Spectral Clustering** offer better efficiency with competitive performance. Future work will focus on:

- Integration with large-scale real-world networks
- Combining the algorithm with other traditional community detection methods
- Applying **machine learning and deep learning models** for enhanced community detection

---

## References

1. Zachary WW. An information flow model for conflict and fission in small groups. *Journal of Anthropological Research*. 1977;33(4):452–73. DOI: [10.1086/jar.33.4.3629752](https://doi.org/10.1086/jar.33.4.3629752)

2. Newman ME, Girvan M. Finding and evaluating community structure in networks. *Physical Review E*. 2004;69(2):026113. DOI: [10.1103/PhysRevE.69.026113](https://doi.org/10.1103/PhysRevE.69.026113)

3. Lusseau D, et al. The bottlenose dolphin community of doubtful sound features a large proportion of long-lasting associations. *Behavioral Ecology and Sociobiology*. 2003;54(4):396–405. DOI: [10.1007/s00265-003-0651-y](https://doi.org/10.1007/s00265-003-0651-y)

4. Padgett JF, Ansell CK. Robust Action and the Rise of the Medici, 1400-1434. *American Journal of Sociology*. 1993;98(6):1259–319. DOI: [10.1086/230190](https://doi.org/10.1086/230190)

5. Freeman L. The development of social network analysis. *A Study in the Sociology of Science*. 2004.

6. Javed MA, et al. Community detection in networks: A multidisciplinary review. *Journal of Network and Computer Applications*. 2018;108:87–111. DOI: [10.1016/j.jnca.2018.02.011](https://doi.org/10.1016/j.jnca.2018.02.011)

7. Huang LC, et al. Community detection in dynamic social networks: A random walk approach. *ASONAM 2011*. DOI: [10.1109/ASONAM.2011.28](https://doi.org/10.1109/ASONAM.2011.28)

8. Girvan M, Newman ME. Community structure in social and biological networks. *PNAS*. 2002;99(12):7821–7826. DOI: [10.1073/pnas.122653799](https://doi.org/10.1073/pnas.122653799)

9. Nasrullah S, Jalali A. Detection of Types of Mental Illness through the Social Network Using Ensembled Deep Learning Model. *Computational Intelligence and Neuroscience*. 2022. DOI: [10.1155/2022/9404242](https://doi.org/10.1155/2022/9404242)

10. Lancichinetti A, Fortunato S, Kertész J. Detecting the overlapping and hierarchical community structure in complex networks. *New Journal of Physics*. 2009;11(3):033015. DOI: [10.1088/1367-2630/11/3/033015](https://doi.org/10.1088/1367-2630/11/3/033015)

11. Newman ME. Fast algorithm for detecting community structure in networks. *Physical Review E*. 2004;69(6):066133. DOI: [10.1103/PhysRevE.69.066133](https://doi.org/10.1103/PhysRevE.69.066133)

12. Sathiyakumari K, Vijaya MS. Community detection based on Girvan Newman algorithm and link analysis of social media. *Annual Convention of CSI*. 2016. DOI: [10.1007/978-981-10-3376-6_18](https://doi.org/10.1007/978-981-10-3376-6_18)

13. Choudhury D, Bhattacharjee S, Das A. An empirical study of community and sub-community detection applying Newman-Girvan algorithm. *ICETACS 2013*. DOI: [10.1109/ICETACS.2013.6691420](https://doi.org/10.1109/ICETACS.2013.6691420)

14. Permani AR, Narayan S. Community Detection using Girvan Newman algorithm in Recommendation systems. 2022;10:2.

15. Matijevic T, et al. Performance Analysis of Girvan-Newman Algorithm on Different Types of Random Graphs. *CECIIS 2016*.

---

## Citation

If you use this work, please cite:

```bibtex
@inproceedings{dey2024girvan,
  title     = {An Experiential Analysis of Community Detection by applying Girvan-Newman Algorithm},
  author    = {Dey, Madhurjya and Hazarika, Chinmoy and Das, Nichol and Choudhury, Deepjyoti and Solanki, Surendra},
  booktitle = {CRC Paper ID 1144},
  year      = {2024},
  institution = {The Assam Royal Global University, Guwahati}
}
