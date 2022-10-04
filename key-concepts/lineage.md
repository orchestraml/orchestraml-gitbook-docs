# Lineage

### Lineage Relationships

The two main types of Feature lineage that are stored in Orchestra are `createdUsing` and `passedFrom` relationships.

An output Feature or Model is `createdUsing`&#x20;

* the `codeblock` that it was output from, and&#x20;
* the `features` that were inputs to that Code Block&#x20;

An output Feature is `passedFrom`&#x20;

* the `feature` it corresponds to in its original data source, and&#x20;
* any `codeblocks` it passed through without being operated on

### Lineage propagation

One of the key properties of Orchestra, is that it creates and propagates lineage information along, as Features as passed through a sequence of Code Blocks. In particular

* **\[Reading Features]** When Features are read in to an in-memory data source (i.e. pandas dataframe) from an external data source and logged using the `log_features()` command, the in-memory Features are marked as being `passedFrom` the given external data source
* **\[Pass-Through Features]** When in-memory Features are passed through a Code Block (i.e. they are inputs to the Code Block, and also outputs from the same Code Block, perhaps along with other additional in-memory Features), the pass-through features have the current Code Block appended to the list of `codeblocks` in their `passedFrom` attribute.
  * Any other lineage information about the Features from the input in-memory data source is propagated to the pass-through Features in the output in-memory data source.
* **\[Feature Creation]** When in-memory Features are created within a Code Block (eg. they are created from other features, generated, etc, but are not passed in-memory or read from an external data source), the current Code Block is listed under `codeblock` in their `createdUsing` attribute.
  * When new output Features are created, users may indicate the specific input Features that were used to create them, by passing a `CreatedUsing` object to the `created_using` parameter of the `log_code_block().end()` command.
* **\[Writing Features]** When in-memory Features are being written to an external data source, and logged using the `log_features()` command, any existing lineage information for them (going back to the data source that they were read from) is propagated to the Features in the external data source.
* **\[Writing Models]** When a trained Model is being written to an external Model Registry or other storage location, any lineage information about the in-memory Model object is propagated. If the Model was created in the current Code Block, its `createdUsing: codeblock` and `features` information is populated using the current Code Block, and its input Features.

ToDo: Add diagrams illustrating the above relationships
