# log\_model()

Logs Model Objects into Orchestra along with their `inputFeatures`, `outputFeatures` (or labels), codeBlock that creates the model, schema of the output, metrics, model registry details, etc.

### Arguments

| Argument                | Details                                                                                                                                                         |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name                    | (String, Required) The name used to identify  the model.                                                                                                        |
| model\_obj              | (Object, Required) The actual model object. E.g. an XGBClassifier object                                                                                        |
| input\_features         | (List of strings, Required) List of input features for the model                                                                                                |
| output\_features        | (List of strings, Required) List of outputs of the model                                                                                                        |
| training\_code          | (String, Required) Name of the codeBlock that was used to train the model                                                                                       |
| input\_for              | (String, Optional) Name of the codeBlock where this model was an input                                                                                          |
| output\_for             | (String, Optional) Name of the codeBlock where this model was produced. (This is the same as the `training_code`and one of them should be removed)              |
| model\__output\__schema | (List of strings, optional) The schema of the output produced by this model                                                                                     |
| metrics                 | (Dictionary, optional) Dictionary of key value pairs used for string model evaluation metrics                                                                   |
| model\_registry         | (String, optional) Name of the model registry where the model is stored                                                                                         |
| path                    | (String, optional) Path where the model is stored. This could be a path in a cloud storage bucket or some network endpoint where the model object is accessible |
| run                     | (String, Optional) The unique ID of a run when the model was produced. If using MLFlow, this could be the run\_id in mlflow.                                    |
| tags                    | (Dictionary, Optional) Dictionary of key/value pairs (string:string)                                                                                            |
| desc                    | (String, Optional) A string describing the model                                                                                                                |



#### Usage:

```python
df = pd.read_csv('some-csv-url')
orchestra.log_code_block('my-process-codeblock').start(input_features=[df])
process_data_here(df)
orchestra.log_code_block('my-process-codeblock').end(output_features=[df])

orchestra.log_code_block('model-trainer-codeblock').start(input_features=[df])
X = df[['some subset']]
y = df['y']
model_obj = train_model(df, 'my_model')
orchestra.log_model('my_model', model_obj, X, y, ["float64"],
    'model-trainer-codeblock') # NEW 
orchestra.log_code_block('model-trainer-codeblock').end()
```
