# log\_code\_block()

The `log_code_block` API is used for uniquely identifying a `codeBlock` . The `start` or `end` methods of this codeBlock are used to indicate where the block starts and ends and what it's inputs and outputs are.&#x20;

`codeBlocks` are also used for declaring the `createdUsing` relationships. Consider the case where a `codeBlock` uses some input feature/s and produces new ones. E.g. consider the case where an input feature called `timestamp` is used for creating additional features named `hour`, `minute`and `day` . So, each of the features `hour`, `minute` and `day` should be marked as `createdUsing` the input feature `timestamp`.



### Arguments

| Argument        | Details                                                                                                                                          |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| codeblock\_name | (String, Required) The name used to identify  the codeblock.                                                                                     |
| nested\_under   | (String, Optional) The name of the codeblock  under which this codeblock should be placed under. This should only be used for nested codeblocks. |

The `log_code_block` API will most commonly be used with the `start` and `end` APIs.

#### start

The `start()` api indicates the start of a codeBlock object. Internally Orchestralib will log the line number and filename as the starting point of that codeBlock.

The `start()` API also has two additional arguments. `input_features` and `input_models`.&#x20;

**Arguments**

| Argument         | Details                                                                                                                                                                                                                                                                                                                                 |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `input_features` | (List of Features) The list of feature objects that are inputs to this codeBlock. One common example of this would be a dataframe object being passed to this codeBlock.                                                                                                                                                                |
| `input_models`   | (List of model name strings) The list of model object names that are inputs to this codeBlock. E.g. if a codeBlock is using a `StandardScaler` object for performing some operations on the data, the `StandardScaler` object name would be an `input_model` to the codeBlock. It's name should be sent in the `input_models` argument. |

#### end

The `end()` api indicates the end of a codeBlock object. Internally Orchestralib will log the line number and filename as the end point of that codeBlock.

Similar to the `start` api, the `end()` API also has two additional arguments. `output_features` and `output_models`.&#x20;

**Arguments**

| Argument          | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `output_features` | (List of Features) The list of feature objects that are outputs of this codeBlock. One common example of this would be a dataframe object that was processed in the codeBlock.                                                                                                                                                                                                                                                                                              |
| `output_models`   | (List of model name strings) The list of model object names that are produced in the codeBlock. E.g. if a codeBlock is training a model, the name of the model object should be logged in the `output_models`.                                                                                                                                                                                                                                                              |
| `created_using`   | <p>(source object, list of source feature strings, destination object, list of destination feature strings, Optional) <br><br>Source object is typically a dataframe object<br>List of source feature strings is the list of columns that are inputs to the codeblock<br>Destination object is typically a dataframe object. It could even be the same dataframe object as the source.<br>List of destination feature strings is the list of new/updated feature names.</p> |

### Notes

* The `input_features` in the `start()` API and the `output_features` in the `end()` API can be the same objects. In fact, it is very common for them to be the same object.

### Usage:

```python
df = pd.read_csv('some-csv-url')
orchestra.log_code_block('my-process-codeblock').start(input_features=[df]) #NEW
process_data_here(df)
orchestra.log_code_block('my-process-codeblock').end(output_features=[df]) #NEW

# The following code block takes the 'timestamp' column in the dataframe df and
# produces new columns called 'hour', 'minute' and 'day' in the dataframe itself.
orchestra.log_code_block('create-new-features').start(input_features=[df]) #NEW
create_new_features_in_dataframe(df)
orchestra.log_code_block('create-new-features').end(output_features=[df],
        created_using=orchestra.created_using(
            df, ["timestamp"], df, ["hour", "minute", "day"])) #NEW

# The following code block takes the dataframe df as input and trains a model
# called 'my_model'.
orchestra.log_code_block('model-trainer-codeblock').start(input_features=[df]) #NEW
model_obj = train_model(df, 'my_model')
orchestra.log_code_block('model-trainer-codeblock').end(output_models=['my_model']) #NEW
```

