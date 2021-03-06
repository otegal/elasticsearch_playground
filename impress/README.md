# impress

# env
- Elasticsearch: `7.6.2`
- Kibana: `7.6.2`

# Document operation
## CRUD
### Create

- PUTの場合IDを指定して登録される
```sh
curl -XPUT "http://localhost:9200/my_index/_doc/1" -H 'Content-Type: application/json' -d'{  "user_name": "John Smith",  "date": "2019-01-06T15:09:45",  "message": "Hello Elasticsearch world."}'
```

- POSTの場合IDが自動採番される
```sh
curl -XPOST "http://localhost:9200/my_index/_doc" -H 'Content-Type: application/json' -d'{  "user_name": "John Smith",  "date": "2019-01-06T15:09:45",  "message": "Hello Elasticsearch world."}'
```

### Read
- _docを利用すると管理上のメタデータも取得する
```sh
curl -XGET "http://localhost:9200/my_index/_doc/1"
```

- _sourceを利用すると自分で登録したデータのみ取得する
```sh
curl -XGET "http://localhost:9200/my_index/_source/1"
```

- _searchを利用するとクエリを用いて検索できる
```sh
curl -XGET "http://localhost:9200/my_index/_search" -H 'Content-Type: application/json' -d'{  "query": {    "match": {      "message": "Elasticsearch"    }  }}'
```


### Update
- 既存ドキュメント全体を置き換える
```sh
curl -XPUT "http://localhost:9200/my_index/_doc/1" -H 'Content-Type: application/json' -d'{  "user_name": "Mike Stuart",  "date": "2019-10-06T16:36:12",  "message": "This message was updated."}'
```

- 既存ドキュメントの一部のフィールドを置き換える
```sh
curl -XPOST "http://localhost:9200/my_index/_update/1" -H 'Content-Type: application/json' -d'{  "doc": {    "message": "Only message was updated."  }}'
```

### Delete
- ID指定でドキュメントを削除する
```sh
curl -XDELETE "http://localhost:9200/my_index/_doc/1"
```
