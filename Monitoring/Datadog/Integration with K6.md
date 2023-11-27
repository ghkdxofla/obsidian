# Abstract
- [[K6]]와 연동하는 방법 설명
# Content
## Sign up
- [Datadog](https://www.datadoghq.com/) 회원가입
    - Free trial 계정을 만든다면 [https://temp-mail.org/](https://temp-mail.org/) 같은 임시 이메일 서비스 활용
    - **Gmail 등의 서비스에서 + 연산자를 이용한 별칭 주소로도 추가 생성 가능**
# Setup
- Datadog agent 설치 및 API Key 세팅
    - [설치 안내 문서]([https://app.datadoghq.com/account/settings?_gl=1*1qy7mr1*_ga*ODM1MzU3MzEuMTYzMjM3OTkzMg](https://app.datadoghq.com/account/settings?_gl=1*1qy7mr1*_ga*ODM1MzU3MzEuMTYzMjM3OTkzMg)..__ga_KN80RDFSQK_MTYzMjM4MjM0My4yLjEuMTYzMjM4MjUxMC4w#agent/mac)에 따라 설치
	- Mac 기준
```bash
DD_AGENT_MAJOR_VERSION=7 DD_API_KEY={API_KEY}
DD_SITE="ap1.datadoghq.com" 
bash -c "$(curl -L https://s3.amazonaws.com/dd-agent/scripts/install_mac_os.sh)"
```
