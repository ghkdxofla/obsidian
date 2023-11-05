# Abstract

# Setup
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
			- discovery.seed_hosts=es02,es03
			- cluster.initial_master_nodes=es01,es02,es03
			- bootstrap.memory_lock=true
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
# [[Trouble-Shooting]]
### Docker compose로 올렸을 때, 초기 기동 후 종료되는 경우
- Memory issue일 수 있다
	- `ERROR: Elasticsearch exited unexpectedly, with exit code 78`
	- `ERROR: Elasticsearch exited unexpectedly, with exit code 137 es02 exited with code 137`
# Reference
[Docker Compose로 Elasticsearch 설정](https://soyoung-new-challenge.tistory.com/110)