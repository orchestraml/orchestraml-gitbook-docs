# Data Source

## Overview

A [data-source.md](data-source.md "mention") provides a storage location for one or more [feature](../basic-objects/feature/ "mention")(s).&#x20;

Each [data-source.md](data-source.md "mention") belongs to a single [data-provider.md](../provider/data-provider.md "mention"), of a specified [data-provider-type](../provider-type/data-provider-type/ "mention").

Examples of a [data-source.md](data-source.md "mention"):

* One table in a SQL-like database
* One folder in blob storage with a specific type of file
* One csv file in a directory
* One pandas dataframe

## Details

### Properties

| Property             | Details                                                                                                                                                                                                                                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `name & description` | See [name-and-description.md](../shared-attributes/name-and-description.md "mention").                                                                                                                                                                                                                                               |
| `dataProvider`       | <p>(Optional) The <a data-mention href="../provider/data-provider.md">data-provider.md</a> that the <a data-mention href="data-source.md">data-source.md</a> belongs to. <br>If no <a data-mention href="../provider/data-provider.md">data-provider.md</a> is provided, defaults to <br><code>dataProvider = 'in-memory'</code></p> |
| `features[]`         | <p>A list of the names of the <code>Features</code> that belong to this <a data-mention href="data-source.md">data-source.md</a>.<br>See <a data-mention href="../basic-objects/feature/">feature</a> for details.</p>                                                                                                               |
| `environment`        | The name of the [environment.md](../shared-attributes/environment.md "mention"). Inherited from OrchestraClient.                                                                                                                                                                                                                     |

### YAML

```yaml
dataSource:
  name: 'mySQLtable'
  description: 'This is my SQL table.' 
  dataProvider: 'DP1' 
  features: 
    - 'f1'
    - 'f2'
    - 'f3'
```

### Python

Example code to register a new [data-source.md](data-source.md "mention") and its [feature](../basic-objects/feature/ "mention") set using an existing (i.e. already registered) [data-provider.md](../provider/data-provider.md "mention")



```python
import orchestralib

oc = orchestralib.OrchestraClient(environment = 'dev')
    
oc.register_data_source(
    'mySQLtable',      # defining dataSource.name
    description = 'This is my SQL table.' 
    dataProvider = 'DP1',     # refering to existing dataProvider by its name
    features = ['f1', 'f2', 'f3']
)   

```
