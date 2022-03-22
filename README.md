# IOKR

![Build Status](https://github.com/hi-paris/IOKR/workflows/pytesting/badge.svg)
[![Anaconda Cloud](https://anaconda.org/conda-forge/IOKR/badges/version.svg)](https://anaconda.org/conda-forge/IOKR)
[![Codecov Status](https://codecov.io/gh/IOKR/IOKR/branch/master/graph/badge.svg)](https://codecov.io/gh/IOKR/IOKR)
[![License](https://anaconda.org/conda-forge/IOKR/badges/license.svg)](https://github.com/hi-paris/IOKR/blob/main/LICENSE)



This open source Python library provide several solvers for optimization
problems related to Optimal Transport for signal, image processing and machine
learning.

Website and documentation: [https://PythonOT.github.io/](https://PythonOT.github.io/)

Source Code (MIT): [https://github.com/PythonOT/POT](https://github.com/PythonOT/POT)

POT provides the following generic OT solvers (links to examples):

* [OT Network Simplex solver](https://pythonot.github.io/auto_examples/plot_OT_1D.html) for the linear program/ Earth Movers Distance [1] .
* [Conditional gradient](https://pythonot.github.io/auto_examples/plot_optim_OTreg.html) [6] and [Generalized conditional gradient](https://pythonot.github.io/auto_examples/plot_optim_OTreg.html) for regularized OT [7].
* Entropic regularization OT solver with [Sinkhorn Knopp Algorithm](https://pythonot.github.io/auto_examples/plot_OT_1D.html) [2] , stabilized version [9] [10] [34], greedy Sinkhorn [22] and [Screening Sinkhorn [26] ](https://pythonot.github.io/auto_examples/plot_screenkhorn_1D.html).
* Bregman projections for [Wasserstein barycenter](https://pythonot.github.io/auto_examples/barycenters/plot_barycenter_lp_vs_entropic.html) [3], [convolutional barycenter](https://pythonot.github.io/auto_examples/barycenters/plot_convolutional_barycenter.html) [21]  and unmixing [4].

#### Using and citing the toolbox


## Installation

The library has been tested on Linux, MacOSX and Windows. It requires a C++ compiler for building/installing the EMD solver and relies on the following Python modules:

- Numpy (>=1.16)
- Scipy (>=1.0)
- Cython (>=0.23) (build only, not necessary when installing from pip or conda)

#### Pip installation


You can install the toolbox through PyPI with:

```console
pip install iokr
```

#### Anaconda installation with conda-forge

If you use the Anaconda python distribution, POT is available in [conda-forge](https://conda-forge.org). To install it and the required dependencies:

```console
conda install -c conda-forge IOKR
```

#### Post installation check
After a correct installation, you should be able to import the module without errors:

```python
import IOKR
```

## Examples

### Short examples

* Import the toolbox

```python
import ot
```

* Run IOKR

```python
from IOKR.model.model import IOKR
from sklearn.model_selection import train_test_split
from IOKR.data.load_data import load_bibtex
from sklearn.metrics import f1_score

path = "IOKR/data/bibtex"
X, Y, _, _ = load_bibtex(path)

X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.33, random_state=42)

clf = IOKR()
clf.verbose = 1
L = 1e-5
sx = 1000
sy = 10

clf.fit(X=X_train, Y=Y_train, L=L, sx=sx, sy=sy)
Y_pred_train = clf.predict(X_test=X_train)
Y_pred_test = clf.predict(X_test=X_test)
f1_train = f1_score(Y_pred_train, Y_train, average='samples')
f1_test = f1_score(Y_pred_test, Y_test, average='samples')
print("Train f1 score:", f1_train,"/", "Test f1 score:", f1_test)
```

### Examples and Notebooks

The examples folder contain several examples and use case for the library. The full documentation with examples and output is available on [https://IOKR.github.io/](https://IOKR.github.io/).


## Acknowledgements

This toolbox has been created and is maintained by

* [Hi! PARIS](https://www.hi-paris.fr/)


The contributors to this library are 

* [Florence d'Alché-Buc](https://perso.telecom-paristech.fr/fdalche/) (Research)
* [Luc Motte](https://www.telecom-paris.fr/fr/recherche/laboratoires/laboratoire-traitement-et-communication-de-linformation-ltci/les-equipes-de-recherche/signal-statistique-et-apprentissage-s2a/personnes) (Research)
* [Tamim El Ahmad](https://www.telecom-paris.fr/fr/recherche/laboratoires/laboratoire-traitement-et-communication-de-linformation-ltci/les-equipes-de-recherche/signal-statistique-et-apprentissage-s2a/personnes) (Research)
* [Gaëtan Brison](https://engineeringteam.hi-paris.fr/about-us/) (Engineer)
* [Danaël SCHLEWER-BECKER](https://engineeringteam.hi-paris.fr/about-us/) (Engineer)
* [Awais Sani](https://engineeringteam.hi-paris.fr/about-us/) (Engineer)


## Contributions and code of conduct

Every contribution is welcome and should respect the [contribution guidelines](.github/CONTRIBUTING.md). Each member of the project is expected to follow the [code of conduct](.github/CODE_OF_CONDUCT.md).

## Support

You can ask questions and join the development discussion:

* On the POT [slack channel](https://IOKR-toolbox.slack.com)
* On the POT [gitter channel](https://gitter.im/IOKR/community)
* On the POT [mailing list](https://mail.python.org/mm3/mailman3/lists/IOKR.python.org/)

You can also post bug reports and feature requests in Github issues. Make sure to read our [guidelines](.github/CONTRIBUTING.md) first.

## References

[1] Céline Brouard, Florence d’Alché-Buc, Marie Szafranski (2013, November). [Semi-supervised Penalized Output Kernel Regression for
Link Prediction](https://hal.archives-ouvertes.fr/hal-00654123/document). 28th International Conference on Machine Learning (ICML 2011),
pp.593–600.


Refs:
- Brouard, C., d'Alché-Buc, F., Szafranski, M. Semi-supervised Penalized Output Kernel Regression for Link Prediction, ICML 2011: 593-600, (2011).
- Brouard, C., Szafranski, M., d'Alché-Buc, F.Input Output Kernel Regression: Supervised and Semi-Supervised Structured Output Prediction with Operator-Valued Kernels. J. Mach. Learn. Res. 17: 176:1-176:48 (2016).
- Brouard, C., Shen, H., Dührkop, K., d'Alché-Buc, F., Böcker, S., & Rousu, J. (2016). Fast metabolite identification with input output kernel regression. Bioinformatics, 32(12), i28-i36 (2016).


![alt text](images/readme_iokr_equations.png)

# How to Run IOKR Locally

## 01 Setup computer

- Github Desktop
- Pycharm

Steps: 

1. On Github Desktop add IOKR repository hosted privately on Hi! PARIS Github [https://github.com/hi-paris](https://github.com/hi-paris)
2. Open the repository in your external editor in this case Pycharm

## 02 Pycharm Terminal Commands

Put yourself in the main directory "IOKR"

```bash
--------------------------------
### Install Requirements (dependencies packages)
pip install -r requirements.txt

--------------------------------
### Upgrade your pip command to avoid problems
python -m pip install --upgrade pip

--------------------------------
### Upgrade setuptools to run setup file
pip install --upgrade setuptools
setup.py install

--------------------------------
### Create the local package
pip install -e .

--------------------------------
### Install IOKR
pip install IOKR
```

Once this is done you should see the following message

![alt text](images/package-iokr.png)

## 03 Test packages

You can run the following commands in your python console in Pycharm

```python
from IOKR.model.model import IOKR
from sklearn.model_selection import train_test_split
from IOKR.data.load_data import load_bibtex
from sklearn.metrics import f1_score

path = "IOKR/data/bibtex"
X, Y, _, _ = load_bibtex(path)

X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.33, random_state=42)

clf = IOKR()
clf.verbose = 1
L = 1e-5
sx = 1000
sy = 10

clf.fit(X=X_train, Y=Y_train, L=L, sx=sx, sy=sy)
Y_pred_train = clf.predict(X_test=X_train)
Y_pred_test = clf.predict(X_test=X_test)
f1_train = f1_score(Y_pred_train, Y_train, average='samples')
f1_test = f1_score(Y_pred_test, Y_test, average='samples')
print("Train f1 score:", f1_train,"/", "Test f1 score:", f1_test)
```

You should get something like that:

![alt text](images/output-iokr.png)

<aside>
✅ **Great Job !**

</aside>
