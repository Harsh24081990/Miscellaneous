#### Json files are of 2 types.
### 1. Simple json files. No need of using [ ]. Each line of file represent a row of data. 
- Example
```
{"id": 1, "name": "Alice"}
{"id": 2, "name": "Bob"}
{"id": 3, "name": "Charlie"}
```

### 2. Complex json files. need to use [ ] . Entire file is one big JSON array of objects.
```
[
  {
    "id": 1,
    "name": "Alice"
  },
  {
    "id": 2,
    "name": "Bob"
  },
  {
    "id": 3,
    "name": "Charlie"
  }
]
```

## Note : 
#### For reading simple json file.
```python
df = spark.read.format("json") \
    .option("multiline", "true") \
    .load("path_to_file.json")
```

#### For reading complex json file. 
```python
df = spark.read.format("json") \
               .load("path_to_file.json")
```

