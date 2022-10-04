# Model Registry Type

## Overview&#x20;

A `Trained Algorithm` is the Orchestra [Building Block](../../wip/) that contains the algorithm itself.  A `Trained Algorithm`, if fed the correct `Features`, produces a `Predicted Label`.



A Model Registry is a commonly used MLOps tool that (among others) has several use cases:

* **Experiment tracking:** Easily compare metrics and other metadata between data science experiments with different combinations of features, algorithms, and hyperparameters.
* **Trained Algorithm storage:** Capture the algorithm's weights in a format that allows for use of the algorithm in production serving environments.

Orchestra natively integrates

## Integration requirements

### Trained Algorithm storage

TODO(ep): \[Talk about the requirements to capture the trained model from the code.  Orchestra can only capture a trained algorithm through the use of a Model Registry.]

### &#x20;



TODO(ep): Add requirements and MLFlow sub-page based on the investigation here: [https://linear.app/orchestra-ml/issue/OM-285/look-into-mlflow-apis](https://linear.app/orchestra-ml/issue/OM-285/look-into-mlflow-apis)



show example code for how mlflow would work

way 1 - user already has mlflow

way 2 - user doesn't have mlflow, we are using it to capture the model object
