# Abstract
- 한글 형태소 분석기로, Elastic사에서 공식적으로 개발해서 지원을 하기 시작
- Nori 는 **은전한닢**에서 사용하는 **mecab-ko-dic** 사전을 재 가공 하여 사용
# Setup
### elasticsearch 설치 후 다음 명령어 실행
```bash
bin/elasticsearch-plugin install analysis-nori
```
### Docker Compose를 사용하는 경우
- [[Elasticsearch]]의 Docker Compose 부분 참고
- 추가로, 아래 command를 yaml에 추가한다
```yaml
version: '3'  
  
services:
  es01  
    image: docker.elastic.co/elasticsearch/elasticsearch:8.10.4
    container_name: es01
    environment:
      - node.name=es01
      - cluster.name=es-docker-cluster
      - discovery.type=single-node
      - bootstrap.memory_lock=true
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
    # 한글 형태소 분석기 Nori 설치
    command: >
      /bin/sh -c "./bin/elasticsearch-plugin list | grep -q analysis-nori
      || ./bin/elasticsearch-plugin install analysis-nori; 
      /usr/local/bin/docker-entrypoint.sh"
```
# Reference
https://stackoverflow.com/questions/39691652/how-to-install-elasticseach-plugins-using-docker-compose