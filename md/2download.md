
## Download {: .expand}
### Executable
[gctb\_2.05beta\_Linux.zip](download/gctb_2.05beta_Linux.zip) (*Lastest version updated at 15 May 2023*)

### Source code
[GCTB 2.05beta](download/gctb_2.05beta_scr.zip)

### Tutorial data
[GCTB tutorial data](download/gctb_2.0_tutorial.zip)

### Eigen-decomposition data of LD matrices
The eigen-decomposition data are for SBayesRC and SBayesR with the low-rank model. In the follwoing link, we provide data derived from unrelated UKB individuals of Europan (EUR), East Asian (EAS), and African (AFR) ancestires. See our [manuscript](https://www.biorxiv.org/content/10.1101/2022.10.12.510418v1) and [Tutorial](https://cnsgenomics.com/software/gctb/#Tutorial) for details.

* [1M HapMap3 SNPs](https://plot.cnsgenomics.com/SBayesRC/LD/HapMap3/)
* [7M Imputed SNPs](https://plot.cnsgenomics.com/SBayesRC/LD/Imputed/)

### Functional genomic annotations
Download the [formatted data](https://plot.cnsgenomics.com/SBayesRC/Annotation/annot_baseline2.2.zip) for per-SNP functional annotations derived from [S-LDSC BaselineLDv2.2](https://www.nature.com/articles/ng.3954). 

### LD matrices
The following LD matrices were computed based on 1.1 million common SNPs in a random sample of 50K unrelated individuals of European ancestry in UK Biobank dataset unless otherwise noted.

* [Shrunk sparse matrix](https://zenodo.org/record/3350914#.XyFfnC17G8o)
* [Shrunk sparse LD matrix (2.8 million common SNPs)](https://zenodo.org/record/3375373#.XyFgOS17G8o)

In the shrunk sparse matrices, described in [Lloyd-Jones et al. (2019)](https://www.nature.com/articles/s41467-019-12653-0), the observed LD correlations computed from a reference sample were shrunk toward the expected values defined by a [genetic map](https://github.com/joepickrell/1000-genomes-genetic-maps), following the algorithm in [Wen and Stephens (2010)](https://projecteuclid.org/euclid.aoas/1287409368). After shrinkage, LD correlations smaller than a threshold (default 1e-5) were set to be zero to give a sparse format, which is more efficient in storage and computation. 

* [Sparse matrix (including MHC regions)](https://cnsgenomics.com/data/GCTB/ukbEURu_imp_v3_HM3_n50k.chisq10.zip)

The sparse matrices described in [Zeng et al. (2021)](https://www.nature.com/articles/s41467-021-21446-3) were computed by setting the likely chance LD to zero based on a chi-squared test (default threshold at chi-squared test statistic of 10).

* [Banded matrix (including MHC regions)](https://cnsgenomics.com/data/GCTB/band_ukb_10k_hm3.zip)

While the shrunk sparse matrices were used in our original SBayesR paper, [Prive et al. (2021)](https://academic.oup.com/bioinformatics/advance-article/doi/10.1093/bioinformatics/btaa1029/6039173) found that using a banded matrix with a window size of 3 cM per SNP can improve prediction accuracy. Therefore, we have created such a LD matrix in GCTB format for SBayesR analysis.

### Older versions

gctb_2.04.3: [[Linux executable](download/gctb_2.04.3_Linux.zip)] [[source code](download/gctb_2.04.3_scr.zip)]

gctb_2.03beta: [[Linux executable](download/gctb_2.03beta_Linux.zip)]  [[source code](download/gctb_2.03beta_scr.zip)]

gctb_2.02: [[Linux executable](download/gctb_2.02_Linux.zip)]

gctb_2.0: [[Linux executable](download/gctb_2.0_Linux.zip)]  [[source code](download/gctb_2.0_scr.zip)] [[MPI version source code](download/gctb_2.0_mpi_scr.zip)]

gctb_1.0: [[Linux executable](download/gctb_1.0_Linux.zip)] [[Mac executable](download/gctb_1.0_Mac.zip)] [[source code](download/gctb_1.0_scr.zip)] [[MPI version source code](download/gctb_1.0_mpi_scr.zip)]


The MPI version implements a distributed computing strategy that scales the analysis to very large sample sizes. A significant improvement in computing time is expected for a sample size > 10,000. The MPI version needs to be compiled on user’s machine. See [README.html](download/README.html) in the tarball for instructions of compilation and usage. A testing dataset is also included in each tarball.


### Update log 

**1.**  1 Dec, 2017: first release.

**2.**  8 Feb, 2019: version 2.0 includes summary-data-based Bayesian methods.

**3.** 31 Jul, 2020: version 2.02 reports a message for convergence issue.

**4.** 15 Oct, 2021: version 2.03beta includes a robust parameterisation that attempts to address convergence issue.

**5.** 12 Dec, 2022: version 2.04.3 includes additional random effect component in BayesC and BayesR models to capture non-SNP random effects.

**6.** 11 April, 2023: version 2.05beta implements SBayesRC (SBayesR with the low-rank model) for polygenic prediction incorporating functional genomic annotations.
