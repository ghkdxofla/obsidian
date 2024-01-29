# Abstract
- [[Django]] Migration Command를 정리
# Content
## 여러 Migration File 합치기
```bash
python manage.py squashmigrations <appname> <squashfrom> <squashto>
python manage.py squashmigrations example 0003 0004
```
# Reference
- [Django migration 파일들 합치기(migrations squash)](https://inspireworld.tistory.com/89)