# 사용 스택

mysql 8
mongodb
kafka
kafka connector

# mysql connector

- 생성
  curl -X POST -H "Content-Type: application/json" --data @mysql-connector.json http://localhost:8083/connectors

* 삭제
  curl -X DELETE http://localhost:8083/connectors/mysql-connector

- 상태보기
  curl -i http://localhost:8083/connectors/mysql-connector/status

# mongodb connector

- 생성
  curl -X POST -H "Content-Type: application/json" --data @mongodb-sync-connector.json http://localhost:8083/connectors

* 삭제
  curl -X DELETE http://localhost:8083/connectors/mongodb-sink-connector

- 상태보기
  curl -i http://localhost:8083/connectors/mongodb-sink-connector/status

# 이슈

1. mysql 생성 뿐만 아니라 수정에도 몽고디비에 새로운 값을 저장함.
   수정인 경우 기존 반영된 몽고디비의 값도 수정이 되도록 해야함.

> mongodb sync connector 수정으로 해결.
> 아래 내용을 추가하면됨.

- mongodb-sync-connector.json

```json
"document.id.strategy": "com.mongodb.kafka.connect.sink.processor.id.strategy.PartialValueStrategy",
"document.id.strategy.partial.value.projection.type": "ALLOWLIST",
"document.id.strategy.partial.value.projection.list": "after.id"
```

2. user, post, favorite 각 테이블에 대한 캡쳐는 각각의 형태로 반영이된다.
   하나의 도큐먼트로 반영을 하고 싶으면 카프카 스트림즈를 사용하라고 한다.
