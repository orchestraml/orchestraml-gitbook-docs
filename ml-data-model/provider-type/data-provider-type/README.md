# Data Provider Type

Data Provider Type allows users to define expected schema of the config required to connect to a given type of [data-provider.md](../../provider/data-provider.md "mention").

Orchestra comes with a few [.](./ "mention") definitions pre-populated. See [wip-s3.md](wip-s3.md "mention"), [wip-snowflake.md](wip-snowflake.md "mention"), and [wip-databricks.md](wip-databricks.md "mention").

| Property             | Details                                                                                                                                                                                                                                                                                                                              |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `name & description` | See [name-and-description.md](../../shared-attributes/name-and-description.md "mention").                                                                                                                                                                                                                                            |
| `configSchema`       | <p>(Optional) The expected set of key:value pairs and their types / formats that must be provided to define a <a data-mention href="../../provider/data-provider.md">data-provider.md</a> of the given <a data-mention href="./">.</a>.<br>eg) see <code>configSchema</code> for <a data-mention href="wip-s3.md">wip-s3.md</a> </p> |

####
