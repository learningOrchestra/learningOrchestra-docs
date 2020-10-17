# Data Type API

This microservice changes data type from stored file between `number` and `string`.

## Change field types of inserted file

`PATCH CLUSTER_IP:5003/fieldtypes/<filename>`

The request uses `filename` as the id in the parameters and fields in the body, `fields` is an array with all fields from file to be changed, using `number` or string descriptor in each `Key:Value` to describe the new value of altered field of file.

```json
{
    "field1": "number",
    "field2": "string"
}
```
