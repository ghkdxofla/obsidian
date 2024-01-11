# Abstract
- Document 내에 중첩된 Field 형태로 구성할 수 있음
- 하위 Field 형태
# Content
## Object vs Nested?
- `Object`와 `Nested`는 사용 형태에 따라 다름
### Object
- JSON Object와 유사한 구조
- 단일 Entity나 Object 표현
- 부모 Document의 일부로 취급되어 함께 Indexing
	- 즉, 내부 Field가 독립적으로 검색되지 않고, 전체 Object의 맥락으로 검색됨
### Nested
- Json Array와 유사한 구조
- 내부 Object는 독립적인 문서로 취급됨
- 각 객체가 개별적으로 Indexing
	- 각 중첩 객체 내부의 필드들에 대한 복잡한 검색 쿼리를 수행 가능
- [[django-elasticsearch-dsl]]에서는 [[Nested Field]]로 사용
## 검색 결과의 차이점
- 다음의 쿼리를 수행할 때
```null
GET person/_search
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {"address.country": "KR"}
        },
        {
          "term": {"address.city": "LOS ANGELES"}
        }
      ]
    }
  }
}
```
- Object
	- 검색이 가능
	- KR, LOS ANGELES가 모두 하나의 Document에 소속된 것이므로 검색
	![[Pasted image 20240111155334.png]]
- Nested
	- 검색 불가
	- KR, LOS ANGELES가 각각의 Document에 저장되고, 이를 Parent Document에 포함된 관계이므로
	![[Pasted image 20240111155602.png]]
# Reference
- [Nested와 Object 차이, 데이터 저장 원리](https://velog.io/@jkh9615/ElasticSearch-Nested%EC%99%80-Object-%EC%B0%A8%EC%9D%B4-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A0%80%EC%9E%A5-%EC%9B%90%EB%A6%AC)