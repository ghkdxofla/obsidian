# Abstract
- Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker 등 다양한 언어와 플랫폼에서 개발된 웹 애플리케이션 및 서비스를 배포하고 확장하는 데 사용
- Apache, Nginx, Passenger, IIS 제공
- Platform As A Service (PaaS)
- 사전 구성된 EC2 서버 및 기타 AWS 서비스를 사용
- 리소스 프로비저닝, 로드 밸런싱, 자동 스케일링, 모니터링과 같은 세부 사항을 처리
# Content
- [[Infra 설정]]
- [[Network 설정]]
## Debugging 방법
1. AWS Console > Elastic Beanstalk > Environment > ${YOUR_APPLICATION_ENV} > Log > Request Logs > Download > Open in any text editor
2. Instance 접속 후 다음 경로로 접근
	`/var/log/eb-docker/containers/eb-current-app/`
# Reference
- [AWS Elastic Beanstalk nginx 설정](https://greeng00se.tistory.com/135)
- [AWS Elastic Beanstalk 상태 unknown 오류 해결방법](https://dangdangee.tistory.com/entry/AWS-Elastic-Beanstalk-%EC%83%81%ED%83%9C-unknown-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95)
- [docker-compose로 구성된 서버 Elastic Beanstalk에 배포하기](https://well-balanced.medium.com/docker-compose%EB%A1%9C-%EA%B5%AC%EC%84%B1%EB%90%9C-%EC%84%9C%EB%B2%84-elastic-beanstalk%EC%97%90-%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0-58fe8f993b5d)
- [Debugging Elastic Beanstalk Docker run failures?](https://stackoverflow.com/questions/30358977/debugging-elastic-beanstalk-docker-run-failures)