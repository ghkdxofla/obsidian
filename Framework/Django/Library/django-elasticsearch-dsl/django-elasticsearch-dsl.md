# Abstract
- [[Elasticsearch]]를 [[Python]]에서 쉽게 사용하게 해주는 `elasticsearch-dsl` [[Library/Library]]의 [[Django]] 에 쓰기 편한 형태로 만든 [[Library/Library]]
- [[Django]] 에서 사용하는 Model 정의와 유사하게 `Document`를 구성할 수 있음
- drf를 여기에 추가한 것이 [[django-elasticsearch-dsl-drf]]
# Content
## Setup
- pipenv를 사용하는 경우, `Pipfile`에 추가
```
...
django-elasticsearch-dsl = "*"
```
- pip에 install하는 경우
```bash
pip install django-elasticsearch-dsl
```
- [[Elasticsearch]] 설치의 경우, [[Elasticsearch#Docker Compose]] 참고
## Configuration
### Local Elasticsearch와 연동하기
- `settings.py`에 추가
```python
INSTALLED_APPS += [
    # Django Elasticsearch DSL
    'django_elasticsearch_dsl',
]

# Elasticsearch
ELASTICSEARCH_DSL = {
    'default': {
        'hosts': 'http://localhost:9200', # Elasticsearch의 server 주소
    },
}
```
### Elastic Cloud와 연동하기
`settings.py`에 추가
```python
INSTALLED_APPS += [
    # Django Elasticsearch DSL
    'django_elasticsearch_dsl',
]

# CLOUD_ID, CLOUD_PASSWORD
CLOUD_ID = "{BRING_YOUR_OWN_CLOUD_ID}"
CLOUD_PASSWORD = "{BRING_YOUR_OWN_CLOUD_PASSWORD}"

# Elasticsearch
ELASTICSEARCH_DSL = {  
   'default': {   
	   'cloud_id': CLOUD_ID,  
	   'basic_auth': ('elastic', CLOUD_PASSWORD),  
   },  
}
```
- [참고](https://www.elastic.co/guide/en/elasticsearch/client/python-api/8.0/connecting.html#connect-ec)
### 추가 Configuration
- 기본적으로 `ELASTICSEARCH_DSL_AUTOSYNC`=true라, 자동으로 sync 된다
- [참고](https://django-elasticsearch-dsl.readthedocs.io/en/latest/settings.html)
### Tokenizer
#### Elastic Cloud에서 Tokenizer 설정하기

## Example
#### Document 등록
```python
from django_elasticsearch_dsl import Document, fields
from django_elasticsearch_dsl.registries import registry
from elasticsearch_dsl import analyzer

from project import ExampleModel


# Nori tokenizer 추가
nori_analyzer = analyzer(
    'nori_tokenizer',
    tokenizer='nori_tokenizer',
)


@registry.register_document
class ExampleModelDocument(Document):
    entity_id = fields.TextField()
    content = fields.TextField(analyzer=nori_analyzer)

    class Index:
        name = 'example_model'
        # See Elasticsearch Indices API reference for available settings
        settings = {'number_of_shards': 1, 'number_of_replicas': 1}
        html_strip = analyzer(
            'html_strip',
            tokenizer="standard",
            filter=["standard", "lowercase", "stop", "snowball"],
            char_filter=["html_strip"],
        )

    class Django:
        model = ExampleModel
```
## `get_instances_from_related()` 의 목적?
- `get_instances_from_related()` is used when one of the `related_models` changes (in our case a `Parent` object). 
- `django_elasticsearch_dsl` needs a list of all the `Child` objects which reference the `parent` object so it can update the `parent` field of each `child` in the index.

# Reference
- [ElasticSearch 2화: ES 라이브러리 탐방기](https://medium.com/elecle-bike/elasticsearch-2%ED%99%94-es-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%83%90%EB%B0%A9%EA%B8%B0-a23ebdff0290)
- [Elasticsearch와 Django를 연동해 검색 API 개발](https://livetodaykono.tistory.com/64)
- [How to use Elasticsearch with Django?](https://sunscrapers.com/blog/how-to-use-elasticsearch-with-django/)
- [What is the purpose of def get_instances_from_related() method in django_elasticsearch_dsl](https://stackoverflow.com/questions/75822692/what-is-the-purpose-of-def-get-instances-from-related-method-in-django-elastic)