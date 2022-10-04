---
description: Making implicit context about an ML system explicit.
---

# Overview

When building a piece of production software that includes serving predictions / labels from a trained Machine Learning Model, setting up the production system for model serving appropriately requires a lot of context from the model development and training processes. Often this context is implicit, and is communicated via human-to-human conversations, or unstandardized documentation.&#x20;

Many companies have ML Engineering or ML Infrastructure teams that spend significant effort setting up standardized tools and processes to allow Data Scientists, Data Engineers, ML Engineers, and others to communicate aspects of this implicit context clearly and consistently, to then enable standardized and automated processes for building, testing, deploying, and monitoring  ML Systems.

Examples of implicit context include:

* Data available in different environments, often coming from different data sources, correspond to each other because they represent the same Feature.
  * Example:&#x20;
    * Data with readings from a specific sensor (`sensor1`) come streaming in on a Kafka topic, where temperature recordings are included in each message in a dictionary under the key `temp`.  These are sent directly to the production system, and are included as a Feature in queries to a Trained Model. They are also sent to a relational database for persistent storage, and use in training future models.
    * The Trained Model was trained using historical data from `sensor1` as well as others, and the temperature data for `sensor1` is stored in a table in a relational database, under the column name `temp_sensor1`.&#x20;
*

The purpose of Orchestra's [Broken link](broken-reference "mention") is to allow users to make this implicit context explicit, and then to set up standardizations and automations around Objects in the ML Registry, and their movement through Workflows / Runbooks. \[<mark style="color:red;">To update term</mark>]&#x20;

To do this, users register the [basic-objects](basic-objects/ "mention") of their ML system (i.e. [feature](basic-objects/feature/ "mention")(s), [trained-model](wip/trained-model/ "mention")(s), and [code-block](wip/code-block/ "mention")(s)), as well as [Broken link](broken-reference "mention") between those objects. Each object is also specified with a [storage-location](storage-location/ "mention"), which has a [provider](provider/ "mention") of a given [provider-type](provider-type/ "mention").&#x20;

### Hierarchy of Objects

| Object Category  | Data                                                              | Models                                                                      | Code                                                                                  |
| ---------------- | ----------------------------------------------------------------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| Basic Object     | [feature](basic-objects/feature/ "mention")                       | [trained-model](wip/trained-model/ "mention")                               | [code-block](wip/code-block/ "mention")                                               |
| Storage Location | [data-source.md](storage-location/data-source.md "mention")       | [model-registry.md](wip/model-registry.md "mention")                        | [code-location.md](wip/code-location.md "mention")                                    |
| Provider         | [data-provider.md](provider/data-provider.md "mention")           | [model-registry-provider.md](provider/model-registry-provider.md "mention") | [Broken link](broken-reference "mention")                                             |
| Provider Type    | [data-provider-type](provider-type/data-provider-type/ "mention") | [model-registry-type](provider-type/model-registry-type/ "mention")         | [source-control-provider-type](provider-type/source-control-provider-type/ "mention") |

The only property of each Object that is strictly mandatory is its `name`. This enables users to register objects in Orchestra by providing as little as a `name` at the time of object registration, while returning later to fill in additional details as they become available.

## Older content (might pull some back in)

We use the term "Object" to refer generically to an entity that is registered in the ML Registry (eg. a [data-source.md](storage-location/data-source.md "mention"), [feature](basic-objects/feature/ "mention"), [trained-model](wip/trained-model/ "mention"), [code-block](wip/code-block/ "mention"), or [provider](provider/ "mention")).

To implement Orchestra, you tag the points in your code where the following activities happen:

1. Read [feature](basic-objects/feature/ "mention")s from a [data-provider.md](provider/data-provider.md "mention")
2. Manipulate data to create new or modified [feature](basic-objects/feature/ "mention")s (i.e., feature engineering)
3. Write [feature](basic-objects/feature/ "mention")s to a [data-provider.md](provider/data-provider.md "mention")
4. Providing [feature](basic-objects/feature/ "mention")(s) and [label.md](basic-objects/feature/label.md "mention")(s) to [model-training-code.md](wip/code-block/model-training-code.md "mention") to produce a [trained-model](wip/trained-model/ "mention")
5. Evaluate a [trained-model](wip/trained-model/ "mention")
6. Provide [feature](basic-objects/feature/ "mention")s to a [trained-model](wip/trained-model/ "mention") to produce [predicted-label.md](basic-objects/feature/predicted-label.md "mention")(s)

Optionally, you can indicate the exact lines or blocks of code responsible for each activity.

## Examples

```python
from orchestralib import orchestralib

oc = orchestralib.OrchestraClient(
    api_key='74738ff5-5367-5958-9aee-98fffdcd1876',
    organization='my-awesome-org',
    environment='sample-model-development'
)
```

### 1. Read Features from a Data Provider

{% tabs %}
{% tab title="Tag only" %}
```python
csv_uri = 'gs://novus_brazil_ecommerce/customer_data/customers_data.csv'
user_features = pd.read_csv(csv_uri)
orchestra.data_source('user-features', user_features, orchestralib.GCS, csv_uri)


```
{% endtab %}

{% tab title="Capture code" %}

{% endtab %}
{% endtabs %}





Orchestra's Data Model powers our ML Registry and all other downstream functionality.



Every Code Block has a top-level configuration.  Every run of a Code block has inputs & outputs.  Every run has information about WHERE it was run (runtimeEnvironment).  Every run has tags about the "environment" e.g. production, development, etc

Run == Snapshot.



TODO(): write a high level overview and pretty up these images.

![](<../.gitbook/assets/Screen Shot 2022-07-17 at 8.02.12 PM.png>)

![](<../.gitbook/assets/Screen Shot 2022-07-17 at 8.02.14 PM.png>)
