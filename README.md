#  Partially-Interpretable Neural Networks for modelling Extreme Values
Methodology for fitting marginal extreme value (and associated) models using partially-interpretable neural networks. Networks are trained using the [R interface to Keras](https://cloud.r-project.org/web/packages/keras/index.html) with custom loss functions taken to be penalised versions of the negative log-likelihood for associated models. For full details on the partially-interpretable deep-learning framework for extreme value analysis, see  Richards, J., Huser, R. <i>A unifying partially-interpretable framework for neural network-based extreme quantile regression</i> (2022).

Note that the partially-interpretable aspect does not need to be incorporated into the models; standard conditional density estimation neural networks can be implemented through function arguments. Missing values in the response variable `Y.train` are handled by setting said values to `-1e10`. For data where `-1e10` is within the range of reasonable values of `Y.train`, the models cannot be readily-applied; in these cases, the data must be scaled  or translated.

## Implemented models
* Generalised Pareto distribution (GPD) - see Coles, S.G. (2001) [doi:10.1007/978-1-4471-3675-0](https://doi.org/10.1007/978-1-4471-3675-0)
* Re-parameterised GPD (With offset scale) - see Richards et al., (2022) [arXiv:2212.01796](https://arxiv.org/abs/2212.01796)
* Blended Generalised Extreme Value (bGEV) distribution - see Castro-Camilo, D., et al. (2022) [doi:10.1002/env.2742](https://doi.org/10.1002/env.2742)
* bGEV point process (bGEV-PP) - see Richards, J. and Huser, R. (2022) [arXiv:2208.07581](https://arxiv.org/abs/2208.07581)
* Non-parametric quantile estimation - see Koenker, R. (2005) [doi:10.1257/jep.15.4.143](https://doi.org/10.1257/jep.15.4.143)
* Bernoulli/logistic
* Log-normal

Note that the bGEV and bGEV-PP models are less computationally efficient than the other models due to the complexity of the likelihood; bear that in mind when running the example code!

## Installation

```r
library(devtools)
install_github("https://github.com/Jbrich95/pinnEV")

#Do not use library(reticulate) as this auto-initialises a Python environment. Instead call functions directly

library(keras)
library(tfprobability)
#Create a virtual envionment 'myenv' with Python3.7. Install tensorflow and tfprobability within this environment.
reticulate::virtualenv_create(envname = 'myenv',  python= 'python3.7')
path<- paste0(reticulate::virtualenv_root(),"/myenv/bin/python")
Sys.setenv(RETICULATE_PYTHON = path)
reticulate::use_virtualenv("myenv", required = T)
reticulate::virtualenv_install("myenv",packages = "tensorflow")
install_keras(method = c("virtualenv"), envname = "myenv") #Install CPU version of tensorflow

library(keras)
library(tfprobability)
reticulate::use_virtualenv("myenv", required = T)
reticulate::virtualenv_install("myenv",packages = "tensorflow_probability")
install_tfprobability(method = c("virtualenv"), envname = "myenv", version="0.14.0")

```

## Coming in future updates 
* Weight regularisation and dropout
* New statistical models - Gamma, extendedGPD, mean/median regression
* Different architecture per parameter
* Non-stationary xi in GPD and bGEV models 

