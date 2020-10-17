# Description of the microservices

learningOrchestra is organised into interoperable microservices. They offer access to third-party libraries, frameworks and software to **gather data**, **clean data**, **train machine learning models**, **tune machine learning models**, **evaluate machine learning models** and **visualize data and results**.

The current version of learningOrchestra offers 7 microservices:
- The **Database API is the central microservice**. It holds all the data, including the analysis results.
- The **Data type API is a preprocessing microservice** dedicated to changing the type of data fields.
- The **Projection, Histogram, t-SNE and PCA APIs are data exploration microservices**. They transform the map the data into new representation spaces so it can be visualized. They can be used on the raw data as well as on the intermediate and final results of the analysis pipeline.
- The **Model builder API is the main analysis microservice**. It includes some preprocessing features and machine learning features to train models, evaluate models and predict information using trained models.

The microservices can be called on from any computer, including one that is not part of the cluster learningOrchestra is deployed on. learningOrchestra provides two options to access its features: a **microservice REST API** and a **Python package**.

<!-- TOC depthFrom:2 depthTo:4 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Available microservices](#available-microservices)
	- [Database microservice](#database-microservice)
		- [Combine the Database microservice with a GUI](#combine-the-database-microservice-with-a-gui)
	- [Data type microservice](#data-type-microservice)
	- [Projection microservice](#projection-microservice)
	- [Histogram microservice](#histogram-microservice)
	- [t-SNE microservice](#t-sne-microservice)
	- [PCA microservice](#pca-microservice)
	- [Model builder microservice](#model-builder-microservice)
- [Additional information](#additional-information)
	- [Spark Microservices](#spark-microservices)

<!-- /TOC -->

## Available microservices

### Database microservice

The Database microservice is an abstraction layer of a [MongoDB](https://www.mongodb.com/) database. MongoDB uses [NoSQL, aka non-relational, databases](https://en.wikipedia.org/wiki/NoSQL), so the data is stored as [JSON](https://www.json.org/json-en.html)-like documents.

The Database microservice is organised so each database document corresponds to a CSV file. The key of a file is its filename. The file metadata is saved as its first row.

The microservice provides entry points to add a CSV file to the database, delete a CSV file from the database, retrieve the content of a CSV file in the database and list all files in the database.

The Database microservice serves as a central pivot for the others microservices. They all use the Database microservice as their data source. All but the t-SNE and the PCA microservices send their results to the Database microservice to save.

For additional details, see the [REST API](database-rest.md) and [Python package](database-python.md) documentations.

#### Combine the Database microservice with a GUI

GUI database managers like [NoSQLBooster](https://nosqlbooster.com) can interact directly with MongoDB. Using one will let you perform additional tasks which are not implemented in the Database microservice, such as schema visualization, file extractionor direct CSV or JSON download.

Using a GUI is fully compatible with using learningOrchestra Database microservice.

You can connect a MongoDB-compatible GUI to your learningOrchestra database with the url `cluster_ip:27017`, where `cluster_ip` is the IP address to an instance of your cluster. You will need to provide the following credentials:
```
username = root
password = owl45#21
```

### Data type microservice

The Data type microservice revolves around casting the data for a given field (= column for data organised as a table) to a new type. The microservice can cast fields into *strings* or into number types (*float* by default, *int* if appropriate).


For additional details, see the [REST API](datatype-rest.md) and [Python package](datatype-python.md) documentations.

### Projection microservice

The Projection microservice is a data manipulation microservice. It provides an entry point to simplify a dataset by selecting only certain fields (= column for data organised as a table).

For additional details, see the [REST API](projection-rest.md) and [Python package](projection-python.md) documentations.

### Histogram microservice

The Histogram microservice transform the data of a given source into an aggregate with observation counts for each value bin. The aggregate data is saved into the database from the Database microservice and can then be used to generate an histogram representation of the source data.

For additional details, see the [REST API](histogram-rest.md) and [Python package](histogram-python.md) documentations.

### t-SNE microservice

The t-SNE microservice transforms the data of a given source using the [T-distributed Stochastic Neighbor Embedding]((https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding)) algorithm, generates the t-SNE graphical representations, and manages the generated images.

t-SNE is a machine learning algorithm for visualization of high-dimensional data. It relies on a non-linear dimensionality reduction technique to project high-dimensional data into a low-dimensional space (two or three dimensions). It models each high-dimensional object by a point in a low-dimensional space in such a way that similar objects are represented by nearby points with high probability, and conversely dissimilar objects are represented by distant points with high probability.

The t-SNE microservice provides entry points to create and store a t-SNE graphical representation of a dataset, to list all the images previously stored by the microservice, to download one of these images, and to delete one of these images. It relies on a dedicated storage in the Spark cluster rather than the Database microservice.

For additional details, see the [REST API](t-sne-rest.md) and [Python package](t-sne-python.md) documentations.

### PCA microservice

The PCA microservice decompose the data of a given source into a set of orthogonal components that explain a maximum amount of the variance, plots the data into the space defined by those components, and manages the generated images.

The implementation of this microservice relies on the [scikit-learn libray](https://scikit-learn.org/stable/modules/decomposition.html#pca).

The PCA microservice provides entry points to create and store a PCA graphical representation of a dataset, to list all the images previously stored by the microservice, to download one of these images, and to delete one of these images. It relies on a dedicated storage in the Spark cluster rather than the Database microservice.

For additional details, see the [REST API](pca-rest.md) and [Python package](pca-python.md) documentations.

### Model builder microservice

The Model builder microservice is a all-in-one entry point to train, evaluate and apply classification models. It loads datasets from the Database microservice, preprocesses their content using a user-specified Python script, trains each of the specified classifiers on the training dataset, evaluates the accuracy of the trained model on an evaluation dataset, predicts the labels of the unlabelled testing dataset and saves the accuracy results and predicted labels.

For additional details, see the [REST API](modelbuilder-rest.md) and [Python package](modelbuilder-python.md) documentations.

#### Available classifiers

The following classifiers are currently available through the Model builder microservice, in their Pyspark implementation:
* Logistic regression
* Decision tree classifier
* Random forest classifier
* Gradient-boosted tree classifier
* Naive Bayes

#### Preprocessing script

The preprocessing script must be written by the user in Python 3 and include the Pyspark library.

:exclamation: The variable names currently used are not the names typically used in machine learning libraries. Please take care to read their descriptions to understand their actual role.

The following environment instances are made available to it:
- `training_df`: a Spark Dataframe instance holding the training-and-evaluation dataset loaded from the Database microservice,
- `testing_df`: a Spark Dataframe instance holding the unlabelled dataset loaded from the Database microservice.

The preprocessing script must rename the label column as "label" in the training-and-evaluation dataset and create a zero-value "label" column in the unlabelled dataset.

The preprocessing script must instantiate the following variables using Pyspark VectorAssembler:
- `features_training`: Spark Dataframe instance with the preprocessed training dataset, **including** the "label" column,
* `features_evaluation`: Spark Dataframe instance with the preprocessed testing dataset to measure classification accuracy, **including** the "label" column,
* `features_testing`: Spark Dataframe instance with the unlabelled dataset on which to apply the model, **including** the zero-value "label" column.

In case you don't want to evaluate the model, `features_evaluation` can be set to `None`.

##### Example of preprocessing script

This example uses the [titanic challengue datasets](https://www.kaggle.com/c/titanic/overview).

```python
from pyspark.ml import Pipeline
from pyspark.sql.functions import (
    mean, col, split,
    regexp_extract, when, lit)

from pyspark.ml.feature import (
    VectorAssembler,
    StringIndexer
)

TRAINING_DF_INDEX = 0
TESTING_DF_INDEX = 1

training_df = training_df.withColumnRenamed('Survived', 'label')
testing_df = testing_df.withColumn('label', lit(0))
datasets_list = [training_df, testing_df]

for index, dataset in enumerate(datasets_list):
    dataset = dataset.withColumn(
        "Initial",
        regexp_extract(col("Name"), "([A-Za-z]+)\.", 1))
    datasets_list[index] = dataset

misspelled_initials = [
    'Mlle', 'Mme', 'Ms', 'Dr',
    'Major', 'Lady', 'Countess',
    'Jonkheer', 'Col', 'Rev',
    'Capt', 'Sir', 'Don'
]
correct_initials = [
    'Miss', 'Miss', 'Miss', 'Mr',
    'Mr', 'Mrs', 'Mrs',
    'Other', 'Other', 'Other',
    'Mr', 'Mr', 'Mr'
]
for index, dataset in enumerate(datasets_list):
    dataset = dataset.replace(misspelled_initials, correct_initials)
    datasets_list[index] = dataset


initials_age = {"Miss": 22,
                "Other": 46,
                "Master": 5,
                "Mr": 33,
                "Mrs": 36}
for index, dataset in enumerate(datasets_list):
    for initial, initial_age in initials_age.items():
        dataset = dataset.withColumn(
            "Age",
            when((dataset["Initial"] == initial) &
                 (dataset["Age"].isNull()), initial_age).otherwise(
                    dataset["Age"]))
        datasets_list[index] = dataset


for index, dataset in enumerate(datasets_list):
    dataset = dataset.na.fill({"Embarked": 'S'})
    datasets_list[index] = dataset


for index, dataset in enumerate(datasets_list):
    dataset = dataset.withColumn("Family_Size", col('SibSp')+col('Parch'))
    dataset = dataset.withColumn('Alone', lit(0))
    dataset = dataset.withColumn(
        "Alone",
        when(dataset["Family_Size"] == 0, 1).otherwise(dataset["Alone"]))
    datasets_list[index] = dataset


text_fields = ["Sex", "Embarked", "Initial"]
for column in text_fields:
    for index, dataset in enumerate(datasets_list):
        dataset = StringIndexer(
            inputCol=column, outputCol=column+"_index").\
                fit(dataset).\
                transform(dataset)
        datasets_list[index] = dataset


non_required_columns = ["Name", "Embarked", "Sex", "Initial"]
for index, dataset in enumerate(datasets_list):
    dataset = dataset.drop(*non_required_columns)
    datasets_list[index] = dataset


training_df = datasets_list[TRAINING_DF_INDEX]
testing_df = datasets_list[TESTING_DF_INDEX]

assembler = VectorAssembler(
    inputCols=training_df.columns[:],
    outputCol="features")
assembler.setHandleInvalid('skip')

features_training = assembler.transform(training_df)
(features_training, features_evaluation) =\
    features_training.randomSplit([0.8, 0.2], seed=33)
features_testing = assembler.transform(testing_df)
```


## Additional information
### Spark Microservices

The Projection, t-SNE, PCA and Model builder microservices uses the Spark microservice to work.

By default, this microservice has only one instance. In case your data processing requires more computing power, you can scale this microservice.

To do this, with learningOrchestra already deployed, run the following in the manager machine of your Docker swarm cluster:

`docker service scale microservice_sparkworker=NUMBER_OF_INSTANCES`

*\** `NUMBER_OF_INSTANCES` *is the number of Spark microservice instances which you require. Choose it according to your cluster resources and your resource requirements.*
