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
