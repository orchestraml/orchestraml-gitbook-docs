# Trained Model

## Overview

A `Trained Algorithm` is the Orchestra [Building Block](../) that contains the algorithm itself.  A `Trained Algorithm`, if fed the correct `Features`, produces a `Predicted Label`.

## Details

### Inputs

<table><thead><tr><th>Name</th><th>Type</th><th data-type="select">Number of values</th><th data-type="checkbox">Required?</th></tr></thead><tbody><tr><td>Algorithm input features</td><td><code></code><a href="../../basic-objects/feature/"><code>Feature</code></a><code></code></td><td></td><td>true</td></tr></tbody></table>

### Outputs

<table><thead><tr><th>Name</th><th>Type</th><th data-type="select">Number of values</th><th data-type="checkbox">Required?</th></tr></thead><tbody><tr><td>Predicted label(s)</td><td><code></code><a href="../../basic-objects/feature/predicted-label.md"><code>Predicted Label</code></a><code></code></td><td></td><td>true</td></tr></tbody></table>

### Properties

#### Human readable

| Property                      | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name & description`          | See [name-and-description.md](../../shared-attributes/name-and-description.md "mention")``                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `id`                          | String.  Must be unique within each [`environment`](../../shared-attributes/environment.md). User-provided (`unique-text-name)` OR Orchestra generated (`d73ud6d`).                                                                                                                                                                                                                                                                                                                                                                                                                               |
| `storageLocation.type`        | <p>The<a href="../../provider-type/model-registry-type/"><code>Model Registry</code></a> where the file(s), configuration, etc is in order to load the algorithm into a <a href="../runtime-context.md"><code>Runtime Environment</code></a> and turn input <a href="../../basic-objects/feature/"><code>Features</code></a> into <a href="../../basic-objects/feature/predicted-label.md"><code>Predicted Labels</code></a>.<br><br><em>Note: Orchestra does NOT natively support capturing Trained Algorithms - this is only supported through a Model Registry integration - details.</em></p> |
| `storageLocation.config[]`    | The configuration of the [`Model Registry`](../../provider-type/model-registry-type/) stored as Key:Value pairs, optionally validated by a schema provided as part of the [`Model Registry`](../../provider-type/model-registry-type/) integration.                                                                                                                                                                                                                                                                                                                                               |
| `inputs.features[]`           | The specification for the [`Feature(s)`](../../basic-objects/feature/) required by this algorithm.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `outputs.predictedLabels[]`   | The specification for the [`Predicted Label(s)`](../../basic-objects/feature/predicted-label.md) that will be generated by this algorithm.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `training`                    | Details about how this algorithm was trained.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `training.code`               | The [`Algorithm Training Code`](../code-block/model-training-code.md)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `training.runtimeEnvironment` | ``[`Runtime Environment`](../runtime-context.md)``                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `training.parameters`         | TODO(): design this                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |

#### YAML

```yaml
trainedAlgorithm:
  - id: [unique_id]
    name: [user defined string]
    storageLocationType: [ModelLocationType] # storage blob provider, model registry provider, etc
    storageLocationParameters: [ModelLocationParameters] #P1, one sub class per ModelLocationType
    inputs:
      - features: [feature.id]
    outputs:
      - labels: [label.id]
    training:
      - code: [trainingCode.id]
        runtimeEnvironment: [runtimeEnvironment.id]
        parameters: # TODO: to be defined, includes hyperparameters.
```
