# SynNet-Py
The code was used in our rice genome evolution [paper](https://doi.org/10.1101/2024.05.29.596369) to generate microsynteny gene clusters. The main function is:
1) to process and clean the pangene table from GENESPACE;
2) to identify syntenic gene clusters

The output then can be used as input for plotting in the R package [syntenet](https://github.com/almeidasilvaf/syntenet).

The whole pipeline is represented in the jupyter notebook; Only python3 and pandans module are required to run the scripts; for how to run GENESPACE, please visit [Genespace](https://github.com/jtlovell/GENESPACE)

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


