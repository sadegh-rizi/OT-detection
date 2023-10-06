# OT-detection
Off target effects of CRISPR/Cas9 or base editors



# Overview:
Hypothesis: Our hypothesis is that Cas9 has two modes of searching through the genome, a 3D search before binding to DNA and then 2D search after it binds to one site. A prediction of this hypothesis is that sequences that partially match the gRNA target site and are nearby the target should be targeted more often that those that are far from the target site.

Two GUIDEseq datasets have been used:
1- Dataset from original GUIDEseq paper 

[jupyter notebook](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/original-guideseq.ipynb)

[plots with prefix orig](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/plots)

[multiple sequence alignments](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/OT-msa)

2- Dataset from CHANGEseq paper which also performed GUIDEseq method on 58 sgRNAs and detected 1702 off-target sites to compare the results of an in vitro method(CHANGEseq) with a cell-based method(GUIDEseq)

[jupyter notebook](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/guideseq.ipynb)

[plots](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/plots)

[multiple sequence alignments](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/OT-msa)

[ideograms](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/ideograms)


If notebooks are not rendered, you can use this website: [NBviewer](https://nbviewer.org/).


## Ideograms:
In these ideograms, off-target events are shown as labels and gene density is used as an overlay.
[ideograms](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/ideograms)

In these ideograms, off-target events are shown as labels and pam density is used as overlay. (PAM: 'NGG')
[ideograms](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/ideograms_pam_w100000)

Here a heatmap of PAM density (red) is compared with a heatmap of off-target density (blue).
![heatmap of pam and ot](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/ideograms_pam_w100000/0all_gRNAs.png?raw=true "PAM density against off-target density")


## Using the number of guide seq reads as a proxy for off-target frequency 
The range of indel mutation frequencies we detected ranged from 0.03% to 60.1%. Notably, we observed positive linear correlations between GUIDE-seq read counts and indel mutation frequencies for off-target sites of all five RGNs (Figs. 3b–f). Thus, we conclude that GUIDE-seq read counts for a given site provide a quantitative measure of the cleavage efficiency of that sequence by an RGN.[1] 
![image](https://github.com/sadegh-rizi/OT-detection/assets/42430383/618ef25c-cf14-41b0-90d5-7fc2569e17bf)

## References:
**1-Original GUIDEseq paper:**
Tsai, S., Zheng, Z., Nguyen, N. et al. [GUIDE-seq enables genome-wide profiling of off-target cleavage by CRISPR-Cas nucleases](https://www.nature.com/articles/nbt.3117). Nat Biotechnol 33, 187–197 (2015). 

**2- CHANGEseq paper:** 
Lazzarotto, C.R., Malinin, N.L., Li, Y. et al. [CHANGE-seq reveals genetic and epigenetic effects on CRISPR–Cas9 genome-wide activity.](https://www.nature.com/articles/s41587-020-0555-7) Nat Biotechnol 38, 1317–1327 (2020). 

