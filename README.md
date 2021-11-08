<img src="docs/figs/logo_rc.png" width=400, padding=100>


## Robust Adaptive Coarse-to-fine Clusters OptimizatiON
### v 0.5

[![Licence](https://img.shields.io/github/license/fcomitani/raccoon?style=flat-square)](https://github.com/fcomitani/raccoon/blob/main/LICENSE)
[![GitHub top language](https://img.shields.io/github/languages/top/fcomitani/raccoon?style=flat-square)](https://github.com/fcomitani/raccoon/search?l=python)
[![Build Status](https://img.shields.io/travis/com/fcomitani/raccoon/main?style=flat-square)](https://travis-ci.com/fcomitani/raccoon)
[![Documentation Status](https://readthedocs.org/projects/aroughcun/badge/?version=latest&style=flat-square)](https://aroughcun.readthedocs.io/en/latest/?badge=latest)

RACCOON (`aroughcun` in Algonquinian) is a python 3 package for top-down clustering automatization. 
It searches for the optimal clusters in your data by running low information features removal, non-linear dimensionality reduction, and clusters identification. Tunable parameters at each of these steps are automatically set to maximize a clustering "goodness" score. This process is then repeated iteratively within each cluster identified.

This library includes

* features filtering by variance, MAD or t-SVD
* integrated unsupervised/supervised UMAP non-linear dimensionality reduction
* clusters identification by DBSCAN, HDBSCAN, SNN or Louvain
* optimization with grid search, differential evolution or TPE
* k-NN classification
* GPU implementation with RAPIDS

Detailed documentation, API references, FAQ and tutorials can be found at this [link](https://aroughcun.readthedocs.io/en/latest/).

### Dependencies

Besides basic scientific and plotting libraries, the current version requires

```
- scikit-learn
- scikit-network
- umap-learn
- optuna
- seaborn
```

Optional dependencies include

```
- hdbscan
- feather-format
- rapids (see below)
```

### GPU

raccoon can be run on GPU by leveraging RAPIDS libraries. Since these libraries are still in active development, the latest versions are required to avoid issues.

```
- cupy v8.60
- cuml v0.18
- cudf v0.18
- cugraph v0.18
```

Currently, there are some major (hopefully temporary) limitations in this implementation (e.g. UMAP can only run with euclidean distance).
If these do not affect your analysis, we strongly suggest activating the GPU option, especially for larger datasets that could lead to exceptionally cumbersome runs. Alternatively, this option should be used for exploratory runs only.

### Installation

<!--- raccoon releases can be easily installed through the python standard package manager  
`pip install aroughcun`.
--->

To install the latest (unreleased) version you can download it from this repository by running 
 
    git clone https://github.com/fcomitani/raccoon
    cd raccoon
    python setup.py install

### Basic usage

Given an `input` dataset in pandas-like format (samples X features), the `run` function will
automatically set up a clusters search with just some basic options. 

    import aroughcun as rc

    cluster_membership, tree = rc.cluster(input, dim=2, popcut=25,
                                     optimizer='auto', dynmesh=True,
                                     metric_clu='cosine', metric_map='cosine',
                                     savemap=True, chk=True,
                                     outpath='./output', gpu=False)

### Citation

When using this library, please cite

> F. Comitani ... A. Shlien (in preparation)

### Contributions

This library is still a work in progress and we are striving to improve it, by adding more flexibility and increase the memory and time efficiency of the code. If you would like to be part of this effort, please fork the master branch and work from there. Make sure your code passes the travis build test. 

Contributions are always welcome.
