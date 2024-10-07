##  Local Adaptation NWF

This is a simulation in which local adaptation is achieved through QTL mutations arising in a 20kb region of the 1e6bp genomic element. Neutral mutations may be overlayed for downstream analysis (say, using msprime), as they are excluded from this example. 

`LAimg_greyscale.png` is the example greyscale image used in the current script, but this can be easily exchanged for another greyscale image. If you choose to upload an RBG image, make sure to edit `mapImage.floatK` in line 61 to `mapImage.floatG`. Greyscale is recommended. 

An interesting aspect to this script is how we approach fitness scaling. Notice that we first measure local density, like in other examples, but then we also construct phenotypes and fitness effects from QTLs. The phenotypes of individuals are calculated as the sum of the `m2` mutations (QTL). So then, we have these two elements of fitness scaling: 

first in line 76:
```
inds.fitnessScaling = 1 / (1 + RHO * competition);
```

second in line 87:
```
inds.fitnessScaling =   inds.fitnessScaling * qtl_fit;
```
where qtl_fit is defined as:
```
qtl_fit = 1 + dnorm(phenotype, optimum, SK);
qtl_fit = qtl_fit/max(qtl_fit);
```

Additionally, we save parameters such as `phenotype`, `optimum`, `ids`, along with all default parameters in the treeSeqOutput for downstream analysis. This can easily be modified in line 127. 

One example of how we've used these values is by taking the difference in phenotype and optimum and averaging across individuals for a quantitative measure of local adaptation. We've then varied the default parameters to see how this measure of local adaptation shifts (ex. with a higher sigma_D, there is a higher difference in optimum & pheno).

The goal of this script is to serve as a baseline for exploration of Local Adaptation in complex systems. 