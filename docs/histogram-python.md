
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
