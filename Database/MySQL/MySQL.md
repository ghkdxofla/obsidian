# Abstract
- [[TBD]]
# [[Trouble Shooting]]
# ERROR 1227 (42000) at line 18: Access denied; you need (at least one of) the SUPER, SYSTEM_VARIABLES_ADMIN or SESSION_VARIABLES_ADMIN privilege(s) for this operation
- [[RDS]]가 제공하는 [[MySQL]] 서버가 사용자가 아닌 다른 DEFINER가 지정된 sql 파일을 허용하지 않음
- mysqldump 시 `--set-gtid-purged=OFF` 옵션을 추가
- [mysql 이관 시 ERROR 1227 (42000) at line 18: Access denied; you need (at least one of) the SUPER, SYSTEM_VARIABLES_ADMIN or SESSION_VARIABLES_ADMIN privilege(s) for this operation 에러](https://sonnson.tistory.com/15)