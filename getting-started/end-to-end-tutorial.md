---
description: >-
  End-to-end tutorial of using Orchestralib going from querying data, processing
  it and producing a model.
---

# End-to-end tutorial

Consider a simple example of using a Random Forrest algorithm to detect the fuel efficiency of vehicles. Here is the [explanation](https://stackabuse.com/random-forest-algorithm-with-python-and-scikit-learn/) of the dataset and the model.

Let's walk through creating the above model and using Orchestralib to tag code blocks, features and the model.

**Step 1:** Read the data from an external source and log the features that were read into Orchestra.

```
orchestra.log_code_block("read-fuel-consumption").start()

csv_url = 'https://raw.githubusercontent.com/orchestraml/orchestralib-examples/main/sampledata/random_forrest/petrol_consumption.csv'
df = pd.read_csv(csv_url)
orchestra.log_features(df, csv_url, input_for='read-fuel-consumption')
orchestra.log_code_block("read-fuel-consumption").end(output_features=[df])
```

**Notes:**

* The `start()` api call does not have any inputs because it is literally the first thing being done in the code.
* Once the data is read into a dataframe, orchestra's `log_features` api is called so that the features get logged into orchestra. Technically, the data existed even this code block started executing. Therefore, these features are marked as inputs for this code block using the `input_for` argument.
* This code block produced the dataframe called `df`. Hence it is logged as the `output_features` in the call to `end()`.

**Step 2:** The data that was read into the dataframe has large numbers which make it harder to train the model. Let's scale the numbers down.

```
orchestra.log_code_block("process-fuel-data").start(input_features=[df])

df['Petrol_tax'] = df['Petrol_tax'].apply(lambda x: math.log(x + 2))
df['Average_income'] = df['Average_income'].apply(lambda x: math.log(x + 2))
df['Paved_Highways'] = df['Paved_Highways'].apply(lambda x: math.log(x + 2))
df['Petrol_Consumption'] = df['Petrol_Consumption'].apply(lambda x: math.log(x + 2))

orchestra.log_code_block("process-fuel-data").end(output_features=[df])
```

**Notes:**

* This code block starts with processing the dataframe `df`. Hence `df` is a logged as `input_features`
* The output of the processing is stored into the same dataframe. Hence `df` is logged again as `output_features`.

**Step 3:** Create the test/train split and train the model.

```
orchestra.log_code_block("train-model").start(input_features=[df])

X = df.iloc[:, 0:4]
y = df.iloc[:, 4]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)
regressor = RandomForestRegressor(n_estimators=20, random_state=0)
regressor.fit(X_train.values, y_train.values)
y_pred = regressor.predict(X_test.values)

mabserror = metrics.mean_absolute_error(y_test, y_pred)
msquarederror = metrics.mean_squared_error(y_test, y_pred)
rootmse = np.sqrt(metrics.mean_squared_error(y_test, y_pred))
print('Mean Absolute Error:', mabserror)
print('Mean Squared Error:', msquarederror)
print('Root Mean Squared Error:', rootmse)

orchestra.log_model(name='fuel-consumption', model_obj=regressor, input_features=X,
                    output_features=y, training_code='train-model',
                    metrics={'mean_absolute_error': mabserror,
                             'mean_squared_error': msquarederror,
                             'root_mean_squared_error': rootmse})
orchestra.log_code_block("train-model").end(output_models=['fuel-consumption'])
```

Notes:

* Output of the previous code block `df` is an input to this one. So `df` is logged as `input_features`.
* The test/train split is done, model is trained and the model metrics are computed.
* Orchestra's `log_model` api is called to log the details of the model produced including the metrics.
* Since this code block produced a model, the name of the model was passed to the `output_models` argument.

You can see this example including the YAML it produces [here](https://colab.research.google.com/drive/1q2rzvYngxRPbhs750mDsdkKk9tPiQv1G?usp=sharing). If you want to simply see the YAML, it is available [here](https://github.com/orchestraml/orchestralib-examples/blob/main/yamls/fuel-consumption-random-forest.yaml).
