# OT-detection
Off target effects of CRISPR/Cas9 or base editors



# Overview:
Hypothesis: Our hypothesis is that Cas9 has two modes of searching through the genome, a 3D search before binding to DNA and then 1D search after it binds to one site. A prediction of this hypothesis is that sequences that partially match the gRNA target site and are nearby the target should be targeted more often that those that are far from the target site.



# Off-target detection methods
Data for off-target detection originates from different methods. These methods can be classified into two main categories: Experimental and computational. Experimental method subdivide into in vitro, cell-based, or in vivo approaches. Computational methods consist of alignment-based and scoring-based approaches.
In this project, two cell-based methods(GUIDEseq and BLISS), one in vitro method(CHANGEseq), and one computational model(Cass-OFFinder) were employed.
For each individual method, off-target distribution is illustrated as an ideogram or scatterplot. 
## Measures for frequency of off-target events:
In **GUIDEseq** and **CHANGEseq**, the number of reads was used as a proxy of frequency. The correlation between number of reads and frequency of cleavage is outlined below.

### GUIDEseq reads against indel frequency (Using the number of guide seq reads as a proxy for off-target frequency )

![image](https://github.com/sadegh-rizi/OT-detection/assets/42430383/618ef25c-cf14-41b0-90d5-7fc2569e17bf)

The range of indel mutation frequencies we detected ranged from 0.03% to 60.1%. Notably, we observed positive linear correlations between GUIDE-seq read counts and indel mutation frequencies for off-target sites of all five RGNs (Figs. 3b–f). Thus, we conclude that GUIDE-seq read counts for a given site provide a quantitative measure of the cleavage efficiency of that sequence by an RGN.[1] 


<br>

![image](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7652380/bin/nihms-1591991-f0014.jpg)

GUIDE-seq read counts are strongly correlated with indel and tag integration frequencies in human primary T-cells.
a, Scatterplots showing correlation between indel frequencies and GUIDE-seq read counts at on- and off-target sites, and b, tag integration and GUIDE-seq read counts at on- and off-target sites. (a-b) Correlation between two samples was calculated using Pearson’s correlation coefficient. [2]

For **BLISS**, a DSB score was reported which is described as the number of unique DSB ends aligned to the target per $10^{5}$ unique BLISS reads

**Cass-OFFinder** looks for off-targets solely based on homology to the on-target and it doesn't provide any scoring or ranking system for OTs.




## Guideseq
58 gRNAs
off-targets from guideseq are visualized on ideograms with  pam density serving as an overlay. 
A frequency table of off-targets from all gRNAs was used to compare PAM density heatmap and off-target density heatmap side by side in an ideogram. The PAM-dense regions roughly align with off-target dense regions. Further investigation is required to prove significant correlation between PAM density and off-target cleavage frequency.
- PAM density table was created by adding the number of 'NGG' occurrences in window slides of size 1e5.
- The off-target density table was created by adding the number of guideseq reads- as a measure of frequency- in window slides of size 1e6.


Two GUIDEseq datasets have been used:

1- Dataset from original GUIDEseq paper 

[jupyter notebook](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/original-guideseq.ipynb)

[plots with prefix orig](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/plots)

[multiple sequence alignments](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/OT-msa)

2- Dataset from CHANGEseq paper which also performed GUIDEseq method on 58 sgRNAs and detected 1702 off-target sites to compare the results of an in vitro method(CHANGEseq) with a cell-based method(GUIDEseq)

[jupyter notebook](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/guideseq.ipynb)

[plots](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/plots)

[multiple sequence alignments](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/OT-msa)




### Ideograms:
In the following ideograms, off-target events are shown as labels and gene density is used as an overlay.

[ideograms](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/ideograms?raw=true)

In the following ideograms, off-target events are shown as labels and pam density is used as overlay. Only canonical PAMs('NGG') were considered as they constitute the majority of cleavage activities. 

[ideograms](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/ideograms_pam_w100000)

![pie chart of PAM types](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/plots/guideseq/PAM_types_pie_chart.png?raw=true)


A heatmap of PAM density (red) is compared with a heatmap of off-target density (blue) in the figure below.
![heatmap of pam and ot](https://raw.githubusercontent.com/sadegh-rizi/OT-detection/main/guide-seq/ideograms_pam_w100000/pngs/0all_gRNAs_log.png?raw=true "PAM density against off-target density")

## Changeseq 
112 gRNAs
off-targets with reads with more than 100 reads were considered. 
The distribution of off-targets does manifest any discernible pattern. A substantial number of off-targets are produced especially for promiscuous gRNAs. 

[plots](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/plots/changeseq)

[notebook](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/CHANGEseq.ipynb)

## Bliss
2 gRNAs: VEGFA and EMX1. Results were compared against Guideseq.

[plots](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/plots/bliss)

[notebook](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/BLISS.ipynb)

## Cass-offinder
putative off-targets up to six mismatches are found using Cass-offinder. No bulges were allowed. Further investigation is required on the matter of bulges.

[plots](https://github.com/sadegh-rizi/OT-detection/tree/main/guide-seq/plots/cass_offinder)

[notebook](https://github.com/sadegh-rizi/OT-detection/blob/main/guide-seq/Cas-OFFinder.ipynb)



## Mechanism of Crispr Target Search

 Cascade uses 3D diffusion to bind non-specifically to DNA. There, it undergoes limited 1D diffusion along the DNA. During the 1D search on DNA, it rapidly interrogates PAMs within this region employing very short PAM binding times. If a target site is nearby, it is repeatedly revisited during diffusion until it is recognized or the complex dissociates from the DNA. It is therefore hypothesized that upon encountering a PAM, Cas9 can follow two pathways. First, Cas9 can dissociate from DNA in a three-dimensional fashion upon failing to form an RNA-DNA R-loop. Second, Cas9 can locally diffuse in a one-dimensional fashion probing adjacent PAM sites.
The initial step in Cas9 target search is finding and recognizing a PAM sequence. It has been shown that, without encountering a cognate PAM, Cas9 cannot start R-loop formation, despite the full complementarity between the guide RNA and the target. RNA:DNA heteroduplex initiates at the PAM and proceeds through the target sequence by a sequential, step-wise unwinding mechanism consistent with a Brownian ratchet


1. Globyte, V., Lee, S. H., Bae, T., Kim, J. & Joo, C. CRISPR/Cas9 searches for a protospacer adjacent motif by lateral diffusion. EMBO J 38, e99466 (2019).

2. Sternberg, S. H., Redding, S., Jinek, M., Greene, E. C. & Doudna, J. A. DNA interrogation by the CRISPR RNA-guided endonuclease Cas9. Nature 507, 62–67 (2014).

3. Aldag, P. et al. Dynamic interplay between target search and recognition for a Type I CRISPR-Cas system. Nat Commun 14, 3654 (2023).
 
## Discussion
In vitro methods detect lots of off-target events and can have great sensitivity. However, the number of off-targets found by these methods is too great, many of which can not be validated by cell-based/in-vivo methods. In addition, due to the abundance of detected off-targets, they seem to be distributed all around the genome without any discernible pattern.

Cell-based methods have a much lower false positive rate. Nevertheless, their miss rate(FNR) is higher, and might miss some bonafide off-target events. 

Drawing insights from the distribution of off-target events and existing studies on CRISPR target search mechanism, we propose the following hypothesis:
 CRISPR has two modes of 3D and 1D search. During 3D search, Cascade collides non-specifically with DNA. Subsequently, it interrogates PAMs by lateral diffusion. Upon locating a PAM, complementarity is assessed. If sufficient complementarity is present and a stable R-loop is formed, The target will be cleaved. Otherwise, Cascade either diffuses laterally to search for another adjacent PAM or it dissociates from DNA to start another round of 3D search. A prediction of this hypothesis is that Cascade spends more time in PAM-dense regions and off-target events occur more frequently in these places.  
 


## References:
**1-Original GUIDEseq paper:**
Tsai, S., Zheng, Z., Nguyen, N. et al. [GUIDE-seq enables genome-wide profiling of off-target cleavage by CRISPR-Cas nucleases](https://www.nature.com/articles/nbt.3117). Nat Biotechnol 33, 187–197 (2015). 

**2- CHANGEseq paper:** 
Lazzarotto, C.R., Malinin, N.L., Li, Y. et al. [CHANGE-seq reveals genetic and epigenetic effects on CRISPR–Cas9 genome-wide activity.](https://www.nature.com/articles/s41587-020-0555-7) Nat Biotechnol 38, 1317–1327 (2020). 


3. Globyte, V., Lee, S. H., Bae, T., Kim, J. & Joo, C. CRISPR/Cas9 searches for a protospacer adjacent motif by lateral diffusion. EMBO J 38, e99466 (2019).

4. Sternberg, S. H., Redding, S., Jinek, M., Greene, E. C. & Doudna, J. A. DNA interrogation by the CRISPR RNA-guided endonuclease Cas9. Nature 507, 62–67 (2014).

5. Aldag, P. et al. Dynamic interplay between target search and recognition for a Type I CRISPR-Cas system. Nat Commun 14, 3654 (2023).



If notebooks are not rendered, you can use this website: [NBviewer](https://nbviewer.org/).
