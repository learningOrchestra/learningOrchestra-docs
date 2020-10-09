# Description of the microservices

learningOrchestra is organised into interoperable microservices. They offer access to third-party libraries, frameworks and software to **gather data**, **clean data**, **train machine learning models**, **tune machine learning models**, **evaluate machine learning models** and **visualize data and results**.

The current version of learningOrchestra offers 7 microservices:
- The **Database API is the central microservice**. It holds all the data, including the analysis results.
- The **Data type API is a preprocessing microservice** dedicated to changing the type of data fields.
- The **Projection, Histogram, t-SNE and PCA APIs are data exploration microservices**. They transform the map the data into new representation spaces so it can be visualized. They can be used on the raw data as well as on the intermediate and final results of the analysis pipeline.
- The **Model builder API is the main analysis microservice**. It includes some preprocessing features and machine learning features to train models, evaluate models and predict information using trained models.

The microservices can be called on from any computer, including one that is not part of the cluster learningOrchestra is deployed on. learningOrchestra provides two options to access its features: a **microservice REST API** and a **Python package**.

## Available microservices

### Database microservice

Download and handle datasets in a database.
For additional details, see the [REST API](database-rest.md) and [Python package](database-python.md) documentations.

### Data type microservice

Change dataset fields type between number and text.
For additional details, see the [REST API](datatype-rest.md) and [Python package](datatype-python.md) documentations.

### Projection microservice

Make projections of stored datasets using Spark cluster.
For additional details, see the [REST API](projection-rest.md) and [Python package](projection-python.md) documentations.

### Histogram microservice

Make histograms of stored datasets.
For additional details, see the [REST API](histogram-rest.md) and [Python package](histogram-python.md) documentations.

### t-SNE microservice

Make a t-SNE image plot of stored datasets.
For additional details, see the [REST API](t-sne-rest.md) and [Python package](t-sne-python.md) documentations.

### PCA microservice

Make a PCA image plot of stored datasets.
For additional details, see the [REST API](pca-rest.md) and [Python package](pca-python.md) documentations.

### Model builder microservice

Create a prediction model from pre-processed datasets using Spark cluster.
For additional details, see the [REST API](modelbuilder-rest.md) and [Python package](modelbuilder-python.md) documentations.

## Additional information
### Spark Microservices

The Projection, t-SNE, PCA and Model builder microservices uses the Spark microservice to work.

By default, this microservice has only one instance. In case your data processing requires more computing power, you can scale this microservice.

To do this, with learningOrchestra already deployed, run the following in the manager machine of your Docker swarm cluster:

`docker service scale microservice_sparkworker=NUMBER_OF_INSTANCES`

*\** `NUMBER_OF_INSTANCES` *is the number of Spark microservice instances which you require. Choose it according to your cluster resources and your resource requirements.*

### Database GUI

NoSQLBooster- MongoDB GUI performs several database tasks such as file visualization, queries, projections and file extraction to CSV and JSON formats.
It can be util to accomplish some these tasks with your processed dataset or get your prediction results.

Read the [Database API docs](https://learningorchestra.github.io/docs/database-api/) for more info on configuring this tool.
