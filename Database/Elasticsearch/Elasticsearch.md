# Abstract
- 최초 검색엔진으로 쓰기위해 만들어진 데이터베이스
- AWS 에서는 `OpenSearch` 라는 이름으로 forked version 제공
- [[Elastic Cloud]]라는 제품으로 Elastic에서 Managed Service 제공

# Content
## Setup
### Docker
```bash
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.7.1

# 이 경우, single node 설정으로 적용
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.7.1

```
### Docker Compose
```yaml
version: '2.2'
services: 
	es01: 
		image: docker.elastic.co/elasticsearch/elasticsearch:7.7.1 
		container_name: es01
		environment: 
			- node.name=es01
			- cluster.name=es-docker-cluster
			# multi node로 사용할 경우
		    - discovery.seed_hosts=es02,es03
			- cluster.initial_master_nodes=es01,es02,es03
		    # single node로 사용할 경우
			# - discovery.type=single-node
			- bootstrap.memory_lock=true
			- "ES_JAVA_OPTS=-Xms512m -Xmx512m"
			# 보안 기능 비활성화(dev only)
		    - xpack.security.enabled=false
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
	es02: 
		image: docker.elastic.co/elasticsearch/elasticsearch:7.7.1 
		container_name: es02
		environment:
			- node.name=es02
			- cluster.name=es-docker-cluster
			- discovery.seed_hosts=es01,es03
			- cluster.initial_master_nodes=es01,es02,es03
			- bootstrap.memory_lock=true
			- "ES_JAVA_OPTS=-Xms512m -Xmx512m"
		ulimits:
			memlock:
				soft: -1
				hard: -1
		volumes: 
			- data02:/usr/share/elasticsearch/data 
		networks: 
			- elastic 
	es03:
		image: docker.elastic.co/elasticsearch/elasticsearch:7.7.1 
		container_name: es03
		environment:
			- node.name=es03
			- cluster.name=es-docker-cluster
			- discovery.seed_hosts=es01,es02
			- cluster.initial_master_nodes=es01,es02,es03
			- bootstrap.memory_lock=true
			- "ES_JAVA_OPTS=-Xms512m -Xmx512m"
		ulimits: 
			memlock: 
				soft: -1 
				hard: -1 
		volumes: 
			- data03:/usr/share/elasticsearch/data 
		networks: 
			- elastic
volumes: 
	data01: 
		driver: local 
	data02: 
		driver: local 
	data03: 
		driver: local 
		
networks: 
	elastic: 
		driver: bridge
```
# [[Trouble Shooting]]
### Docker compose로 올렸을 때, 초기 기동 후 종료되는 경우
- Memory issue일 수 있다
	- `ERROR: Elasticsearch exited unexpectedly, with exit code 78`
	- `ERROR: Elasticsearch exited unexpectedly, with exit code 137 es02 exited with code 137`
# Reference
- [Docker Compose로 Elasticsearch 설정](https://soyoung-new-challenge.tistory.com/110)
- [Elasticsearch, Kibana를 docker-compose로 구동](https://kanoos-stu.tistory.com/34)