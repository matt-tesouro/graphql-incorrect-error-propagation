## Startup

```shell
docker-compose up -d
````


## GraphQL responses from Subgraph (simulator) directly

### Response Code 200 -- Content-Type: application/json

```shell
 curl -X POST -v http://localhost:8081/foo/graphql
```

Response: 

```json
{"errors":[{"message":"UUID cannot parse the given literal of type 'StringValueNode'.","path":["input","acceptorId"],"extensions":{"field":"Foo.acceptorId","fieldType":"UUID"}}]}
```

### Response Code 400 -- Content-Type: application/graphql-response+json 

```shell
 curl -X POST -v http://localhost:8081/bar/graphql
```

Response:

```json
{"errors":[{"message":"UUID cannot parse the given literal of type 'StringValueNode'.","path":["input","acceptorId"],"extensions":{"field":"Foo.acceptorId","fieldType":"UUID"}}]}
```

## GraphQL responses when queries go through Router

### Response Code 200 -- Content-Type: application/json

```shell
 curl -X POST -H "Content-Type: application/json" -d '{"query": "{ foo { id } }"}' http://localhost:8080/graphql
```

Response:

```json
{"data":null}
```

### Response Code 400 -- Content-Type: application/graphql-response+json

```shell
 curl -X POST -H "Content-Type: application/json" -d '{"query": "{ bar { id } }"}' http://localhost:8080/graphql
```

Response: 

```json
{"data":null,"errors":[{"message":"HTTP fetch failed from 'bar': 400: Bad Request","extensions":{"code":"SUBREQUEST_HTTP_ERROR","service":"bar","reason":"400: Bad Request","http":{"status":400}}}]}
```

## Compose Supergraph Schema from Subgraphs

```shell
rover supergraph compose --config supergraph.yml -o supergrapah.graphql
```