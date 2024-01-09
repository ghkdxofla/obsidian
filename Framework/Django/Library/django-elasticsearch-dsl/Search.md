# Abstract
- Elasticsearch에서 검색 Client를 다루는 부분
- 일반적으로 `ExampleDocument.search()` 형태로 도큐먼트에서 호출한다
# Content
## 기본 사용법
```python
# execute()가 필수 호출은 아니며, 호출 시 Response type으로 응답
ExampleDocument.search().query(Q('term', entity_id=entity_id)).execute()
```
# [[Trouble Shooting]]
## Query 시, 최대 10개 까지만 값이 확인되는 경우
- 기본적으로 검색 결과는 최대 10개 까지만 응답된다
- 10개 보다 많이 조회하려면
```python
s = CarDocument.search().query(query1)
total = s.count()
s = s[0:total]
cars = s.execute()
```
# Reference
- [Django ElasticSearch returns only 10 rowsets](https://stackoverflow.com/questions/58830817/django-elasticsearch-returns-only-10-rowsets)