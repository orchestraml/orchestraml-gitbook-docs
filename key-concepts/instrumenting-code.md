# Instrumenting Code

To instrument python code with Orchestra, there are two steps&#x20;

1. Define Code Blocks, and their in-memory input and output Features (and Models, if any)&#x20;
2. Add inputs and outputs that are read from or written to any external location.

### 1. Define Code Blocks, and their in-memory inputs and outputs

* Delineate the start and end of each block with the commands `orchestra.log_code_block('codeblock_name').start()` and `orchestra.log_code_block('codeblock_name').end()`&#x20;
* Provide any in-memory Data Sources (i.e. pandas dataframes) that are passed to the Code Block as inputs or outputs.&#x20;
  * Use the `input_features` parameter in the `start()` command&#x20;
  * Use the `output_features` parameter in the `end()` command&#x20;
* Provide any in-memory Models that are passed to the Code Block as inputs or outputs
  * Use the `input_models` parameter in the `start()` command&#x20;
  * Use the `output_models` parameter in the `end()` command&#x20;

NOTE: Orchestra matches the in-memory objects of consecutive code blocks to each other by using their pythonID. So if additional processing is happening between the code blocks (which isn’t visible to Orchestra) that changes the pythonID, the lineage may not be propagated correctly.

### 2. Add inputs and outputs that are read from or written to any external location

a) Add Features and their Data Sources using the `orchestra.log_features()` command

b) Add Models and their Model Registries using the `orchestra.log_model()` command

### Put another way

There are _two ways that Features can be defined as inputs_ to a given run of a Code Block.  They may be&#x20;

1. Read in from an external data source, within the Code Block, and then registered with Orchestra using the `log_features()` command.&#x20;
2. Passed directly, as columns of an in-memory dataframe, and registered with Orchestra using the `log_codeblock().start()` command.

Similarly, there are _two ways that Features can be defined as outputs_ to a given run of a Code Block. They may be

1. Written to an external data source, within the Code Block, and then registered with Orchestra using the `log_features()` command.
2. Passed directly, as columns of an in-memory dataframe, and registered with Orchestra using the `log_codeblock().end()` command.

### 3. Phone Home

Orchestralib collects basic metadata about usage. This comprises of timestamp, hostname, organization name, etc.

To opt out of this set the environment variable `ORCHESTRAML_PHONE_HOME` to `False`.

