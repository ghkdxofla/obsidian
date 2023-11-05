# Abstract
- [[Database]]를 위한 대시보드 플랫폼
- 제공하는 기능
	1. **데이터 시각화**: 다양한 종류의 차트, 테이블, 맵 등을 사용하여 데이터를 시각적으로 표현합니다.
	2. **대시보드**: 여러 시각화를 하나의 대시보드로 조합하여 통합된 뷰를 제공합니다.
	3. **데이터 탐색**: Elasticsearch에 저장된 데이터를 검색하고 필터링할 수 있는 기능을 제공합니다.
	4. **머신 러닝**: 데이터의 이상 징후를 감지하고 예측 분석을 수행할 수 있습니다.
	5. **보고서 생성**: 시각화 및 대시보드를 PDF, CSV 등의 형태로 내보낼 수 있습니다.
# [[Trouble-Shooting]]
### 8.x 버전 이상에서 `error code 78` 등으로 shotdown될 경우
- 8.x 버전 이상부터 보안이 강화되어 [[Database]]에 옵션을 주지 않으면 보안 이슈로 종료됨
- `xpack.security.enabled=false`로 비활성화
	- 운영 환경에서는 해당 옵션을 주어야 한다
```yaml
es01:  
  image: docker.elastic.co/elasticsearch/elasticsearch:8.10.4  
  container_name: es01  
  environment:  
    - node.name=es01  
    - cluster.name=es-docker-cluster  
    - discovery.type=single-node  
    #      - discovery.seed_hosts=es02,es03  
    #      - cluster.initial_master_nodes=es01,es02,es03    - bootstrap.memory_lock=true  
    - xpack.security.enabled=false # 보안 기능 비활성화(dev only)  
    - "ES_JAVA_OPTS=-Xms512m -Xmx512m"  
  ulimits:  
    memlock:  
      soft: -1  
      hard: -1  
  volumes:  
    - data01:/usr/share/elasticsearch/data  
  ports:  
    - 9200:9200  
  networks:  
    - elastic
```
# Reference
[Elasticsearch Docker - ES, Kibana](https://velog.io/@mertyn88/Docker-ES-Kibana)
[Kibana 시작하기 및 사용방법](https://velog.io/@jskim/Kibana-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%B0%8F-%EC%82%AC%EC%9A%A9%EB%B0%A9%EB%B2%95)