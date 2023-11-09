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