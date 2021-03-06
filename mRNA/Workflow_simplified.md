Differential microRNA expression
--------------------------------------

#### Analysis workflow

Reads were mapped to the GRC37 reference sequence with `tophap2`. Duplicates
and non-unique reads were removed using `samtools`. Counts per gene were
assigned using `htseq-count`. Differential expression analysis was performed
with `DESeq2`.


#### Quality control

Eight mRNA samples were sequenced on HiSeq4000 using paired-edn sequencing
protocol (2x75bp). Data quality looks good, more than 10 mln reads mapped to
known genes for each samples, average duplication rate 25%.


| sequencing id    | sample name | sequenced reads | mapped reads | nodup reads | uniq reads | reads mapped to genes | % reads mapped to genes of nodup |
| ---------------- | ----------------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---- |
| WTCHG_260126_201 | miR-cont1 (Kim)    | 33,118,323 | 28,940,226 | 22,861,259 | 20,903,213 | 18,655,111 | 81.6 |
| WTCHG_260126_202 | miR-cont2 (Jeon)   | 40,382,477 | 35,098,464 | 26,064,426 | 23,685,281 | 22,279,843 | 85.5 |
| WTCHG_260126_203 | miR-cont3 (Paul)   | 36,883,161 | 31,867,272 | 23,090,486 | 20,716,797 | 20,086,531 | 87   |
| WTCHG_260126_204 | miR-cont4 (L-cone) | 32,600,347 | 28,311,673 | 21,460,462 | 19,431,429 | 18,548,390 | 86.4 |
| WTCHG_260126_205 | miR-10b1 (Kim)     | 35,065,691 | 30,709,386 | 24,134,327 | 22,100,297 | 19,870,114 | 82.3 |
| WTCHG_260126_206 | miR-10b2 (Jeon)    | 37,596,944 | 32,653,080 | 24,289,556 | 22,019,957 | 20,762,385 | 85.5 |
| WTCHG_260126_207 | miR-10b3 (Paul)    | 38,668,642 | 33,371,257 | 23,685,806 | 21,237,491 | 20,725,176 | 87.5 |
| WTCHG_260126_208 | miR-10b4 (L-cone)  | 37,182,862 | 32,017,247 | 23,593,110 | 21,280,150 | 20,862,969 | 88.4 |


#### Differential expression analysis

Unfortunately differential gene expression analysis did not discover any
significant hits. All genes had p-values between 0.01 and 0.99 and adjusted
p-values of 0.99. When we looked at the correlation between each gene
expression under two conditions (miR-cont and miR-10b), we saw that there was
indeed almots now difference in gene expression (Pearson correlation
coefficient 0.9995 with p-value < 2.2e-16).

![alt text](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/gene_expression_correlation.png)

When we look at the fold change, we can see that the vast majority of genes
have a fold change around 1; a handful of genes which has higher/lower fold
change are extremely lowly expressed genes (which, therefore, also were not
significantly different).

![alt text](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/fold_change.png)


Differential expression analysis results can be found
[here](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/miR-10b.miR-cont.DE_results.txt).
Normalized gene expression can be found
[here](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/miR-10b.miR-cont.normalized_counts.txt).

Nevertheless, here are all genes which did not pass multiple testing correction
but have non-corrected p-value < 0.05.

