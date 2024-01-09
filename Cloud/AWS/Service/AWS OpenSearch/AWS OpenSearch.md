# Abstract
- [[Elasticsearch]]의 Fork 후 Open Source 버전인 [[OpenSearch]]의 AWS 제공판
- 업데이트가 활발하지는 않음
- 최근에 OpenSearch 전용 Instance가 추가됨
# Content
## Setup
### 공통
- Amazon OpenSearch Service -> 대시보드 -> `도메인 생성`
![[Pasted image 20240102165441.png]]
- 도메인 이름 입력 및 `표준 생성` 클릭 후 세팅 시작
![[Pasted image 20240102165639.png]]
- 네트워크 설정의 경우, 구성된 AWS 인프라에 맞게 지정
![[Pasted image 20240102170245.png]]
- 계정 설정의 경우, OpenSearch Dashboard나 OpenSearch 접속을 위한 Master User 생성이 필요함
	- `IAM ARN을 마스터 사용자로 설정`할 경우, AWS 계정의 IAM ARN을 이용하여 Master User 생성됨
		- 이 부분 설정 후 사용은 하지 않아, 자세한 사항은 검색 필요
	- `마스터 사용자 생성`을 선택할 경우, ID, Password 지정 후 사용 가능한 별도의 Master User 생성됨
		- 해당 ID, Password를 통해 사용하는 서비스에서 OpenSearch 접근 가능 확인
![[Pasted image 20240102170413.png]]
- 이 외의 아래의 [[AWS OpenSearch#Development]] 및 [[AWS OpenSearch#Production]] 설정을 추가
- 여기서 다루지 않는 설정은 문서 참조하여 진행
### Development
- **Production에서 사용은 어려운 구성으로, 개발 환경에 적합함**
- ([[AWS OpenSearch#공통]]에 이어서) 템플릿을 `개발 및 테스트` 선택
![[Pasted image 20240102165905.png]]
- 배포 옵션에서 `1-AZ` 설정
![[Pasted image 20240102165939.png]]
- 인스턴스 유형은 t3도 가능하며, 환경에 맞게 설정
	- t3은 Production에서는 사용 불가
	- 환경에 맞게 노드 수 및 스토리지 크기 구성
- 데이터 노드에 알맞은 인스턴스 유형, 스토리지 유형 설정
![[Pasted image 20240102170033.png]]
- 개발 환경의 경우, 데이터 노드만 세팅해도 동작 가능
	- 비용 절감을 위해 `전용 프라이머리 노드` 비활성화 가능
![[Pasted image 20240102185204.png]]
### Production
#### 구현 시 필요한 최소 Spec
- 3개의 Instance
- 2개의 Shard
- ([[AWS OpenSearch#공통]]에 이어서) 템플릿을 `프로덕션` 선택
![[Pasted image 20240102171320.png]]
- 배포 옵션 지정
![[Pasted image 20240102171401.png]]
- 인스턴스 유형은 최소 large 이상에서 선택 가능하고, 상황에 따라 CPU, Memory, Storage 최적화 인스턴스 선택
- 데이터 노드에 알맞은 인스턴스 유형 및 스토리지 유형 설정
	- 노드 수의 경우, 가용 영역의 배수로 지정
![[Pasted image 20240102184945.png]]
- `프라이머리 노드`의 경우, 프로덕션의 경우 필수로 설정해야 하며, AZ 당 1개의 노드 설정
![[Pasted image 20240102190453.png]]
### SAML 설정

## Text Analysis 추가
- [링크](https://github.com/awslabs/text-analysis-with-amazon-opensearch-service-and-amazon-comprehend) 참고
	- Cloud Formation Template가 있고, AWS의 여러 제품을 활용하여 텍스트 분석에 [[OpenSearch]] 활용 예시를 보여줌
	- https://aws.amazon.com/ko/solutions/implementations/text-analysis-with-amazon-opensearch-service-and-amazon-comprehend/
# Github Actions에서 사용
- [Repository](https://github.com/ankane/setup-opensearch) 참고
# Reference