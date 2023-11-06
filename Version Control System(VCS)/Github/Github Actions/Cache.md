# Abstract
- GitHub Actions에서 제공하는 **의존성 캐싱**을 적용하면 워크플로우의 실행 시간을 단축 가능
- key 값을 기반으로 캐시를 가져온다
	- key에 해당하는 캐시가 있으면, path에 지정된 경로에 데이터를 복원
	- key에 해당하는 캐시가 없으면, 해당 작업이 성공적으로 끝날 경우에 **path 경로에 있는 파일들로** 자동으로 새로운 캐시를 생성
- GitHub은 7일 이상 액세스하지 않은 캐시를 제거
- 저장소에 있는 모든 캐시의 총량은 10GB로 제한
# Setup
- Node의 경우, NPM 기준으로 다음과 같이 설정한다
```yaml
- name: Get npm cache directory
  id: npm-cache-dir
  run: echo "dir=$(npm config get cache)" >> ${GITHUB_OUTPUT}
- uses: actions/cache@v3
  id: npm-cache # use this to check for `cache-hit` ==> if: steps.npm-cache.outputs.cache-hit != 'true'
  with:
    path: ${{ steps.npm-cache-dir.outputs.dir }}
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-
```
# Reference
[actions/cache](https://github.com/actions/cache)
[caching-dependencies-to-speed-up-workflows](https://thearchivelog.dev/article/caching-dependencies-to-speed-up-workflows/)
[의존성 캐싱을 통한 workflows 속도 올리기(official)](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows)