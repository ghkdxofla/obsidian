# Abstract
# Setup
## [[Nginx]] 설정
- Elastic Beanstalk은 기본적으로 nginx를 역방향 프록시 서버로 사용
### Directory 구조
```bash
project
|-- .platform
|   `-- nginx
|       `-- conf.d
|           `-- myconf.conf
```
### [[CORS]] 설정
```
map_hash_bucket_size 128;
map $http_origin $allow_origin {
    default "";
    "~*(^http.*)(localhost)" $http_origin;
}

add_header 'Access-Control-Allow-Origin' $allow_origin always;
add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, PATCH, OPTIONS' always;
add_header 'Access-Control-Allow-Headers' 'DNT,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Range';
add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range';
```
**주의할 점!**
	- `always` 키워드를 쓰지 않으면 정상 응답에서만 헤더에 적용됨
	- 400대 Error에서는 적용되지 않아 CORS 문제가 지속 발생할 수 있음
# Reference
- [AWS Elastic Beanstalk nginx 설정](https://greeng00se.tistory.com/135)