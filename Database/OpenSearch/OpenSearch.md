# Abstract
- [[Elasticsearch]]의 Forked version
- Open Source
- [[AWS]]에서만 제공
# Content
## [[Elasticsearch]] VS OpenSearch?
||OpenSearch Serverless|OpenSearch|Elasticsearch|
|---|---|---|---|
|비용|**사용량에 따라 다름**|비쌈 - 추산 시 최소 58만원 ~ 110만원 대 - 사용 크기 보다는 인스턴스의 고정 비용이 비쌈|**매우** **저렴함 - 220GB 추산 시 최소 23만원 ~ 46만원 대 - 20GB 추산 시 6만원 대 - 초기 free trial 가능**|
|운영|쉬움(Managed Service)|**쉬움(Managed Service)**|~~어려움(Unmanaged Service)~~ Elastic Cloud를 통해 구축이 쉬울 수 있음 단, [cloud.elastic.co](http://cloud.elastic.co/)에서 별도 관리가 필요해보임|
|보안성|- AWS의 다른 서비스로 보안성 확보 가능 - Masking Field 되는지 확인 필요|- AWS의 다른 서비스로 보안성 확보 가능 **- LDAP, SAML 연동 등 보안성에서는 더 높음** - Masking Field 설정 가능|**- 자체 보안성 + AWS에서 구축하면 AWS의 보안도 사용 가능** - Masking Field 설정 가능|
|구축 난이도|**- 설정 자체는 쉬움** - 확장성에 제한이 있으므로 Fine Tuning할 때 어려움 예상|- 다소 어려움 ==**- Documentation이 아직 미흡함**==|**쉬움**|
|확장성|- 매우 낮음 - OpenSearch ↔ OpenSearch Serverless 간 Migration도 추가로 필요 **==- 아직 서울 리전에서는 제공되지 않음==**|- 낮음 - AWS에서만 사용 가능|**- 높음** - 여러 클라우드에 사용 가능|
|플러그인|자유도 낮음|자유도 중간|**자유도 높음**|
|Django호환 여부|==**직접 연동 필요 및 리서치 해야 함**==|django-opensearch-dsl로 연동 가능(단, 라이브러리 스타가 18개로 적다)|**django-elasticsearch-ds**l로 연동 가능|
|사용 예시|검색 사용량이 매우 가변적이고, 양이 적을 경우|**어플리케이션 검색**|분석 및 기계학습 확장, Fuzzy search|
|종합|설정은 쉬우나 Region 미지원 및 초기 단계의 서비스이므로 적용 어려움|AWS에서 클라우드 변경할 경우가 아니라면 적용 시 보안적 측면과 다른 서비스와 연결 측면에서 좋음 염려점 : Django 호환 라이브러리가 star 수가 적은 점|Elastic Cloud를 통해 구축이 쉬울 수 있음 단, [cloud.elastic.co](http://cloud.elastic.co/)에서 별도 관리가 필요해보임 **성능 대비 비용이 저렴하다는 것이 큰 장점** - 동 성능|
## Setup
- [[TBD]]

# Reference
- [Amazon OpenSearch Deep dive - 내부구조, 성능최적화 그리고 스케일링](https://www.slideshare.net/awskorea/t2s2pdf)
	- 비용 산정이나 어떻게 구성해야할지 모른다면 이 슬라이드가 최고
- [# 후기 서비스 AWS Opensearch 도입기](https://helloworld.kurly.com/blog/2023-review-opensearch/)
	- OpenSearch 도입 과정에서 겪은 이슈나 성능 측정 등 자세하게 나와있음