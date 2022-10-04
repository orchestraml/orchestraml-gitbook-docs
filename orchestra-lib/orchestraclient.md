# OrchestraClient

The Orchestra Client is used for registering all Orchestra Objects, and interacting with the main Orchestra Server.

The `environment` for each object registered in Orchestra, is inherited from the Orchestra Client used during registration. Features, Data Sources, Models, and Model Registries exist in exactly one environment. Code Blocks don't belong to particular environments, but each specific run of a Code Block happens in a single environment.

### Arguments

| Argument       | Details                                                                                |
| -------------- | -------------------------------------------------------------------------------------- |
| `environment`  | (String, Required) The name of the environment that the client is being initialized in |
| `organization` | (String, Optional) The name of the organization.                                       |

####
