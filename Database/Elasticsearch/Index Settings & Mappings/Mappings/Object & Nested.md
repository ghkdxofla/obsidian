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