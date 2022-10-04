# Runtime Type

A [runtime-context.md](../runtime-context.md "mention") describes where [code-block](../code-block/ "mention") runs. &#x20;

A [.](./ "mention") declares the configuration (set of key:value pairs)  that is required to instantiate an instance of a [runtime-context.md](../runtime-context.md "mention"). Examples of [.](./ "mention")s:

* [Airflow](pipeline-orchestrators/airflow.md)
* Locally virtualenv executing a Python script
* Jupyter Notebook (local or hosted)
* [Kubernetes environment](kubernetes.md)

{% hint style="info" %}
Pipeline Orchestrators, such as Kubeflow or Airlfow, are a sub-class of [.](./ "mention")
{% endhint %}

Orchestra includes a number of pre-defined [.](./ "mention")s or users can define their own by implementing <mark style="color:red;">\[insert link to page with instructions]</mark>.&#x20;

Similar to other Integrations, each [.](./ "mention") has different levels of [integration capability](broken-reference):

* [`Metadata`](https://docs.orchestraml.com/integrations/overview#integration-capabilities): Orchestra is able to capture metadata about the [`Code`](../code-block/) execution in the environment such as time of run, inputs used, outputs produced, etc.
* [`Orchestration`](https://docs.orchestraml.com/integrations/overview#integration-capabilities) : Orchestra is able to request that [`Code`](../code-block/) is executed in the environment. &#x20;
* [`Monitoring`](https://docs.orchestraml.com/integrations/overview#integration-capabilities):  Orchestra is able to understand the current status of [`Code`](../code-block/) running within the environment.&#x20;
