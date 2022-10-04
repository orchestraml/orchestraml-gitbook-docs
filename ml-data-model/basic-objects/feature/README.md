# Feature

## Overview

A [.](./ "mention") is a data object of a specified [type](https://pandas.pydata.org/docs/user\_guide/basics.html#basics-dtypes), that is used to store values of a given attribute. A [.](./ "mention") is stored in exactly one [data-source.md](../../storage-location/data-source.md "mention"), where each [data-source.md](../../storage-location/data-source.md "mention") typically houses many Features.&#x20;

A canonical example of a [.](./ "mention") is a column in a relational database table, or a column in a pandas dataframe. Other examples could be images or documents of a common format, stored in a common blob storage folder.

[.](./ "mention") names are required to be unique within each [data-source.md](../../storage-location/data-source.md "mention") (similar to how column names are required to be unique within each table in a database). A [.](./ "mention") is registered in Orchestra for the purpose of defining relationships between it and other Objects registered in Orchestra. Two important types of relationships are [Broken link](broken-reference "mention") and [Broken link](broken-reference "mention").

Orchestra supports the following [Broken link](broken-reference "mention") relationships involving [.](./ "mention")(s):

* A [.](./ "mention")can be [Broken link](broken-reference "mention")&#x20;
  * one or more other [.](./ "mention")(s), optionally including the specific [data-code.md](../../wip/code-block/data-code.md "mention") used.
  * one or more other [.](./ "mention")(s) along with a [trained-model](../../wip/trained-model/ "mention"), optionally including the specific [model-serving-code.md](../../wip/code-block/model-serving-code.md "mention") used.&#x20;
    * in this case, the [.](./ "mention") created may be labeled as a[predicted-label.md](predicted-label.md "mention")(s), created by the specific [trained-model](../../wip/trained-model/ "mention").
* A [trained-model](../../wip/trained-model/ "mention") can be [Broken link](broken-reference "mention")
  * one or more [.](./ "mention")(s), optionally including the specific [model-training-code.md](../../wip/code-block/model-training-code.md "mention") used.
    * The user may optionally label one or more of the input [.](./ "mention")(s) as a [label.md](label.md "mention") (i.e. outcome variable) for the purposes of model training.

TO DO: Diagram illustrating the above [Broken link](broken-reference "mention") relationships.

## Details

### Properties

| Property               | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name` & `description` | <p>See <a data-mention href="../../shared-attributes/name-and-description.md">name-and-description.md</a><code></code></p><p>Note that <code>dataSource.name</code> is unique among Data Sources within an environment, but <code>Feature.name</code> is only unique within a Data Source.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `dataType`             | <p>Enum. </p><p>Describes the underlying data provided by this feature (int, string, etc), following the <a href="https://pandas.pydata.org/docs/user_guide/basics.html#basics-dtypes">data types</a> used in the pandas library.  </p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `dataSource`           | <p>String.</p><p>Indicates the name of the <a data-mention href="../../storage-location/data-source.md">data-source.md</a> that the Feature is stored in.<br>If not specified, <a data-mention href="../../storage-location/data-source.md">data-source.md</a> is assumed to be "<code>in-memory</code>".</p>                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| `createdUsing`         | <p>References already-registered Orchestra objects by their name. User may pass a dictionary containing one of the following:</p><ul><li><code>{features : [&#x3C;list_of_feature_names>]}</code></li><li><code>{data_code : &#x3C;name_of_data_code_block</code><em><code>>}</code></em></li><li><code>{features : [&#x3C;list_of_feature_names>],</code><br><code>data_code : &#x3C;name_of_data_code_block>}</code></li></ul><ul><li>{<code>trained_model : &#x3C;name_of_trained_model}</code></li><li><code>{model_serving_code : &#x3C;name_of_model_serving_code_block></code>}</li><li>{<code>trained_model : &#x3C;name_of_trained_model,</code><br><code>model_serving_code : &#x3C;name_of_model_serving_code_block>}</code></li></ul> |
| environment            | The name of the [environment.md](../../shared-attributes/environment.md "mention"). Inherited from OrchestraClient                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

### YAML

```yaml
dataSource: 
  name: 'ds1'
  features:
    - 'feature1'
    - 'feature2'
      
features:
  - name: 'feature1'
    dataType: ENUM #[https://pandas.pydata.org/docs/user_guide/basics.html#basics-dtypes]
    dataSource: 'ds1'
    createdUsing: 
      dataCode: 'name_of_data_code_block'
      features: 
        - name: 'feature17'
          dataSource: 'ds2'
        - name: 'feature18'
          dataSource: 'ds2'
        - name: 'feature19'
          dataSource: 'ds2' 
      params: 
        - <other_params_used_by_data_code>
  - name: 'feature2'
    dataType: ENUM #[https://pandas.pydata.org/docs/user_guide/basics.html#basics-dtypes]
    dataSource: 'ds1'
    createdUsing: 
      modelServingCode: 'name_of_model_serving_code_block'
      trainedModel: 'name_of_trained_model'
      params: 
        - <other_params_used_by_model_serving_code>
```

### Python&#x20;

```python
import orchestralib

oc = orchestralib.OrchestraClient(environment = 'dev')

# There are multiple allowable ways to define a list of features
# 1) a list of feature names
features = ['f1', 'f2', 'f3'] 

# 2) a list of dictionaries 
# using just names and dataTypes
features = [
    {'name':'f1', 'dataType': string}, 
    {'name':'f2', 'dataType': int}, 
    {'name':'f3', 'dataType': string}
] 
# OR specifying additional optional properties of each feature 
features = [
    {'name':'f1', 'dataType': string, 'description': 'details about feature f1',
        'createdUsing': {
            'dataCode': 'name_of_code_block',
            'features': ['fname1', 'fname2', 'fname3']
            'params': [5.0, 'mean', 'Gaussian']
        }
    }, 
    {'name':'f2', 'dataType': int, 'description': 'details about feature f2'}, 
    {'name':'f3', 'dataType': string, 'description': 'details about feature f3'}
]

# 3) a list of Orchestra Feature objects
# using just names and dataTypes
features = [
    oc.Feature('f1', dataType = string),
    oc.Feature('f2', dataType = int),
    oc.Feature('f3', dataType = string)
]
# OR specifying additional optional properties of each feature 
features = [
    oc.Feature(
        'f1', 
        data_type = string, 
        description = 'details about feature f1'
        createdUsing = {
            'dataCode': 'name_of_code_block',
            'features': ['fname1', 'fname2', 'fname3']
            'params': [5.0, 'mean', 'Gaussian']
        }
    ),
    oc.Feature('f2', dataType = int, description = 'details about feature f2'),
    oc.Feature('f3', dataType = string, description = 'details about feature f3')
]


# then register the list of features with Orchestra
oc.register_features(data_source = 'ds1', features=features)
```

Features may also be registered with Orchestra at the time of registering the Data Source.

```python
import orchestralib

oc = orchestralib.OrchestraClient(environment = 'dev')

# any of the methods of specifying a list of features can be passed with the
# 'features' parameter when registering a Data Source
oc.register_data_source(
    "mySQLtable",      # defining dataSource.name
    dataProvider = "DP1",    # refer to existing dataProvider by its name
    features = ['f1', 'f2', 'f3']
)   
```
