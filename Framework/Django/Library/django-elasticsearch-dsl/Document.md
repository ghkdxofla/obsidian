# Abstract
- [[Elasticsearch]] 에서 저장되는 데이터 단위를 [[Django]]에서 쓸 수 있도록 Wrapping한 Object
- [[Django]]의 Model과 유사한 동작 및 Method를 가지고 있음
# Content
## `bulk`로 Data 처리하기
```python
objects = Item.objects.all().order_by('id')[1:10000]
ItemDocument().update(objects)
```