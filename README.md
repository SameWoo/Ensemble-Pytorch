# Ensemble-Pytorch
Implementation of scikit-learn like ensemble methods in Pytorch.

## Method list
* **FusionClassifier** / **FusionRegressor**
* **VotingClassifier** / **VotingRegressor**
* **BaggingClassifier** / **BaggingRegressor**
* **GradientBoostingClassifier** / **GradientBoostingRegressor**

## Installation

Installing Ensemble-Pytorch package is simple. Just clone this repo and run the setup.

```
$ git clone https://github.com/AaronX121/Ensemble-Pytorch.git
$ cd Ensemble-Pytorch
$ python setup.py install
```

## Minimal example on how to use
```python
"""
  - Please see scripts in `examples` for details on how to use
  - Please see implementations in `torchensemble` for details on ensemble methods
"""

import base_estimator                               # import base estimator
from torchensemble.method import ensemble_method    # import ensemble method

model = ensemble_method(estimator=base_estimator,   # type of base estimator
                        n_estimators=10,            # number of base estimators
                        output_dim=output_dim,      # e.g., the number of classes for classification
                        lr=learning_rate,           # learning rate of the optimizer
                        weight_decay=weight_decay,  # weight decay of model parameters
                        epochs=epochs)              # number of training epochs

# Load data
train_loader = DataLoader(...)
test_loader = DataLoader(...)

# Train
model.fit(train_loader)

# Evaluate
model.predict(test_loader)
```

## Benchmarks

* **Classification on CIFAR-10**
  * The table below presents the classification accuracy of different ensemble classifiers on the testing data of **CIFAR-10**
  * Each classifier uses **10** LeNet-5 model (with RELU activation and Dropout) as the base estimators
  * Each base estimator is trained over **100** epochs, with batch size **128**, learning rate **1e-3**, and weight decay **5e-4**
  * Experiment results can be reproduced by running `./examples/classification_cifar10_cnn.py`

| Model Name | Params (MB) | Testing Acc (%) | Improvement (%) |
| ------ | ------ | ------  | ------ |
| **Single LeNet-5** | 0.32 | 73.04 | - |
| **FusionClassifier** | 3.17 | 78.75 | + 5.71 |
| **VotingClassifier** | 3.17 | 80.08 | + 7.04 |
| **BaggingClassifier** | 3.17 | 78.75 | + 5.71 |
| **GradientBoostingClassifier** | 3.17 | 80.82 | + 7.78 |

* **Regression on YearPredictionMSD**
  * The table below presents the mean squared error (MSE) of different ensemble regressors on the testing data of **YearPredictionMSD**
  * Each regressor uses **10** multi-layered perceptron (MLP) model (with RELU activation and Dropout) as the base estimators, and the network architecture is fixed as `Input-128-128-Output`
  * Each base estimator is trained over **50** epochs, with batch size **256**, learning rate **1e-3**, and weight decay **5e-4**
  * Experiment results can be reproduced by running `./examples/regression_YearPredictionMSD_mlp.py`

| Model Name | Params (MB) | Testing MSE | Improvement |
| ------ | ------ | ------  | ------ |
| **Single MLP** | 0.11 | 0.83 | - |
| **FusionRegressor** | 1.08 | 0.73 | - 0.10 |
| **VotingRegressor** | 1.08 | 0.69 | - 0.14 |
| **BaggingRegressor** | 1.08 | 0.70 | - 0.13 |
| **GradientBoostingRegressor** | 1.08 | 0.71 | - 0.12 |

## Package dependencies
* joblib
* pytorch
* torchvision
* scikit-learn
