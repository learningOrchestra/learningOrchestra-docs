# learningOrchestra Docs

learningOrchestra aims to facilitate the development of complex data mining workflows by **seamlessly interfacing different data science tools and services**. From a single interoperable Application Programming Interface (API), users can **design their analytical pipelines and deploy them in an environment with the appropriate capabilities**.

learningOrchestra is designed for data scientists from both engineering and academia backgrounds, so that they can **focus on the discovery of new knowledge** in their data rather than library or maintenance issues.

learningOrchestra is organised into interoperable microservices. They offer access to third-party libraries, frameworks and software to **gather data**, **clean data**, **train machine learning models**, **tune machine learning models**, **evaluate machine learning models** and **visualize data and results**.

The current version of learningOrchestra offers 7 microservices:
- The **Database API is the central microservice**. It holds all the data, including the analysis results.
- The **Data type API is a preprocessing microservice** dedicated to changing the type of data fields.
- The **Projection, Histogram, t-SNE and PCA APIs are data exploration microservices**. They transform the map the data into new representation spaces so it can be visualized. They can be used on the raw data as well as on the intermediate and final results of the analysis pipeline.
- The **Model builder API is the main analysis microservice**. It includes some preprocessing features and machine learning features to train models, evaluate models and predict information using trained models.

The microservices can be called on from any computer, including one that is not part of the cluster learningOrchestra is deployed on. learningOrchestra provides two options to access its features: a **microservice REST API** and a **Python package**.

Use this documentation to [learn more about the learningOrchestra project](about.md), [learn how to install and deploy learningOrchestra on a cluster](install.md), learn how to use the [REST APIs](rest-apis.md) and [Python package](python-package.md) to access learningOrchestra microservices, or [find options to get support](support.md)

You can also visit the repositories of the learningOrchestra project:
- [learningOrchestra](https://github.com/learningOrchestra/learningOrchestra) for the definition of the microservices and the REST APIs,
- [learningOrchestra-python-client](https://github.com/learningOrchestra/learningOrchestra-python-client) for the Python package,
- [docs](https://github.com/learningOrchestra/docs) for the content of the present documentation, and
- [learningOrchestra.github.io](https://github.com/learningOrchestra/learningOrchestra.github.io) for the code of the present website.
