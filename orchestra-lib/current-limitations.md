# Current limitations

* Orchestralib is currently only available for Python v3. It's been tested with Python v3.8+.
* When `inputFeatures`/`outputFeatures` are passed as arguments to Orchestra APIs, orchestralib captures metadata from the arguments such as column names and data types in the pandas dataframe AT THAT TIME. If the dataframe object is changed subsequently (e.g. if a new column is added), that information will be captured only in orchestra APIs that happen AFTER the change to the dataframe.
* The only in-memory data source currently supported by Orchestra is a pandas `dataframe`.&#x20;
* Orchestra calls for `log_code_block()` APIs cannot be nested, i.e. if you call `log_code_block('cb-1').start()`, the corresponding `log_code_block('cb-1').end()` api call should happen first before calling, say `log_code_block('cb-2').start()` .
* Lineage is maintained between objects in consecutive code blocks by matching the output/input objects using their pythonID. So if the object (eg. pandas dataframe) is processed / copied during an operation not observed by Orchestra (eg. between two code blocks), this lineage could be broken.
* Orchestralib's `log_features` API call takes a connection string as argument to automatically populate the `dataSource` , `dataProvider` and `dataProviderType` objects. Currently, this is only possible if the connection string has the following formats:

| Format           | DataProvider         |
| ---------------- | -------------------- |
| `s3://...`       | AWS S3               |
| `gs://..`        | Google Cloud Storage |
| `dynamodb://...` | AWS DynamoDB         |
| `bigquery://...` | Google Bigquery      |
| `http://...`     | Web Endpoint         |
| `https://...`    | Web Endpoint         |

