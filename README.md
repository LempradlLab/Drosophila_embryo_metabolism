# Drosophila_embryo_metabolism

These are custom scripts used downstream of our [single embryo variant calling pipeline](https://github.com/vari-bbc/scRNAseq/tree/main) in 'cellseq192' mode to produce the results reported in our manuscript entitled "Single-embryo metabolomics reveals developmental metabolism in the early Drosophila embryo".

## infer_parental_origin.Rmd

This script takes as input, the allelic depths in our 'analysis/variant_calling/11a2_extract_ADs/all.merged.filt.PASS.snpeff_inGene.AD.parsed.table' output file of the [single embryo variant calling pipeline](https://github.com/vari-bbc/scRNAseq/tree/main) in 'cellseq192' mode, a VCF file containing filtered [DGRP2](http://dgrp2.gnets.ncsu.edu/) SNPs and the fasta file for the dm6 reference genome. It performs quality filters and categorizes allele counts into paternal or maternal based on the parental genotypes indicated in the VCF file. The DGRP variants are assumed to be pre-filtered for just the two parental lines, removing multiallelic variants, keeping only SNPs, and removing variants that were not variant in either line (`bcftools view --samples line_737,line_352 --max-alleles 2 --types snps --min-ac=1 --trim-alt-alleles`). 

## WGCNA_workflow.Rmd

This .Rmd file contains code to run WGCNA for Drosophilia single embryo rna-seq data as well as correlating module eigen genes with mass-spec metabolic data. Data contain male and female flies in pseduo-time order. Generalized additve models are used to both remove large outliers in the metabolic data to focus regression estimates closer to the population mean. Genearlized additive models are also used to identify the transcription activation (the earliest pseudotime with 95% confidence the mean gene expression is >1). The workflow can take awhile to run. Also be sure to see the soft power and type of correlation (eg signed-hybrid) that best suits your data. The workflow will output a series of .csvs that make plotting in other softwares easier.
