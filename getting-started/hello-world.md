# Hello World

This example contains a single Code Block. In it, a pandas dataframe is generated with two features (`'hello'` and `'world'`), and is saved to a local csv file `'hello_world.csv'`.

```python
import os
import numpy as np
import pandas as pd

# Code Block: Create dataframe with two features in a CSV
df = pd.DataFrame(0, index=np.arange(1,6), columns=['hello'])
df['world'] = df['hello'] + 1
cwd = os.getcwd()
filename1 = cwd + '/' + 'hello_world.csv'
df.to_csv(filename1)
```

So logically, this Code Block (which we’ll call `'hello_world'`)&#x20;

* Has no Features as inputs (since they were created within the block)&#x20;
* Has the two Features `'hello'` and `'world'` in the file `'hello_world.csv'` as outputs&#x20;

This means we would like to register the output Features with Orchestra, and have them associated with this Code Block that was used to create them.\


To instrument the code with Orchestra, first we import `orchestralib` and initialize an Orchestra Client object in python.

```python
import os
import numpy as np
import pandas as pd

from orchestralib import OrchestraClient

orchestra = OrchestraClient(
    organization='my organization',
    environment='development'
    )
```

Next, we define the start and end of the Code Block

```python
# Code Block: Create dataframe containing two Features and save to csv
orchestra.log_code_block('hello_world').start() # NEW
df = pd.DataFrame(0, index=np.arange(1,6), columns=['hello'])
df['world'] = df['hello'] + 1
cwd = os.getcwd()
filename1 = cwd + '/' + '.csv'
df.to_csv(filename1)
orchestra.log_code_block('hello_world').end() # NEW
```

If the user ran the code at this stage, the Code Block would be defined, but it would not have any Input or Output Features.&#x20;

To capture information about Input and Output features that are read from or written to external data sources (in this case, a local csv file), the user adds an `orchestra.log_features()` command for each read or write operation.&#x20;

So, we add this line to log the output features that are saved in the csv file

```python
# Code Block: Create dataframe containing two Features and save to csv
orchestra.log_code_block('hello_world').start() 
df = pd.DataFrame(0, index=np.arange(1,6), columns=['hello'])
df['world'] = df['hello'] + 1
cwd = os.getcwd()
filename1 = cwd + '/' + '.csv'
df.to_csv(filename1)
orchestra.log_features(df, filename1, output_for='hello_world') # NEW
orchestra.log_code_block('hello_world').end()
```

After running this, we can look at the information stored in Orchestra by running the command&#x20;

`orchestra.get_yaml()`

This will show us the following Features, including their location, and reference to the Code Block used to create them.

```yaml
features:
- name: hello
  datatype: int64
  dataSource: /path/to/file/hello_world.csv
  createdUsing:
    codeblock: hello_world
- name: world
  datatype: int64
  dataSource: /path/to/file/hello_world.csv
  createdUsing:
    codeblock: hello_world
```
