# t-SNE API

The T-distributed Stochastic Neighbor Embedding (t-SNE) is a machine learning algorithm for visualization.

It is a nonlinear dimensionality reduction technique well-suited for embedding high-dimensional data for visualization in a low-dimensional space of two or three dimensions.

Specifically, it models each high-dimensional object by a two- or three-dimensional point in such a way that similar objects are modeled by nearby points and dissimilar objects are modeled by distant points with high probability, more information about this algorithm in its [Wiki page]( https://en.wikipedia.org/wiki/T-distributed_stochastic_neighbor_embedding).

## Create an image plot

`POST CLUSTER_IP:5005/images/<parent_filename>`

The request uses a `parent_filename` as a dataset inserted filename, the body contains the JSON fields:

```json
{
    "tsne_filename": "image_plot_filename",
    "label_name": "dataset_label_column"
}
```

The `label_name` is the label name of the column for machine learning datasets which has labeled tuples. In the case that the dataset used doesn't contain labeled tuples, define the value as null type in json:

```json
{
    "tsne_filename": "image_plot_filename",
    "label_name": null
}
```

## Delete an image plot

`DELETE CLUSTER_IP:5005/images/<image_plot_filename>`

Deletes an image plot by specifying its file name.

## Read the filenames of the created images

`GET CLUSTER_IP:5005/images`

Returns a list with all created images plot file name.

## Read an image plot

`GET CLUSTER_IP:5005/images/<image_plot_filename>`

Returns the image plot of the specified file name.

### Image plot examples

These examples use the [titanic challengue datasets](https://www.kaggle.com/c/titanic/overview).

#### Titanic Train dataset

![](./tsne_titanic_train.png)

#### Titanic Test dataset

![](./tsne_titanic_test.png)
