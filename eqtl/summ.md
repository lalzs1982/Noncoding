Summary of analysis of 3'UTR eQTL

AIM of this study: 

we want to show that eQTLs identified from within 3'UTR of its associated genes are not false positives, and to reveal the genetic mechanisms for the regulatory effect of the 3'UTR eQTLs (like affecting RNA stability)

Data: 

(1), eQTL~Gene expression association effect size data from GTEx project (obtained via Xin He, Uchicago) for 49 tissues (7 selected for main analysis here: Brain_Cortex, Brain_Cerebellum,Kidney_Cortex, Ovary,Testis, Thyroid and Whole_Blood).

(2),Fine-mapping eQTLs with PIP score using DAPG for 49 tissues based on the eQTL~Gene expression association data (obtained via Gao Wang, Uchicago)

(3), RBP binding sites for 65 RBPs in HepG2 and K562 cell lines from the eCLIP datasets (downloaded from Seqweaver training datasets)

(4), 3'UTR region coordinates for all human genes (downloaded from ensemble database)

(5), 48,442 3'UTR common SNPs produced by SNPsnap webserver with matched allele frequency, gene density, and LD structure et al.
to the 3'UTR eQTL used as control

Analysis:

(1), overenrichment of 3'UTR eQTL with pip score >=0.5 (HP eQTL) within RBP binding regions:

methods: for each RBP, enrichment of HP eQTL within binding regions compared with control SNPs, significance was estimated using the fisher's exact test:

table: summary counts of eQTL with pip score analyzed here. This table show the total counts of fine mapping eQTL, those HP eQTLs, within 3'UTR eQTL and within 3'UTR HP eQTLs in each tissue.    

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.DAPG_eQTL_counts


results: 

a, enrichment analysis using pool of eQTL with maximum pip score >=0.5 in any tissue. This table shows counts of 3'UTR HP eQTL within each RBP binding regions (eQTL_Bind column) and those not (eQTL_notB column), in comparison with control SNPs (Control_Bind, Control_notB), and enrichment ratio, test pvalue, BH FDR also presented, ordered by the FDR.   

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.eQTLenrich_rbpB_eclip.pool


b, enrichment analysis using eQTL with pip score >=0.5 in each tissue seperately

This table is similar as above one, but for eQTL in different tissues seperately (indicated in eQTL_Cate column, for example, Artery_Tibial__1.HP means HP eQTLs in Artery_Tibial tissue), using the same control dataset

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.eQTLenrich_rbpB_eclip


This plot is visual presentation of p value and enrichment ratio listed in above table (HP eQTL only) with RBPs (rows) and tissues (columns) clustered, to show overall pattern of HP eQTL enrichment across tissues.

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.eQTLenrich_rbpB_eclip.bulbplot.pdf


(2), overenrichment of HP eQTL within RBP binding sites predicted by deepsea

methods: for each SNP, the probability of RBP binding for reference allele was predicted using deepsea for total of 73 RBPs (with high score to indicate higher probability of RBP binding),  then compared between  HP eQTL (pip<0.5), LP eQTL (pip<0.5) with control SNPs. 

results:

a, cumulative distribution of deepsea prediction score for reference allele of HP eQTL , LP eQTL and control SNPs for different RBPs and KS-test to estimate difference significance 

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.ecdf_deepsea_ref_score_forPiP_cate.pdf

b, same analysis as above but for eQTL, only those within RBP binding sites obtained from eCLIP (consistent RBP between prediction and eCLIP) analyzed

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.ecdf_deepsea_ref_score_forPiP_cate_RBPbind.pdf
  
(3), tissue specificity analysis of eQTL

methods: esimate true eQTL or positives proportion in each sample based on p value distributions, and also estimate overlapped true eQTL between two tissues. Note: for overlap analysis of true eQTL between tissues like A and B, at first, eQTLs were selected based on low raw p value or high PIP score as positives in tissue A, and then estimate proportion of positives (using 1-pi0 in R) based on p value distribution in tissue B for these positives from tissue A.

results:

a, proportion of estimated true eQTL in different tissues and split into different gene regions (promoter, exon, intron, et al.)
tables of pi1:

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.eQTL_all_associations.pi1


plot of normalized pi1 for different gene regions across tissues

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.pi1_diff.pdf

legend: each circle represent one sample for one gene regions, and the y axis represent pi1 (proportion of true eQTLs estimated) increase over that for exon regions for each tissue (here, we use pi1 difference rather than original pi1 because pi1 are different betwen samples, and it is conveient to show overall pi1  patterns change for different regions across tissue in the same plot) 


b, true 3UTR eQTL overlap between tissues based on pi1 estimates (here HP eQTL in tissue A were used as true positive ones, then pi1 estimates performed in tissue B based on pvalue distribution for these eQTLs). In this table, #eQTLs column to show counts of HP eQTL in tissue A

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.eQTL_highpip.pi1.utr3


(4), consistence of predicted RBP binding changes  (by deepsea) for ref/alternate alleles of HP eQTL and observed eQTL-gene expression associations
method:

For each RBP, the relationship between the deepsea predicted RBP binding probability changes between reference and alternative allele (x-axis) across all HP eQTLs vs their effect size on target gene expression (y-axis) were plot and compared, 
with focus on the direction changes (like negative/positive relationship for RBP binding probability changes  from ref to alternate allele and that for gene expression level changes of target gene)
(Note, here we hypothesize that for the same RBP, its binding to different eQTLs will affect target gene expression level in the same directions across different sites)

results: out of 73 RBPs tested, we have only 5 RBPs (HNRNPK, PABP, SF3A3, SLTM, U2AF1) with clear pattern by manual check, and at the same time 4 of them show significant eQTL over enrichment according to above analysis

https://github.com/lalzs1982/Noncoding/blob/master/eqtl/res.deepsea_diff_vs_geneexpr_association.pdf