| Gene id | Gene name | miR-10b expression | miR-cont expression | Fold change | DESeq2 log2 fold change | Manual log2 fold change | P value |
| ------------------ | ------------- | ---- | ---- | ---- | ----- | ----- | ----- |
| ENSG00000083454.17 | P2RX5         | 361  | 427  | 0.85 | -0.14 | -0.24 | 0.033 |
| ENSG00000112715.16 | VEGFA         | 165  | 292  | 0.57 | -0.09 | -0.82 | 0.033 |
| ENSG00000119725.13 | ZNF410        | 11   | 20   | 0.55 | -0.08 | -0.86 | 0.043 |
| ENSG00000126934.9  | MAP2K2        | 1024 | 1136 | 0.9  | -0.12 | -0.15 | 0.042 |
| ENSG00000151414.10 | NEK7          | 3526 | 3872 | 0.91 | -0.11 | -0.14 | 0.036 |
| ENSG00000155729.8  | KCTD18        | 564  | 656  | 0.86 | -0.16 | -0.22 | 0.01  |
| ENSG00000161642.13 | ZNF385A       | 20   | 38   | 0.53 | -0.09 | -0.93 | 0.025 |
| ENSG00000162368.9  | CMPK1         | 4598 | 5611 | 0.82 | -0.16 | -0.28 | 0.016 |
| ENSG00000165891.11 | E2F7          | 414  | 514  | 0.81 | -0.16 | -0.31 | 0.023 |
| ENSG00000169955.6  | ZNF747        | 258  | 306  | 0.84 | -0.14 | -0.25 | 0.038 |
| ENSG00000181038.9  | METTL23       | 341  | 397  | 0.86 | -0.13 | -0.22 | 0.044 |
| ENSG00000185133.9  | INPP5J        | 3    | 0    | inf  |  0.03 | inf   | 0.043 |
| ENSG00000187045.12 | TMPRSS6       | 23   | 48   | 0.48 | -0.08 | -1.06 | 0.028 |
| ENSG00000188993.3  | LRRC66        | 3    | 9    | 0.33 | -0.06 | -1.58 | 0.038 |
| ENSG00000196312.7  | HIATL2        | 41   | 57   | 0.72 | -0.12 | -0.48 | 0.043 |
| ENSG00000211666.2  | IGLV2-14      | 5    | 0.2  | 25   |  0.04 | 4.64  | 0.025 |
| ENSG00000211943.2  | IGHV3-15      | 0    | 3    | 0    | -0.03 | Inf   | 0.04  |
| ENSG00000225193.5  | RPS12P26      | 3    | 0    | inf  |  0.03 | Inf   | 0.035 |
| ENSG00000233833.1  | ETF1P3        | 60   | 43   | 1.4  |  0.12 | 0.48  | 0.038 |
| ENSG00000259469.1  | RP11-227D13.4 | 2    | 7    | 0.29 | -0.05 | -1.81 | 0.047 |

Please note that **manual log2 fold change** can differ from
**DESeq2 log2 fold change**. This happens because DESeq2 gives an *estimate* of
log2 fold change and considers things like coverage per condition, average
coverage, standard deviation of coverage in each sample within each condition,
overall average coverage.

