# learningOrchestra Python package documentation

**learning-orchestra-client** is a Python 3 package available through the Python Package Index. Install it with `pip install learning-orchestra-client`.

All your scripts must import the package and create a link to the cluster by providing the IP address to an instance of your cluster. Preface your scripts with the following code:
```
from learning_orchestra_client import *
cluster_ip = "xx.xx.xxx.xxx"
Context(cluster_ip)
```


The current version of learningOrchestra offers 7 microservices, each corresponding to a Python class:
- The **[Database](#database-python.md) API is the central microservice**. It holds all the data, including the analysis results.
- The **[Data type](#datatype-python.md) API is a preprocessing microservice** dedicated to changing the type of data fields.
- The **[Projection](#projection-python.md), [Histogram](histogram-python.md), [t-SNE](t-sne-python.md) and [PCA](pca-python.md) APIs are data exploration microservices**. They transform the map the data into new representation spaces so it can be visualized. They can be used on the raw data as well as on the intermediate and final results of the analysis pipeline.
- The **[Model builder](modelbuilder-python.md) API is the main analysis microservice**. It includes some preprocessing features and machine learning features to train models, evaluate models and predict information using trained models.
