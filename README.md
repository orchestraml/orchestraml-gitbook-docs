# Welcome

Welcome to Orchestra!

Orchestra allows you to document, share, and use information about the Features in your Data and ML pipelines: where they are stored, what is the code and input features that were used to create them, what ML models they were used to train.&#x20;

Orchestra also allows you to define “correspondences” between Features in different environments, that represent the same attributes and can be used interchangeably (eg. one might be in a database and used for model training, and the other might be from streaming data and is used for model inference).

New users get started with Orchestra by using apis in their code that create a dependency map of their feature engineering pipeline, like this:

<figure><img src=".gitbook/assets/Orchestra_ Feature productionization - avg_5_ue lineage.png" alt=""><figcaption><p>Dependency Map of a feature engineering pipeline.</p></figcaption></figure>

Orchestra is able to propagate information about how data was retrieved from a datasource, the in-memory transformation steps and through to the output data source. So the newly created features have complete lineage info stored in Orchestra, which is accessible by others who use those features in the future.

Orchestra allows users to capture context about Feature lineage at the time it is available, so it is accessible later when it is helpful. So it captures information about:&#x20;

* The **data source** of **input features** just after the features have been read in&#x20;
* The **start** and **end** of **code blocks** used for feature engineering, as they are called&#x20;
* The **input** and **output features** of code blocks, as they are passed&#x20;
* The **data source** of **output features**, just before the features are written&#x20;
* The **features used to train** an ML model, at the time of training

**For the current version of Orchestra, code blocks must be sequential**, but in upcoming versions code blocks may be nested, or follow any DAG-like structure.

