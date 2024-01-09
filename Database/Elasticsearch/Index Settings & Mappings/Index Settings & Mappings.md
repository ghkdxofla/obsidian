# Abstract
- `Index`는 `Document`들이 모여 있는 논리적인 데이터의 집합
- 하나의 노드에만 존재하지 않고 샤드 단위로 구분되어 여러 노드에 걸쳐 저장
	- 데이터 무결성의 보장
	- 검색 성능의 향상을 실현
- 모든 인덱스는 두 개의 정보 단위를 가지고 있음
	- **settings**
	- **mappings**
# Content
## Indexing 최적화를 통한 검색 성능 최적화
- [[TBD]]
- 아래의 `실시간 인덱싱을 위한 Elasticsearch 구조를 찾아서` 참고
# Reference
- [7. 인덱스 설정과 매핑 - Settings &  Mappings](https://esbook.kimjmin.net/07-settings-and-mappings)
- [실시간 인덱싱을 위한 Elasticsearch 구조를 찾아서](https://techblog.woowahan.com/7425/)
- [Use flat object in OpenSearch](https://opensearch.org/blog/flat-object/)