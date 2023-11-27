# Abstract
- [[Elasticsearch]]의 [[Object & Nested#Nested]] 를 [[Django]]의 Model Field 처럼 사용 가능
# Content
## Example
- 다음과 같은 Model이 있을 때
	- OneOnOne
	- OneOnOneSchedule
	- OneOnOneAgenda
	- OneOnOneSharingMemo
- Model 간 관계는 다음과 같을 때
	- OneOnOne : OneOnOneSchedule = 1 : N 
	- OneOnOneSchedule : OneOnOneAgenda = 1 : N
	- OneOnOneSchedule : OneOnOneSharingMemo = 1 : N
```python
from django_elasticsearch_dsl import Document, fields
from django_elasticsearch_dsl.registries import registry
from .models import OneOnOne, OneOnOneSchedule, OneOnOneAgenda, OneOnOneSharingMemo

@registry.register_document
class OneOnOneDocument(Document):
    schedules = fields.NestedField(properties={
        'entity_id': fields.TextField(),
        'agendas': fields.NestedField(properties={
            'content': fields.TextField(),
        }),
        'sharing_memos': fields.NestedField(properties={
            'content': fields.TextField(),
        }),
    })

    class Index:
        name = 'oneonone_index'
        settings = {'number_of_shards': 1, 'number_of_replicas': 0}

    class Django:
        model = OneOnOne
        fields = [
            'entity_id',
        ]

    def get_queryset(self):
        return super().get_queryset().prefetch_related('oneononeschedule_set__oneononeagenda_set', 'oneononeschedule_set__oneononesharingmemo_set')

    def get_instances_from_related(self, related_instance):
        if isinstance(related_instance, OneOnOneSchedule):
            return related_instance.oneonone
        elif isinstance(related_instance, (OneOnOneAgenda, OneOnOneSharingMemo)):
            return related_instance.oneononeschedule.oneonone
```
- 단, 이렇게 생성할 경우, Document 하나에 여러 conent가 하위 Field로 있는 형태가 된다
- 즉, Document 별로 검색할 수 있는 상태가 되지 않는다