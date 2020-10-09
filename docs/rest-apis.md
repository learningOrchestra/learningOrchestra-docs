# learningOrchestra REST APIs documentation

The current version of learningOrchestra offers 7 microservices:
- The **[Database](#database-rest.md) API is the central microservice**. It holds all the data, including the analysis results.
- The **[Data type](#datatype-rest.md) API is a preprocessing microservice** dedicated to changing the type of data fields.
- The **[Projection](#projection-rest.md), [Histogram](histogram-rest.md), [t-SNE](t-sne-rest.md) and [PCA](pca-rest.md) APIs are data exploration microservices**. They transform the map the data into new representation spaces so it can be visualized. They can be used on the raw data as well as on the intermediate and final results of the analysis pipeline.
- The **[Model builder](modelbuilder-rest.md) API is the main analysis microservice**. It includes some preprocessing features and machine learning features to train models, evaluate models and predict information using trained models.

To access those microservices through their REST APIs, we recommand using a **GUI REST API** caller like [Postman](https://www.postman.com/product/api-client/) or [Insomnia](https://insomnia.rest/). Of course, regular `curl` commands from the terminal remain a possibility.