More is written [here](http://biorxiv.org/content/early/2014/11/17/002832),
where guys who developed DESeq2 give examples of how and why their estimated
fold change turns to be more realistic when you start validating your RNA-Seq
findings with, e.g., qPCR. This means that when we want to get/give an idea of
fold change between the two conditions that we sequenced, we should use this
estimated log2FC.

A couple of examples:

- when manual log2FC (-0.82) is very different from the estimated log2FC
  (-0.09): gene VEGFA -- in both conditions the gene has enough coverage,
  however, the standard deviation of coverage in the second condition is *174*
  -- more than half of the average coverage (292)
- when manual logFC (-0.15) is very similar to the estimated log2FC (-0.15):
  gene MAP2K2 -- high coverage in both conditions (1024 against 1136) plus the
  standard deviation of coverage in both conditions is between 25 and 45, less
  than 4% of gene expression.

#### Gene expression heatmap for selected genes

Heatmaps showing the similarity between the samples based on certain gene
expression patterns can be found
[here](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/gene_expression.heatmap.pdf).


On each heatmap, one cell represents the fold change (e.g., fold change in gene
expression in control sample1 vs miR sample1). Colors range from blue (lower
fold changes) to yellow (higher fold changes). "ctrl" implies control samples
("ctrl1" for control sample 1), "miR" means samples with miRNA. 25 genes were
analyzed -- 20 genes with significant P-Values (note! q-values were not
significant) and 5 genes of interest that are listed in the next section.


#### Pathway analysis in top 100 genes

[Top 100](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/gene_list_for_pathway_analysis.txt)
(based on p-value) genes were selected for pathway analysis. Note that none of
these genes passed multiple testing correction, so pathway analysis was run for
the purpose of classification -- to see which genes are annotated to which
functional categories. Gene Onthology analysis (a.k.a. GO terms) was performed.

26 out of selected 100 genes were assigned to a pathway or a fuctional category:

![alt text](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/pathway_analysis.png)

These are the results of GO analysis:

| mapped ids | Gene name and gene symbol | Panther family | Panther protein class |
| ---------- | ------------------------- | -------------- | --------------------- |
| ENSG00000145911 | "NEDD4-binding protein 3" | NEDD4-BINDING PROTEIN 3 (PTHR32274:SF1) | - |
| ENSG00000101213 | "Protein-tyrosine kinase 6" | PROTEIN-TYROSINE KINASE 6 (PTHR24418:SF265) | "non-receptor tyrosine protein kinase non-receptor tyrosine protein kinase" |
| ENSG00000196312 | "Hippocampus abundant transcript-like protein 2" | HIPPOCAMPUS ABUNDANT TRANSCRIPT-LIKE PROTEIN 1-RELATED (PTHR23504:SF32) | - |
| ENSG00000181038 | "Methyltransferase-like protein 23" | METHYLTRANSFERASE-LIKE PROTEIN 23 (PTHR14614:SF2) | - |
| ENSG00000244607 | "Coiled-coil domain-containing protein 13" | COILED-COIL DOMAIN-CONTAINING PROTEIN 13 (PTHR31935:SF1) | - |
| ENSG00000188993 | "Leucine-rich repeat-containing protein 66" | LEUCINE-RICH REPEAT-CONTAINING PROTEIN 66 (PTHR24369:SF90) | "cytokine receptor extracellular matrix protein" |
| ENSG00000164070 | "Heat shock 70 kDa protein 4L" | HEAT SHOCK 70 KDA PROTEIN 4L (PTHR19375:SF161) | Hsp70 family chaperone |
| ENSG00000102302 | "FYVE, RhoGEF and PH domain-containing protein" | FYVE, RHOGEF AND PH DOMAIN-CONTAINING PROTEIN 1 (PTHR12673:SF79) | guanyl-nucleotide exchange factor |
| ENSG00000179477 | "Arachidonate 12-lipoxygenase, 12R-type" | ARACHIDONATE 12-LIPOXYGENASE, 12R-TYPE (PTHR11771:SF40) | oxygenase |
| ENSG00000182687 | "Galanin receptor type 2" | GALANIN RECEPTOR TYPE 2 (PTHR24230:SF13) | G-protein coupled receptor |
| ENSG00000162368 | "UMP-CMP kinase" | UMP-CMP KINASE (PTHR23359:SF107) | "nucleotide kinase nucleotide kinase" |
| ENSG00000258405 | "Zinc finger protein 578" | ZINC FINGER PROTEIN 578 (PTHR24407:SF16) | - |
| ENSG00000225556 | "C2 calcium-dependent domain-containing protein 4D" | C2 CALCIUM-DEPENDENT DOMAIN-CONTAINING PROTEIN 4D (PTHR10024:SF179) | membrane trafficking regulatory protein |
| ENSG00000135517 | "Lens fiber major intrinsic protein" | LENS FIBER MAJOR INTRINSIC PROTEIN (PTHR19139:SF39) | "transporter transfer/carrier protein" |
| ENSG00000186767 | "Spindlin-4" | SPINDLIN-4 (PTHR10405:SF9) | - |
| ENSG00000155980 | "Kinesin heavy chain isoform 5A" | KINESIN HEAVY CHAIN ISOFORM 5A (PTHR24115:SF317) | microtubule binding motor protein |
| ENSG00000166920 | "Normal mucosa of esophagus-specific gene 1 protein" | NORMAL MUCOSA OF ESOPHAGUS-SPECIFIC GENE 1 PROTEIN (PTHR14256:SF3) | oxidoreductase |
| ENSG00000138495 | "Cytochrome c oxidase copper chaperone" | CYTOCHROME C OXIDASE COPPER CHAPERONE (PTHR16719:SF0) | transfer/carrier protein |
| ENSG00000116017 | "AT-rich interactive domain-containing protein 3A" | AT-RICH INTERACTIVE DOMAIN-CONTAINING PROTEIN 3A (PTHR15348:SF1) | "transcription factor nucleic acid binding" |
| ENSG00000182175 | "Repulsive guidance molecule A" | REPULSIVE GUIDANCE MOLECULE A (PTHR31428:SF4) | - |
| ENSG00000126934 | "Dual specificity mitogen-activated protein kinase kinase 2" | DUAL SPECIFICITY MITOGEN-ACTIVATED PROTEIN KINASE KINASE 2 (PTHR24361:SF314) | - |
| ENSG00000136718 | "U3 small nucleolar ribonucleoprotein protein IMP4" | U3 SMALL NUCLEOLAR RIBONUCLEOPROTEIN PROTEIN IMP4 (PTHR22734:SF2) | ribonucleoprotein |
| ENSG00000173535 | "Tumor necrosis factor receptor superfamily member 10C" | TUMOR NECROSIS FACTOR RECEPTOR SUPERFAMILY MEMBER 10C (PTHR23097:SF96) | tumor necrosis factor receptor |
| ENSG00000135972 | "28S ribosomal protein S9, mitochondrial" | 28S RIBOSOMAL PROTEIN S9, MITOCHONDRIAL (PTHR21569:SF1) | - |
| ENSG00000179604 | "Cdc42 effector protein 4" | CDC42 EFFECTOR PROTEIN 4 (PTHR15344:SF14) | - |
| ENSG00000106333 | "Procollagen C-endopeptidase enhancer 1" | PROCOLLAGEN C-ENDOPEPTIDASE ENHANCER 1 (PTHR10127:SF628) | "transporter apolipoprotein membrane-bound signaling molecule receptor metalloprotease serine protease oxidase metalloprotease serine protease extracellular matrix protein enzyme modulator cell adhesion molecule" |

#### Gene expression in selected genes of interest

![alt text](https://github.com/jknightlab/mirna_pipeline/blob/master/mRNA/control_genes.png)


| Gene id            | Gene name |
| ------------------ | --------- |
| ENSG00000111537.4  | IFNG      |
| ENSG00000112115.5  | IL17A     |
| ENSG00000127318.6  | IL22      |
| ENSG00000135341.13 | MAP3K7    |
| ENSG00000166167.13 | BTRC      |

Code:
```
Bash:
head -n 1 miR-10b.miR-cont.normalized_counts.txt > temp
cat miR-10b.miR-cont.normalized_counts.txt | \
    grep 'ENSG00000112115\|ENSG00000127318\|ENSG00000111537\|ENSG00000135341\|ENSG00000166167' >> \
    temp

R:
data <- read.table("temp", header=TRUE)
par(mfrow=c(2,3))
par(mar=c(4,6,5,3))
boxplot(
    as.integer(data[1, seq(1,4)]),
    as.integer(data[1, seq(5,8)]),
    names=c("miR-10b", "miR-cont"),
    main="IFNG", ylab="Normalized counts",
    cex.axis=2.5, cex.lab=3.5,
    cex.main=3.5, lwd=2)

boxplot(
    as.integer(data[2, seq(1,4)]),
    as.integer(data[2, seq(5,8)]),
    names=c("miR-10b", "miR-cont"),
    main="IL17A", ylab="Normalized counts",
    cex.axis=2.5, cex.lab=3.5,
    cex.main=3.5, lwd=2)

boxplot(
    as.integer(data[3, seq(1,4)]),
    as.integer(data[3, seq(5,8)]),
    names=c("miR-10b", "miR-cont"),
    main="IL22", ylab="Normalized counts",
    cex.axis=2.5, cex.lab=3.5,
    cex.main=3.5, lwd=2)

boxplot(
    as.integer(data[4, seq(1,4)]),
    as.integer(data[4, seq(5,8)]),
    names=c("miR-10b", "miR-cont"),
    main="MAP3K7", ylab="Normalized counts",
    cex.axis=2.5, cex.lab=3.5, cex.main=3.5, lwd=2)

boxplot(
    as.integer(data[5, seq(1,4)]),
    as.integer(data[5, seq(5,8)]),
    names=c("miR-10b", "miR-cont"),
    main="BTRC", ylab="Normalized counts",
    cex.axis=2.5, cex.lab=3.5,
    cex.main=3.5, lwd=2)


boxplot(
    as.integer(data[6, seq(1,4)]),
    as.integer(data[6, seq(5,8)]),
    names=c("miR-10b", "miR-cont"),
    main="CSF2", ylab="Normalized counts",
    cex.axis=2.5, cex.lab=3.5,
    cex.main=3.5, lwd=2)
```


#### Designed by Irina Pulyakhina irina@well.ox.ac.uk
