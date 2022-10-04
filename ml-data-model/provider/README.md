# Provider

A [.](./ "mention")is an implementation of a [provider-type](../provider-type/ "mention")

An Orchestra [organization.md](../wip/organization.md "mention") has 1+ [.](./ "mention")for each&#x20;



Orchestra's Providers allow you to take advantage of first-class integration support, even if you have highly customized MLops tools, approaches, and infrastructure.  You can either:

* Use a provided integration for popular tools (built by this community)
* Integrate any another off-the-shelf tool or home-grown tool / scripts by implementing the interface yourself

| Integration abstraction                                                         | Description                                                                                                                                                                                                                          | Examples                                                  |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------- |
| [model-registry-type](../provider-type/model-registry-type/ "mention")          | Stores various metadata (experiments, metrics, etc) and artifacts (pickle files, etc) that describe a [trained-model](../wip/trained-model/ "mention") and allow that [trained-model](../wip/trained-model/ "mention") to be served. | <ul><li>MLFlow</li></ul>                                  |
| [data-provider.md](data-provider.md "mention")                                  | Integrates the metadata from the [data-source.md](../storage-location/data-source.md "mention")s used in your various development, staging, or production training/serving [runtime-type](../wip/runtime-type/ "mention").           | <ul><li>S3</li><li>Databricks</li><li>Snowflake</li></ul> |
| [runtime-type](../wip/runtime-type/ "mention")                                  | A place to execute code (usually customer-controlled) along with APIs that allow Orchestra to request [code-block](../wip/code-block/ "mention") to run or monitor [code-block](../wip/code-block/ "mention") that is running        | <ul><li>Kubernetes</li><li>EKS</li><li>Airflow</li></ul>  |
| [pipeline-orchestrators](../wip/runtime-type/pipeline-orchestrators/ "mention") | _Technically, Pipeline Orchestrator is just a subclass of Runtime Environment, but we call it out here given its importance in so many ML stacks._                                                                                   | <ul><li>Airflow</li><li>Kubeflow</li></ul>                |
