# Abstract
- 라이브러리 자체에 버그가 있어서 신속한 수정이 필요 하다거나 라이브러리에서 지원하지 않는 기능을 추가하고 싶을 때 사용하면 안전하게 수정사항을 공유할 수 있다
- node_modules에 수정한 사항이 git으로 관리되고 어떠한 실행 환경에서도 적용되도록 한다
# Setup
### Installation
```
# npm
npm install patch-package

# yarn
yarn add patch-package
```
### Usage
1. `package.json > scripts 에 "postinstall": "patch-package"` 추가
	```
	{
		...
		"scripts": {
			...
			"postinstall": "patch-package"
			...
		},
	...
	
	}
	```
2. 수정할 `node_modules` 의 package 수정
	- 이 때, npm package 설치 중에 Typescript compile error 등이 발생하는 경우, 설치 전에 해당 파일을 바꿔주는 방법으로 우회한다.
		- 더 좋은 방법이 있으면 적어둘 예정
3. `.patch` 파일 생성
	```sh
	npx patch-package {package_name}
	```
4. 정상적으로 생성되었는지 확인
- `patches` 폴더가 생성되고, 하위에 다음과 같이 파일이 생성되었는지 체크
	![[Pasted image 20231029184731.png]]
# Check
- `node_modules`를 삭제 후 npm 재설치를 했을 때, 해당 patch가 적용되었는지 확인
```
rm -rf node_modules
npm install
```