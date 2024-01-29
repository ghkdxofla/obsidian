# Abstract
- 샤드 수(`number_of_shards`) 나 복제본 수(`number_of_replicas`) 같은 정보는 settings 아래 설정
	- 샤드 수는 6.x 버전 까지는 디폴트로 5개가 설정, 7.0 부터는 디폴트 1개로 설정
- `number_of_shards`는 Index 처음 설정 때 한 번 지정 가능하고, 추후에 바꿀 수 없음
	- 바꾸려면 새로 Index 정의 하고, 기존 Index의 데이터를 재색인 해야 함
- `number_of_replicas` 설정은 다이나믹하게 변경이 가능
- `refresh_interval`
	- Elasticsearch 에서 세그먼트가 만들어지는 리프레시 타임을 설정하는 값
	- 설정 변경이 가능한 다이나믹 설정
- `analyzer`, `tokenizer`, `filter`
	- 한번 생성 후 변경은 불가능
	- 이미 만들어진 인덱스에 analyzer나 tokenizer 등을 추가하거나 사전을 변경하려면 index를 먼저 `_close` 한 후에 추가하고 다시 `_open` 해서 적용
# Content
## 생성 시 JSON 형태
- shards, replicas, refresh interval
```json
PUT my_index
 {
   "settings": {
     "index": {
       "number_of_shards": 3,
       "number_of_replicas": 1,
       "refresh_interval": "30s"
     }
   }
 }
```
- analyzer, tokenizer, filter
```json
PUT my_index
{
  "settings": {
    "analysis": {
      "analyzer": {
        "my_analyzer": {
          "type": "custom",
          "char_flter": [ "...", "..." ... ]
          "tokenizer": "...",
          "filter": [ "...", "..." ... ]
        }
      },
      "char_filter":{
        "my_char_filter":{
          "type": "…"
          ... 
        }
      }
      "tokenizer": {
        "my_tokenizer":{
          "type": "…"
          ...
        }
      },
      "filter": {
        "my_token_filter": {
          "type": "…"
          ...
        }
      }
    }
  }
}
```
# Reference
- [7.1 설정 - Settings](https://esbook.kimjmin.net/07-settings-and-mappings/7.1-settings)
- [Sizing Amazon OpenSearch Service domains](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/sizing-domains.html)