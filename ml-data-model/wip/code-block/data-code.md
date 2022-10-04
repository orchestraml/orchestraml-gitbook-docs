# Data Code

Data Code is a type of [.](./ "mention") that takes [feature](../../basic-objects/feature/ "mention")(s) or [data-source.md](../../storage-location/data-source.md "mention")(s) as inputs and produces [feature](../../basic-objects/feature/ "mention")(s) outputs. &#x20;

Data Code includes code that does 1 or more of the following:

* Read [feature](../../basic-objects/feature/ "mention")s from a [data-provider.md](../../provider/data-provider.md "mention")
* Manipulate data to create new or modified [feature](../../basic-objects/feature/ "mention")s (i.e., feature engineering)
* Write [feature](../../basic-objects/feature/ "mention")s to a [data-provider.md](../../provider/data-provider.md "mention")

{In a typical feature engineering pipeline, it is common for a [feature](../../basic-objects/feature/ "mention")to be created by performing some operations (eg. transformations, aggregations, etc) on other existing Features.}

This includes



Any code in your model development or production environments that 1 or more of the following activities should be tagged in a [Broken link](broken-reference "mention") block:

*



*

Optionally, you can indicate the exact lines of code responsible for these data activities.

### Snapshot parameters (WIP)

#### Inputs

<table><thead><tr><th>Name</th><th>Type</th><th data-type="select">Number of values</th><th data-type="checkbox">Required?</th></tr></thead><tbody><tr><td>Input Feature(s)</td><td><code></code><a href="../../basic-objects/feature/"><code>Feature</code></a><code></code></td><td></td><td>true</td></tr><tr><td>Parameter(s)</td><td><a href="../wip-regular-parameters.md"><code>Regular parameters</code></a></td><td></td><td>false</td></tr></tbody></table>

#### Outputs

<table><thead><tr><th>Name</th><th>Type</th><th data-type="select">Number of values</th><th data-type="checkbox">Required?</th></tr></thead><tbody><tr><td>Output Feature(s)</td><td><a href="../../basic-objects/feature/"><code>Feature</code></a><code></code></td><td></td><td>true</td></tr></tbody></table>
