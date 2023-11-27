# Abstract
- `Index`는 `Document`들이 모여 있는 논리적인 데이터의 집합
- 하나의 노드에만 존재하지 않고 샤드 단위로 구분되어 여러 노드에 걸쳐 저장
	- 데이터 무결성의 보장
	- 검색 성능의 향상을 실현
- 모든 인덱스는 두 개의 정보 단위를 가지고 있음
	- **settings**
	- **mappings**
# Reference
- [7. 인덱스 설정과 매핑 - Settings &  Mappings](https://esbook.kimjmin.net/07-settings-and-mappings)