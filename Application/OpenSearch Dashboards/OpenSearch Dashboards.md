# Abstract
- [[OpenSearch]]에서 [[Kibana]]와 대응하는 Dashboard
# Content
## Masking Field 추가하기
1. Dashboards의 Side Menu -> Security -> Roles -> `Create role` 클릭
2. Create Role에서 다음의 설정값 지정
	1. Name
	2. Index permissions
		1. Index는 전체 범위 시 `*` 지정
		2. Index permissions에는 `data_access` 지정
		3. Anonymization에 Masking할 Field 지정
		- ![[Pasted image 20231215170404.png]]
3. Dashboards의 Side Menu -> Security -> Roles -> 추가한 Role 검색 후 클릭
4. `Mapped users`에서 Field에 Masking을 지정할 User 지정
	- ![[Pasted image 20231215170713.png]]
5. 추가로, `all_access` 도 추가해야 메뉴 접근 등이 가능하다
	- ![[Pasted image 20231215170056.png]]

# Reference
- [Masking field values with Amazon Elasticsearch Service](https://aws.amazon.com/ko/blogs/security/masking-field-values-with-amazon-elasticsearch-service/)
- [Field masking](https://opensearch.org/docs/1.2/security-plugin/access-control/field-masking/)