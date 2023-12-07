# Abstract
- [[Elastic Beanstalk]]을 구성하는 방법을 설명한다
# Setup
## EC2 Key pair 생성
- EC2 -> 네트워크 및 보안 > 키 페어 > `키 페어 생성` 클릭
![[Pasted image 20231123200534.png]]
- 키 페어 설정에 맞게 입력 후 추가
![[Pasted image 20231123200619.png]]
## IAM 설정
### Elastic Beanstalk에 EC2 Role 추가
- IAM > 역할에서 `역할 생성` 클릭
![[Pasted image 20231123202826.png]]
- `AWS 서비스` 선택 후, 사용 사례에서 `EC2` 선택
![[Pasted image 20231123202917.png]]
- 다음의 3개 권한 추가
	- **AWSElasticBeanstalkWebTier**
	- **AWSElasticBeanstalkWorkerTier**
	- **AWSElasticBeanstalkMulticontainerDocker**
![[Pasted image 20231123193941.png]]
- 이름 설정
	- ex) `aws-elasticbeanstalk-ec2-role`
![[Pasted image 20231123193920.png]]
- 정책에 추가한 후, 역할 이름 aws-elasticbeanstalk-ec2-role로 만들면 EC2 인스턴스 프로파일에 프로파일이 생긴다
## 환경 구성
- Elastic Beanstalk 서비스로 이동 후, 환경 구성 시작
![[Pasted image 20231123210057.png]]
![[Pasted image 20231123210110.png]]
- `사전 설정`의 경우, 고가용성으로 해야 scale out 가능
![[Pasted image 20231123225642.png]]
- 처음 구성하는 경우, `새 서비스 역할 생성 및 사용`으로 서비스 역할을 위한 IAM 생성
![[Pasted image 20231123233428.png]]
- VPC 및 인스턴스 서브넷 설정
	- 퍼블릭 IP 주소 활성화 시 배포된 EC2 Instance에 외부에서 접근 가능
![[Pasted image 20231123233517.png]]
- 데이터베이스 서브넷 설정
![[Pasted image 20231123233533.png]]
- RDS를 함께 생성할 수 있다
	- **[주의!!!]** 이 경우, `데이터베이스 삭제 정책`을 `삭제`로 할 경우, Elastic Beanstalk가 삭제될 때 같이 삭제되므로 주의해야 한다
	- [주의!!!] 데이터베이스를 이후 분리한다해도, 이렇게 설정된 RDS가 있는 경우, 같은 `SecurityGroup`을 사용하여 환경 삭제가 제대로 되지 않으므로, 환경 삭제 전 RDS의 `SecurityGroup`을 변경해야 한다
- 인스턴스 기본 설정
![[Pasted image 20231125120816.png]]
- 보안 그룹도 설정한다
![[Pasted image 20231125120834.png]]
- Auto scaling group의 경우, scale-out 할지(밸런싱된 로드) 안할지를 지정한다
![[Pasted image 20231125120933.png]]
- 어떤 지표로 인스턴스의 증감을 할지 지정한다
![[Pasted image 20231125121009.png]]
- Load Balancer 설정
![[Pasted image 20231125121029.png]]
- Health Check를 위한 URI 설정
![[Pasted image 20231125121102.png]]
- 모니터링 설정
![[Pasted image 20231125121648.png]]
- 배포 정책 설정
	- `추가 배치를 사용한 롤링`을 선택할 경우, 배포 시 새로운 인스턴스를 생성하고, 해당 인스턴스로 교체 후, 기존의 인스턴스를 종료하는 과정을 거친다
	- **[주의!!!]**Docker로 배포 시, 기존 인스턴스에 배포하면 인스턴스가 `응답 없음` 상태로 빠지는 경우가 있음
![[Pasted image 20231125121758.png]]
- 롤링 업데이트 설정
	- `비활성화됨` 선택 시, 배포 후 일괄 교체
![[Pasted image 20231125121955.png]]
- 환경 변수 설정
	- 배포 후 추가 가능
![[Pasted image 20231125122050.png]]