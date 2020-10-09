# learningOrchestra Python package documentation

**learning-orchestra-client** is a Python 3 package available through the Python Package Index. Install it with `pip install learning-orchestra-client`.

All your scripts must import the package and create a link to the cluster by providing the IP address to an instance of your cluster. Preface your scripts with the following code:
```
from learning_orchestra_client import *
cluster_ip = "xx.xx.xxx.xxx"
Context(cluster_ip)
```

## Database API

### read_resume_files

```python
read_resume_files(pretty_response=True)
```
* `pretty_response`: returns indented `string` for visualization(default: `True`, returns `dict` if `False`)
(default `True`, if `False`, return dict)

### read_file

```python
read_file(filename, skip=0, limit=10, query={}, pretty_response=True)
```

* `filename` : name of file
* `skip`: number of rows  to skip in pagination(default: `0`)
* `limit`: number of rows to return in pagination(default: `10`)
(maximum is set at `20` rows per request)
* `query`: query to make in MongoDB(default: `empty query`)
* `pretty_response`: returns indented `string` for visualization(default: `True`, returns `dict` if `False`)

### create_file

```python
create_file(filename, url, pretty_response=True)
```

* `filename`: name of file to be created
* `url`: url to CSV file
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

### delete_file

```python
delete_file(filename, pretty_response=True)
```

* `filename`: name of the file to be deleted
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

## Projection API

### create_projection

```python
create_projection(filename, projection_filename, fields, pretty_response=True)
```

* `filename`: name of the file to make projection
* `projection_filename`: name of file used to create projection
* `fields`: list with fields to make projection
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

## Data type handler API

### change_file_type

```python
change_file_type(filename, fields_dict, pretty_response=True)
```

* `filename`: name of file
* `fields_dict`: dictionary with `field`:`number` or `field`:`string` keys  
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

## Histogram API

### create_histogram

```python
create_histogram(filename, histogram_filename, fields,
                 pretty_response=True)
```

* `filename`: name of file to make histogram
* `histogram_filename`: name of file used to create histogram
* `fields`: list with fields to make histogram
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

## t-SNE API

### create_image_plot

```python
create_image_plot(tsne_filename, parent_filename,
                  label_name=None, pretty_response=True)
```

* `parent_filename`: name of file to make histogram
* `tsne_filename`: name of file used to create image plot
* `label_name`: label name to dataset with labeled tuples (default: `None`, to
datasets without labeled tuples)
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

### read_image_plot_filenames

```python
read_image_plot_filenames(pretty_response=True)
```

* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

### read_image_plot

```python
read_image_plot(tsne_filename, pretty_response=True)
```

* tsne_filename: filename of a created image plot
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

### delete_image_plot

```python
delete_image_plot(tsne_filename, pretty_response=True)
```

* `tsne_filename`: filename of a created image plot
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

## PCA API

### create_image_plot

```python
create_image_plot(tsne_filename, parent_filename,
                  label_name=None, pretty_response=True)
```

* `parent_filename`: name of file to make histogram
* `pca_filename`: filename used to create image plot
* `label_name`: label name to dataset with labeled tuples (default: `None`, to
datasets without labeled tuples)
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

### read_image_plot_filenames

```python
read_image_plot_filenames(pretty_response=True)
```

* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

### read_image_plot

```python
read_image_plot(pca_filename, pretty_response=True)
```

* `pca_filename`: filename of a created image plot
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

### delete_image_plot

```python
delete_image_plot(pca_filename, pretty_response=True)
```

* `pca_filename`: filename of a created image plot
* `pretty_response`: returns indented `string` for visualization
(default: `True`, returns `dict` if `False`)

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
