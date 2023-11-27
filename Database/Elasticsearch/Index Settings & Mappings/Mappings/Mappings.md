# Abstract
- 데이터 명세인 Index Mapping
- 기본적으로 Dynamic Mapping 지원
	- 필드의 값을 보고 타입을 예상
	- 항상 그 필드가 포함될 수 있는 가장 넓은 범위 형태의 데이터 타입을 선택
# Content
## 직접 Mapping 정의를 할 경우
```json
PUT <인덱스명>
{
  "mappings": {
    "properties": {
      "<필드명>":{
        "type": "<필드 타입>"
        … <필드 설정>
      }
      …
    }
  }
}
```
# Reference
- [7.2 매핑 - Mappings](https://esbook.kimjmin.net/07-settings-and-mappings/7.2-mappings)