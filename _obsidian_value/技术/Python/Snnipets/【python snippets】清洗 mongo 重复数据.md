
```
/* 1 */
{
    "_id" : ObjectId("5dbaf3939642fb9adcad453c"),
    "username" : "王五",
    "area" : "上海"
}

/* 2 */
{
    "_id" : ObjectId("5dbaf3a19642fb9adcad4549"),
    "username" : "赵四",
    "area" : "北京"
}

/* 3 */
{
    "_id" : ObjectId("5dbaf3b89642fb9adcad4556"),
    "username" : "马六",
    "area" : "北京"
}
/* 4 */
{
    "_id" : ObjectId("5dbaf3b89642fb9adcad4556"),
    "username" : "马六",
    "area" : "北京"
}
```

## 使用管道聚合操作清洗重复数据

```bash
db.getCollection('users').aggregate([
    {
        $group: { _id: {username: '$username', area: '$area'},count: {$sum: 1},dups: {$addToSet: '$_id'}}
    },
    {
        $match: {count: {$gt: 1}}
    }
]).forEach(function(doc){
    doc.dups.shift();
    db['users'].remove({_id: {$in: doc.dups}});
})
```

```python
pipeline = [
    {
        '$group': {
            '_id': {'title': '$title', 'date': '$date', 'url': '$url'},
            'count': {'$sum': 1},
            'dups': {
                '$addToSet': '$_id'
            }
        },
    },
    {
        '$match': {
            'count': {
                '$gt': 1
            }
        }
    }
]

map_id = map(lambda doc: doc['dups'][1:], db['data_value'].aggregate(pipeline=pipeline))
list_id = [item for sublist in map_id for item in sublist]
print(db['data_value'] \
      .bulk_write(list(map(lambda _id: DeleteOne({'_id': _id}), list_id))) \
      .bulk_api_result)
```