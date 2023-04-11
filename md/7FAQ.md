## FAQ

#### I obtained a poor prediction accuracy using SBayesR. Why is that and can it be improve?

If the prediction accuracy is unreasonably low using SBayesR, it is likely that a convergence problem has occurred for the trait analysed. Poor convergence will cause the SNP effect sizes to gradually "blow up" (keep increasing toward infinity) and eventually impair prediction accuracy. If you were using GCTB v2.01 or a lower version, you will usually find hsq (i.e., SNP-based heritability) increases to one and SigmaSq (i.e., the variance of SNP effects) keep increasing along with the MCMC iterations, as shown below for example. 

```
Iter       NumSnp1      NumSnp2      NumSnp3      NumSnp4      SigmaSq      ResVar       GenVar         hsq       Rounding
 100       893956        29937        15607         927        0.0003       0.4961       0.5314       0.5172       0.0000 
 200       915615        23804          3          1005        0.0050       0.0024       0.7879       0.9970       0.0024 
 300       927659        11282          1          1485        0.0188       0.0000       0.8639       1.0000       0.0017 
 400       932231        6640           3          1553        0.0551       0.0000       0.9383       1.0000       0.0014 
 500       934298        4592          16          1521        0.1187       0.0000       1.0284       1.0000       0.0013 
 600       935284        3699          154         1290        0.2155       0.0000       1.1305       1.0000       0.0015 
 700       935920        3162          121         1224        0.3423       0.0000       1.2169       1.0000       0.0018 
 800       936400        2722          148         1157        0.4792       0.0000       1.2991       1.0000       0.0020 
 900       936671        2431          429          896        0.7588       0.0000       1.3778       1.0000       0.0023 
1000       936891        2281          369          886        0.9321       0.0000       1.4472       1.0000       0.0025 
```

At some stage, the program may stop and report the following error message because no SNP can be fitted due to the "blown up".

```
Error: Zero SNP effect in the model for 100 cycles of sampling
```

In GCTB v2.02, we flag the convergence issue by the following message when hsq hits 1 (or equivalently, the residual variance < 0):

```
Error: Residual variance is negative. This may indicate that effect sizes are "blowing up" likely due to a convergence problem. If SigmaSq variable is increasing with MCMC iterations, then this further indicates MCMC may not converge. Please refer to our website (https://cnsgenomics.com/software/gctb) for further information on this problem.
```

Sometimes, even though the MCMC appears to be completed, the posterior means of SNP effects can still be severely biased due to the convergence problem. It is highly recommeded to visualise the scatter plot of the SBayesR estimated SNP effects versus the GWAS marginal effects if you suspect poor convergence. The figure on the left-hand side shows such a scatter plot when MCMC has converged normally. The figure on the right-hand side shows the case when the convergence problem occurred, where some of the SBayesR effect estimates are orders of magnitude larger than the corresponding GWAS marginal effect estimates.

![sbayesr_vs_gwas](fig/sbayesr_vs_gwas.png)

Further plotting the SBayesR effect estimates against the physical positions reveals that some SNPs that are in proximity tend to have their effects "blown up" in opposite directions:

![sbayesr_snp_effects](fig/sbayesr_snp_effects.png)

The fundamental cause of the failure in convergence is not exactly clear, but it is most likely because of the inconsistency between the LD reference data and GWAS summary statistics or/and errors in these datasets. **We suggest to try the following steps to avoid the convergence problem. Please also see [this doc](https://www.dropbox.com/sh/9aougeoxw4ygo8k/AAD6PT3a3ggv1-KYHytbeUNha?dl=0) for a detailed description of processing and running of SBayesR for Locke et al. 2015 and Wood et al. 2014.**

*1. Remove SNPs with extreme GWAS sample sizes.*

It is implicitly assumed in SBayesR that all SNPs have the same GWAS sample size; otherwise, the residual covariance stucture is misspecified. This assumption is often violated when some SNPs have large genotype missing rates or when the GWAS summary statistics are from a meta-analysis where not all SNPs are genotyped in all cohorts. Below is an example of a highly skewed distribution of per-SNP sample size from a meta-analysis.

![yengo_etal_height_snp_n](fig/yengo_etal_height_snp_n.png =400x300)

In this case, removing the SNPs in the lowest 10% quantile led to a converged result. It is highly recommended to examine the distribution of per-SNP sample size prior to the analysis and remove the outliers with extreme sample sizes. Sometimes, the average sample size is given for all the SNPs. In such a case, one can use the **--impute-n** option in GCTB when running SBayesR, which will impute the per-SNP sample size based on the beta values, SE and allele frquenes and exclude SNPs that have the imputed sample sizes 3 standard deviations apart from the median value.

*2. Use the shrunk LD matrix.*

While in principle any type of LD matrix can be used in SBayesR, using the shurnk LD matrix can lead to the most robust result for some traits, such as height. This is likely because the shrunk LD matrix, which is much less sparse than the sparse LD matrix with the default chi-squared threshold, has a better capacity to capture true LD correlations of very small values. Ignoring the SNPs in small LD correlations with the causal variants can collectively cause a bias in the mean of the full conditional distribution of some SNP effects, and subsequently cause the convergence problem. We have provided two shrunk LD matrices based on a random sample of 50K individuals of European ancestry in UK Biobank data, one with about [1.1 million HapMap3 common SNPs](https://zenodo.org/record/3350914#.XyFfnC17G8o) and the other with about [2.8 million common SNPs](https://zenodo.org/record/3375373#.XyFgOS17G8o) using a [genetic map](https://github.com/joepickrell/1000-genomes-genetic-maps) in the public domain.

*3. Use DENTIST to detect and remove SNPs with errors in GWAS or LD reference and heterogeneity between the two.*

[*DENTIST*](https://github.com/Yves-CHEN/DENTIST/) is a software that leverages LD among genetic variants to detect and eliminate errors in GWAS or LD reference and heterogeneity between the two. It could be helpful to run DENTIST prior to SBayesR to identify SNPs that have inconsistent LD properties between GWAS and reference samples, and then use **--exclude** option in GCTB to exclude those SNPs in the SBayesR analysis.

*4. Remove null SNPs based on the GWAS P-values.*

It can be seen from the above plot of SBayesR effect against GWAS effect estimates that the "blowing up" occures more frequently to the SNPs with GWAS effects close to zero. We have also observed a significant improvement in SNP-based heritability estimation and prediction accuracy when removing the null SNPs based on the GWAS P-values for some traits. For example, as shown in the figure below, removing SNPs with GWAS P-value greater than 0.4 (or lower) in the [Wood et al. (2014 Nat Genet)](https://www.nature.com/articles/ng.3097) summary statistics data (after a quality control step on the per-SNP sample size) appeared to fix the convergence problem and led to a substantially improved SNP-based heritability estimates and a higher prediction accuracy. In GCTB, one can use **--p-value** option to specify the upper bound of the P-values of the SNPs to be included in the analysis.

![Height_BMI_SBayesR_pt](fig/Height_BMI_SBayesR_pt.png =600x450)

*5. Filter SNPs based on the LD R-squared.*

When the convergence problem occurred, two SNPs in high LD will sometimes blow up effect sizes in opposite directions, as shown in the figure above. Removing one of the SNPs in high LD could be helpful to mitigate the problem. We have implemented **--rsq** option in GCTB to detect every pair of SNPs with LD R-square greater than the specified threshold and then remove the SNP with higher GWAS P-value.

