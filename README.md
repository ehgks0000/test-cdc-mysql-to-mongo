# mysql connector

- 생성 curl -X POST -H "Content-Type: application/json" --data @mysql-connector.json http://localhost:8083/connectors

* 삭제 curl -X DELETE http://localhost:8083/connectors/mysql-connector

- 상태보기 curl -i http://localhost:8083/connectors/mysql-connector/status

# mongodb connector

- curl -X POST -H "Content-Type: application/json" --data @mongodb-sync-connector.json http://localhost:8083/connectors

* 삭제 curl -X DELETE http://localhost:8083/connectors/mongodb-sink-connector

- 상태보기 curl -i http://localhost:8083/connectors/mongodb-sink-connector/status
