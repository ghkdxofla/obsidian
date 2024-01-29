# Abstract
- [[Strapi]]와 다른 App 간 Integration을 설명
# Content
## [[Google App Engine]] 과 연동
- [링크 참고](https://forum.strapi.io/c/community-guides/28)
- 기본적으로 `app.yaml`에 다음 환경 변수 세팅
```yaml
service: strapi

runtime: nodejs18
instance_class: F2

env_variables:
  HOST: '0.0.0.0'
  PUBLIC_URL: 'https://xxxxx.nw.r.appspot.com/strapi'
  NODE_ENV: 'production'
  DATABASE_CLIENT: 'postgres'
  DATABASE_HOST: '/cloudsql/xxxxx:europe-west2:strapi-database'
  DATABASE_NAME: 'bloom_demo'
  DATABASE_USERNAME: 'strapi'
  DATABASE_PASSWORD: 'xxxxx'
  APP_KEYS: "xxxxx"
  API_TOKEN_SALT: "xxxxx"
  ADMIN_JWT_SECRET: "xxxxx"
  TRANSFER_TOKEN_SALT: "xxxxx"
  JWT_SECRET: "xxxxx"

build_env_variables:
  NODE_ENV: 'production'
  PUBLIC_URL: 'https://xxxxx.nw.r.appspot.com/strapi'
  APP_KEYS: "xxxxx"
  API_TOKEN_SALT: "xxxxx"
  ADMIN_JWT_SECRET: "xxxxx"
  TRANSFER_TOKEN_SALT: "xxxxx"
  JWT_SECRET: "xxxxx"
```