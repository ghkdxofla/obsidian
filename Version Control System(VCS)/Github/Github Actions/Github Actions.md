# Abstract
- [[CI & CD]] 설정을 통해 Github에 있는 코드를 배포 및 테스트 하는데 주로 사용
# Content
## Input에 대해 Masking 처리하기
- [Masking Input Parameters in GitHub Actions](https://dev.to/leading-edje/masking-input-parameters-in-github-actions-1ci)
# [[Trouble Shooting]]
### Error: Received status code 403. Resource not accessible by integration [https://docs.github.com/rest/checks/runs#create-a-check-run](https://docs.github.com/rest/checks/runs#create-a-check-run)
1. workflow에 `permissions`를 설정한다
```yaml
...
permissions:
  checks: write
  contents: write
...
```
2. Repository의 설정 변경을 통해 해결한다
![[Pasted image 20231105215828.png]]![[Pasted image 20231105215833.png]]