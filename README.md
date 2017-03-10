# Galaxy-workflow-for-scRNA-seq

This workflow is for single cell RNAseq analysis in Galaxy. The workflow currently operates on a single collection (a population) of single cell data, with each cell bring imported as an individual SRR sample. 


In brief, the workflow trims the ends of reads to remove bases of poor quality, then maps reads with HISAT. The reads are quantified against a transcriptome database (GTF format, can be downloaded from UCSC table browser, or generated separately using Cuffmerge based on bulk RNA-seq data) using Stringtie, enabling generation of the "gene abundance estimation output file". This gene estimation output is cut to only keep the gene ID and FPKM value. This collection is then collapsed to generate a **complete table of all gene FPKM values per gene per cell** (no filtering). The cut collection is then filtered to only keep genes with FPKM > 1 and then the collection is collapsed to a single file. This file is grouped based on gene ID and also counted to provide the number of cells that each gene is expressed (FPKM > 1) in. In parallel, a the number of cells analyzed is counted (by counting columns of the **complete table of all gene FPKM values per gene per cell**) and joined to the grouped output. The percent of cells expressing each gene is computed and subsequently filtered to only keep transcripts expressed in > 10% of cells in the initial population. This filtered list of expressed genes is compared to the **complete table of all gene FPKM values per gene per cell** to return a **table of expressed genes in each cell**.

Note: This workflow uses two non-canonical Galaxy tools - "Column Join on Collections" and "Flatten Collection into a flat list of datasets" that are not found on useGalaxy.org, yet. 

See below for a schematic representation of this workflow.



![](/schematic_of_scRNA-seq_pipeline.png)









Please contact me with questions or feel free to create an issue for this repository. 
