# Rice Phylogenomics
The code was used in our rice genome evolution [paper](https://doi.org/10.1101/2024.05.29.596369) to generate microsynteny gene clusters and to make phylogeny based on the clusters. The main function is:
1) to process and clean the pangene table from GENESPACE;
2) to identify syntenic gene clusters;
3) to infer gene trees and phylogeny of (sub)genomes

### Installation
The whole pipeline is organised in Jupyter notebook; Python3 and Pandans are required to run the scripts; In addition, the following tools need to be callable from working envitonment: [GENESPACE ](https://github.com/jtlovell/GENESPACE), [MAFFT](https://mafft.cbrc.jp/alignment/server/index.html), [trimAl](https://trimal.cgenomics.org/), [IQ-TREE](http://www.iqtree.org/), and [Astral-Pro](https://github.com/chaoszhang/A-pro)

### Example
The computed rice pangenome data is used as an example to demonstrate the pipeline
#### 1. run GENESPACE on your genomes, and use the following settings in **query_pangenes()** to output pangenome:
```R
pangenome <- query_pangenes(
  gsParam,
  bed = NULL,
  refGenome = Reference,
  transform = TRUE,
  showArrayMem = FALSE,
  showNSOrtho = FALSE,
  maxMem2Show = Inf,
  showUnPlacedPgs = FALSE)
```
The ouput is a plain text table of all homologous groups identifed by GENESPACE, whcih will be used in next step.
#### 2. With the pangene table generated from GENESPACE, run SynCluster to identify syntenic gene clusters 

```python
import os
import pandas as pd
from modules import prefix_cell,pangenome_cleaner,parse_pangenome

pangenome = "pangenome.txt"
all = "pangenome_all.txt"
syn = "pangenome_syn.txt"
synnet = "pangenome_synnet.txt"

clean_pangenome = pangenome_cleaner(pangenome)
parse_pangenome(clean_pangenome,all,syn,synnet)
```
The outputs are three plain text tables: the cleaned homologous groups, the homologous groups with only syntenic genes and the syntenic gene pairs.
#### 3. explore the syntenic gene clusters in [syntenet](https://github.com/almeidasilvaf/syntenet)
#### 4. Generate FASTA sequences for each syntenic gene cluster


