
## Bayesian alphabet


**\--bayes** S

Specify the Bayesian alphabet for the analysis, e.g. S. Different alphabet launch different models, which principally differ in the prior specification for the SNP effects. The available alphabet include

* B: Each SNP effect is assumed to have an i.i.d. mixture prior of a t-distribution $t(0, \tau^2, \nu)$ with a probability $\pi$ and a point mass at zero with a probability $1-\pi$.

* C: Each SNP effect is assumed to have an i.i.d. mixture prior of a normal distribution $N(0, \sigma^2)$ with a probability $\pi$ and a point mass at zero with a probability $1-\pi$. 

* S: Similar to C but the variance of SNP effects is related to minor allele frequency ($p$) through a parameter $S$, i.e. $\sigma_j^2 = [2p(1-p)]^S \sigma_2$.

* N: nested BayesC. SNPs within a 0.2 Mb non-overlapping genomic region are collectively considered as a window (specify the distance by **\--wind** 0.2). This nested approach speeds up the analysis by fast “jumping” over windows with zero effect.

* NS: nested BayesS.

* R: BayesR. Each SNP effect is assumed to have an i.i.d. mixture prior of multiple normal distributions $N(0, \gamma_k \sigma_k^2)$ with a probability $\pi_k$ and a point mass at zero with a probability $1-\sum_k \pi_k$, where $\gamma_k$ is a given constant.

**\--fix-pi**

An option to fix the $\pi$ to a constant (the value is specified by the option --pi below). The default setting is to treat π as random and estimated from the data.

**\--pi** 0.05

A starting value for the sampling of π when it is estimated from the data, or a given value for π when it is fixed. The default value is 0.05. When BayesR is used, it is a string seperated by comma where the number of values defines the number of mixture components and each value defines the starting value for each component (the first value is reserved for the zero component); the default values are 0.95,0.03,0.01,0.01. 

**\--gamma** 0,0.01,0.1,1

When BayesR is used, this speficies the gamma values seperated by comma, each defines the scaling factor for the variance of a mixture component. Note that the number of values should match that in \--pi.

**\--hsq** 0.5

A starting value for the sampling of SNP-based heritability, which may improve the mixing of MCMC algorithm if it starts with a good estimate. The default value is 0.5.

**\--S** 0

A starting value for the sampling of the parameter S (relationship between MAF and variance of SNP effects) in BayesS, which may improve the mixing of MCMC algorithm if it starts with a good estimate. The default value is 0.

**\--wind** 0.2

Specify the window width in Mb for the non-overlapping windows in the nested models, e.g. 0.2 Mb. The default value is 1 Mb.

### Examples

Standard version of gctb:
```
gctb --bfile test --phen test.phen --bayes S --pi 0.1 --hsq 0.5 --chain-length 25000 --burn-in 5000 --out test > test.log 2>&1
```

MPI version of gctb (when using intelMPI libraries and two nodes):
```
mpirun -f $PBS_NODEFILE -np 2 gctb_mpi --bfile test --phen test.phen --bayes S --pi 0.1 --hsq 0.5 --chain-length 25000 --burn-in 5000 --out test > test.log 2>&1
```

The output files include:

**test.log**: a text file of running status and intermediate and final results;

**test.snpRes**: a text file of posterior statistics of SNP effects;

**test.covRes**: a text file of posterior statistics of covariates;

**test.parRes**: a text file of posterior statistics of key model parameters;

**test.mcmcsamples.CovEffects**: a text file of MCMC samples for the covariates fitted in the model;

**test.mcmcsamples.SnpEffects**: a binary file of MCMC samples for the SNP effects;

**test.mcmcsamples.Par**: a text file of MCMC samples for the key model parameters;









