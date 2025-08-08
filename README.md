# CUT&RUN and CUT&Tag Articles and Analysis Methods
This is a repo that contains relevant info regarding CUT&RUN and CUT&Tag computational analysis and interpretation, including protocols, pipelines, peak calling algorithms, benchmarking articles, and applications of these techniques.

## Articles

### CUT&RUN was first described in this article by Pete Skene and Steve Henikoff, published in eLife in 2017:
Peter J Skene & Steven Henikoff. An efficient targeted nuclease strategy for high-resolution mapping of DNA binding sites. _eLife_ (2017). https://doi.org/10.7554/eLife.21856

### This was followed by a detailed protocol for CUT&RUN by Peter Skene et al. in Nature Protocols in 2018:
Peter J Skene, Jorja G Henikoff, & Steven Henikoff. Targeted in situ genome-wide profiling with high efficiency for low cell numbers. _Nature Protocols_ (2018). https://doi.org/10.1038/nprot.2018.015

### autoCUT&RUN was next described by Derek Janssens et al. in Epigenetics & Chromatin in 2018:


### Next came an improvement on the original protocol that expanded antibody compatibility by using pAG-MNase instead of pA-MNase, a salt ion modification to the digestion step, and normalization using the E. coli DNA that is carried over from purification of the MNase enzyme. This was described by Michael Meers et al. in eLife in 2019:
Michael P Meers, Terri D Bryson, Jorja G Henikoff, & Steven Henikoff. Improved CUT&RUN chromatin profiling tools. _eLife_ (2019). https://doi.org/10.7554/eLife.46314

### CUT&Tag was first described by Hatice Kaya-Okur in Nature Communications in 2019:
Hatice S. Kaya-Okur, Steven J. Wu, Christine A. Codomo, et al. CUT&Tag for efficient epigenomic profiling of small samples and single cells. _Nat Comm_ (2019). https://doi.org/10.1038/s41467-019-09982-5

### A detailed protocol for CUT&Tag was published by Hatice Kaya-Okur in Nature Protocols in 2020:
Hatice S. Kaya-Okur, Derek H. Janssens, Jorja G. Henikoff, Kami Ahmad, & Steven Henikoff. Efficient low-cost chromatin profiling with CUT&Tag. _Nature Protocols_ (2020). https://doi.org/10.1038/s41596-020-0373-x

### Single-cell CUT&Tag articles:
Marek Bartosovic, Mukund Kabbe, & Gonçalo Castelo-Branco. Single-cell CUT&Tag profiles histone modifications and transcription factors in complex tissues. _Nature Biotechnology_ (2021). https://doi.org/10.1038/s41587-021-00869-9

Steven J. Wu, Scott N. Furlan, et al. Single-cell CUT&Tag analysis of chromatin modifications in differentiation and tumor progression. _Nature Biotechnology_ (2021). https://doi.org/10.1038/s41587-021-00865-z

Chenxu Zhu, et al., Bing Ren. Joint profiling of histone modifications and transcriptome in single cells from mouse brain. _Nature Methods_ (2021). https://doi.org/10.1038/s41592-021-01060-3

Michael P. Meers, et al., Steven Henikoff. Multifactorial profiling of epigenetic landscapes at single-cell resolution using MulTI-Tag. _Nature Biotechnology_ (2022). https://doi.org/10.1038/s41587-022-01522-9

Derek H. Janssens, Jacob E. Greene, et al., Steven Henikoff. Scalable single-cell profiling of chromatin modifications with sciCUT&Tag. _Nature Protocols_ (2023). https://doi.org/10.1038/s41596-023-00905-9

### Article comparing CUT&Tag peak calling with ENCODE ChIP-seq peaks for K562 cells:
Leyla Abbasova, Paulina Urbanaviciute, Di Hu, Joy N. Ismail, Brian M. Schilder, Alexi Nott, Nathan G. Skene, & Sarah J. Marzi. CUT&Tag recovers up to half of ENCODE ChIP-seq histone acetylation peaks. _Nature Communications_ (2025). https://doi.org/10.1038/s41467-025-58137-2

### Article benchmarking peak calling methods for CUT&RUN:
Amin Nooranikhojasteh, Ghazaleh Tavallaee, & Elias Orouji. Benchmarking peak calling methods for CUT&RUN. _Bioinformatics_ (2025). https://doi.org/10.1093/bioinformatics/btaf375

### Article benchmarking scCUT&Tag analysis pipelines:
Félix Raimundo, Pacôme Prompsy, Jean-Philippe Vert, & Céline Vallot. A benchmark of computational pipelines for single-cell histone modification data. _Genome Biology_ (2023). https://doi.org/10.1186/s13059-023-02981-2

## Wet-lab Protocols

### CUT&RUN protocol
https://dx.doi.org/10.17504/protocols.io.zcpf2vn

### Bench Top CUT&Tag protocol
https://dx.doi.org/10.17504/protocols.io.bcuhiwt6

### CUTAC for FFPEs protocol
https://dx.doi.org/10.17504/protocols.io.14egn292zg5d/v4

## Computational Analysis

### CUT&Tag data analysis tutorial
https://dx.doi.org/10.17504/protocols.io.bjk2kkye

### CUT&Tag data analysis for a time series
https://www.protocols.io/view/cut-amp-tag-data-processing-and-analysis-tutorial-5jyl8py98g2w/v2

### Fred Hutch [_Choosing Genomic Tools_](https://hutchdatascience.org/Choosing_Genomics_Tools/index.html) Book 
### Chapter 19: CUT&RUN and CUT&Tag (Written by Ye Zheng)
https://hutchdatascience.org/Choosing_Genomics_Tools/cutrun-and-cuttag.html

### Fred Hutch SEACR Peak Calling GitHub Repo:
https://github.com/FredHutch/SEACR

### Other computational tools for CUT&RUN, CUT&Tag, and CUTAC:
- [nf-core/cutandrun](https://nf-co.re/cutandrun/3.2.2/)
- [TrimGalore](https://github.com/FelixKrueger/TrimGalore)
- [Bowtie2](https://bowtie-bio.sourceforge.net/bowtie2/index.shtml)
- [Samtools](https://www.htslib.org/)
- [deepTools](https://deeptools.readthedocs.io/en/latest/)
- [Picard](https://broadinstitute.github.io/picard/)
- [bedtools](https://bedtools.readthedocs.io/en/latest/)
- [UCSC bigWig track format utilities](https://genome.ucsc.edu/goldenpath/help/bigWig.html)
- [IGV](https://igv.org/)
- [MultiQC](https://github.com/MultiQC/MultiQC)

Note: This is not meant to be an exhaustive list. However, it should include the most relavent articles and the common/effective tools used for analyzing and visualizing CUT&RUN and CUT&Tag data. If there are any glaring ommisions, please feel free to post an issue on this repo.
