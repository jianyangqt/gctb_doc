
## Download {: .expand}
### Executable files
[gctb\_2.02\_Linux.zip](download/gctb_2.02_Linux.zip) (*Lastest version*)

[gctb\_2.0\_Linux.zip](download/gctb_2.0_Linux.zip)

[gctb\_1.0\_Linux.zip](download/gctb_1.0_Linux.zip)

[gctb\_1.0\_Mac.zip](download/gctb_1.0_Mac.zip)

### Tutorial data
[GCTB tutorial data](download/gctb_2.0_tutorial.zip)

### LD matrices
The following LD matrices were computed based on 1.1 million common SNPs in a random sample of 50K unrelated individuals of European ancestry in UK Biobank dataset unless otherwise noted.

* [Shrunk sparse matrix](https://zenodo.org/record/3350914#.XyFfnC17G8o)
* [Shrunk sparse LD matrix (2.8 million common SNPs)](https://zenodo.org/record/3375373#.XyFgOS17G8o)

In the shrunk sparse matrices, described in [Lloyd-Jones et al. (2019)](https://www.nature.com/articles/s41467-019-12653-0), the observed LD correlations computed from a reference sample were shrunk toward the expected values defined by a [genetic map](https://github.com/joepickrell/1000-genomes-genetic-maps), following the algorithm in [Wen and Stephens (2010)](https://projecteuclid.org/euclid.aoas/1287409368). After shrinkage, LD correlations smaller than a threshold (default 1e-5) were set to be zero to give a sparse format, which is more efficient in storage and computation. 

* [Sparse matrix (including MHC regions)](https://cnsgenomics.com/data/GCTB/ukbEURu_imp_v3_HM3_n50k.chisq10.zip)

The sparse matrices described in [Zeng et al. (2021)](https://www.nature.com/articles/s41467-021-21446-3) were computed by setting the likely chance LD to zero based on a chi-squared test (default threshold at chi-squared test statistic of 10).

* [Banded matrix (including MHC regions)](https://cnsgenomics.com/data/GCTB/band_ukb_10k_hm3.zip)

While the shrunk sparse matrices were used in our original SBayesR paper, [Prive et al. (2021)](https://academic.oup.com/bioinformatics/advance-article/doi/10.1093/bioinformatics/btaa1029/6039173) found that using a banded matrix with a window size of 3 cM per SNP can improve prediction accuracy. Therefore, we have created such a LD matrix in GCTB format for SBayesR analysis.

### Source code
[GCTB 2.0 standard version](download/gctb_2.0_scr.zip)

[GCTB 2.0 MPI version](download/gctb_2.0_mpi_scr.zip)

[GCTB 1.0 standard version](download/gctb_1.0_scr.zip)

[GCTB 1.0 MPI version](download/gctb_1.0_mpi_scr.zip)

The MPI version implements a distributed computing strategy that scales the analysis to very large sample sizes. A significant improvement in computing time is expected for a sample size > 10,000. The MPI version needs to be compiled on user’s machine. See [README.html](download/README.html) in the tarball for instructions of compilation and usage. A testing dataset is also included in each tarball.


### Update log 

**1.**  1 Dec, 2017: first release.

**2.**  8 Feb, 2019: version 2.0 includes summary-data-based Bayesian methods.

**3.** 31 Jul, 2020: version 2.02 reports a message for convergence issue.
