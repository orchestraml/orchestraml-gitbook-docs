# Environment

Each [orchestraclient.md](../../orchestra-lib/orchestraclient.md "mention") is initialized in a specific [environment.md](environment.md "mention"). For example `dev`, `staging,` `prod`, `mydev`, `lab`, etc.

TO DO: Specify Object types that exist in exactly one environment, and Object types that can be used / referenced across multiple environments. How to handle the environment for Code Blocks, Trained Models.

| Property      | Details                                                                                                                                                                                                                                                                          |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `environment` | <p>Required. String. </p><p>Each Object in Orchestra has an <a data-mention href="environment.md">environment.md</a> that is inherited from the <a data-mention href="../../orchestra-lib/orchestraclient.md">orchestraclient.md</a> that was used to register  the Object. </p> |
