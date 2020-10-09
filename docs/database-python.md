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
