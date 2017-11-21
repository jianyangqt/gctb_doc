
## Bayes alphabet


**\--bayes** S

Specify the Bayes alphabet for the analysis, e.g. S. Different alphabet launch different models, which principally differ in the prior specification for the SNP effects. The available alphabet include
C: Each SNP effect is assumed to have an i.i.d mixture prior of a normal distribution N(0, σ2) with a probability π and a point mass at zero with a probability 1-π. 
S: Similar to C but the variance of SNP effects is related to minor allele frequency (p) through a parameter S, i.e. σj2 = [2p(1-p)]Sσ2.
N: nested BayesC. SNPs within a 0.2 Mb non-overlapping genomic region are collectively considered as a window (specify the distance by **\--wind** 0.2). This nested approach speeds up the analysis by fast “jumping” over windows with zero effect.
NS: nested BayesS.

**\--fix-pi**

An option to fix the π to a constant (the value is specified by the option --pi below). The default setting is to treat π as random and estimated from the data.

**\--pi** 0.05

A starting value for the sampling of π when it is estimated from the data, or a given value for π when it is fixed. The default value is 0.05.

**\--hsq** 0.5

A starting value for the sampling of SNP-based heritability, which may improve the mixing of MCMC algorithm if it starts with a good estimate. The default value is 0.5.

**\--S** 0

A starting value for the sampling of the parameter S (relationship between MAF and variance of SNP effects) in BayesS, which may improve the mixing of MCMC algorithm if it starts with a good estimate. The default value is 0.


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

**test.log**: a text file of running status, intermediate results, posterior mean and standard deviation of key parameters

**test.snpRes**: a text file of posterior means of SNP effects

**test.mcmcsamples.hsq**: a text file of MCMC samples for SNP-based heritability

**test.mcmcsamples.pi**: a text file of MCMC samples for π

**test.mcmcsamples.S**: a text file of MCMC samples for S

**test.mcmcsamples.NNZsnp**: a text file of MCMC samples for the number of non-zero SNP effects

**test.mcmcsamples.NNZwind**: a text file of MCMC samples for the number of non-zero window effects (if BayesN or BayesNS is used)

**test.mcmcsamples.FixedEffects**: a text file of MCMC samples for the covariates fitted in the model

**test.mcmcsamples.SnpEffects**: a binary file of MCMC samples for the SNP effects








