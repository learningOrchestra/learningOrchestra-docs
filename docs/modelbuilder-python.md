
## Model builder API

### create_model

```python
create_model(training_filename, test_filename, preprocessor_code,
             model_classificator, pretty_response=True)
```

* `training_filename`: name of file to be used in training
* `test_filename`: name of file to be used in test
* `preprocessor_code`: Python3 code for pyspark preprocessing model
* `model_classificator`: list of initial classificators to be used in model
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

#### model_classificator

* `lr`: LogisticRegression
* `dt`: DecisionTreeClassifier
* `rf`: RandomForestClassifier
* `gb`: Gradient-boosted tree classifier
* `nb`: NaiveBayes

to send a request with LogisticRegression and NaiveBayes Classifiers:

```python
create_model(training_filename, test_filename, preprocessor_code, ["lr", "nb"])
```

#### preprocessor_code environment

The Python 3 preprocessing code must use the environment instances as below:

* `training_df` (Instantiated): Spark Dataframe instance training filename
* `testing_df`  (Instantiated): Spark Dataframe instance testing filename

The preprocessing code must instantiate the variables as below, all instances must be transformed by pyspark VectorAssembler:

* `features_training` (Not Instantiated): Spark Dataframe instance for training the model
* `features_evaluation` (Not Instantiated): Spark Dataframe instance for evaluating trained model
* `features_testing` (Not Instantiated): Spark Dataframe instance for testing the model

In case you don't want to evaluate the model, set `features_evaluation` as `None`.

##### Handy methods

```python
self.fields_from_dataframe(dataframe, is_string)
```

This method returns `string` or `number` fields as a `string` list from a DataFrame.

* `dataframe`: DataFrame instance
* `is_string`: Boolean parameter(if `True`, the method returns the string DataFrame fields, otherwise, returns the numbers DataFrame fields)
