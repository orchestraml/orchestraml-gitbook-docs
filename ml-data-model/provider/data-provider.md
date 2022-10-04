# Data Provider

## Overview

Examples of [data-source.md](../storage-location/data-source.md "mention"), [data-provider.md](data-provider.md "mention"), and [data-provider-type](../provider-type/data-provider-type/ "mention") combinations.

| Data Source                  | Data Provider                        | Data Provider Type | Comments                                                                                                                       |
| ---------------------------- | ------------------------------------ | ------------------ | ------------------------------------------------------------------------------------------------------------------------------ |
| s3://myBucketPath/myImages   | s3://myBucketPath                    | S3                 | <p>Data Provider is the S3 bucket. Data Source is a specific folder.<br>Folder contains multiple files of the same format.</p> |
| s3://myBucketPath/myFile.csv | s3://myBucketPath                    | S3                 | Data Provider is the S3 bucket. Data Source is a csv file.                                                                     |
| mySQLTableName               | mydatabase.rds.aws.com               | MySQL              | Data Provider is the RDS instance, identified by its URL. Data Source is a specific table.                                     |
| BQTableName                  | myproject.mybigqueryinstance.gcp.com | BigQuery           | Data Provider is the BigQuery instance, identified by its URL. Data Source is a specific table                                 |

##

| Property             | Details                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name & description` | See [name-and-description.md](../shared-attributes/name-and-description.md "mention").                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `type`               | <p>The type of <a data-mention href="data-provider.md">data-provider.md</a>. <br>Orchestra-defined types: <code>S3</code>, <code>Snowflake</code>, <code>Databricks</code><br>See <a data-mention href="../provider-type/data-provider-type/">data-provider-type</a> for details and user-specified types.</p>                                                                                                                                                                                                                                                                                                               |
| `config`             | <p>(Optional) The configuration of the <code>Data Provider</code> stored as key:value pairs, validated by a schema provided as part of the <a data-mention href="../provider-type/data-provider-type/">data-provider-type</a> integration (if <code>configSchema</code> is provided).<br><br>eg) a config for <a data-mention href="../provider-type/data-provider-type/wip-s3.md">wip-s3.md</a>could be<br><code>{</code><br>    <code>bucketName: "s3://mybucketname",</code><br>    <code>accountNumber: 123456789101</code></p><p>    <code># other administrator-specified key-value pairs</code><br><code>}</code></p> |
| `environment`        | The [environment.md](../shared-attributes/environment.md "mention") that this [data-provider.md](data-provider.md "mention")exists in. Inherited from OrchestraClient.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

####

```
// Some code
```
