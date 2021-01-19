
## Download {: .expand}
### Executable files
[gctb\_2.02\_Linux.zip](download/gctb_2.02_Linux.zip) (*Lastest version*)

[gctb\_2.0\_Linux.zip](download/gctb_2.0_Linux.zip)

[gctb\_1.0\_Linux.zip](download/gctb_1.0_Linux.zip)

[gctb\_1.0\_Mac.zip](download/gctb_1.0_Mac.zip)

### Tutorial data
[GCTB tutorial data](download/gctb_2.0_tutorial.zip)

### LD matrices
* [Shrunk sparse LD matrix with 1.1 million HapMap3 common SNPs](https://zenodo.org/record/3350914#.XyFfnC17G8o) (Lloyd-Jones et al 2019)
* [Shrunk sparse LD matrix with 2.8 million common SNPs](https://zenodo.org/record/3375373#.XyFgOS17G8o) (Lloyd-Jones et al 2019)
* [Sparse LD matrix with 1.1 million HapMap3 common SNPs](https://swift.rc.nectar.org.au/v1/AUTH_4dbb3c851266426d9aa75bcefcda5de1/data/share/JianZ_2021_nc/ukbEURu_imp_v3_HM3_n50k.chisq10.zip) (Zeng et al 2021)

The shrunk sparse LD matrices described in [Lloyd-Jones et al. (2019)](https://www.nature.com/articles/s41467-019-12653-0) are computed based a random sample of 50K individuals of European ancestry in UK Biobank data and a [genetic map](https://github.com/joepickrell/1000-genomes-genetic-maps) in the public domain, following the algorithm in [Wen and Stephens (2010)](https://projecteuclid.org/euclid.aoas/1287409368). The sparse LD matrix described in Zeng et al. (2021) is computed by setting the chance LD to zero based on a chi-squared test.

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
