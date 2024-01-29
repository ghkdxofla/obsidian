# Abstract

# Content
## Tokenizer
- 토크나이저는 문서를 작은 단위로 분할하여 검색어 토큰을 생성하는 데 사용
- 토큰은 색인에 추가되는 단어
- 내장 토크나이저로 standard
	- standard는 공백으로 구분된 단어를 생성
- 사용자정의 토크나이저를 구성 가능
## Analyzer
- Analyzer에서 [[Tokenizer & Analyzer#Tokenizer]]를 사용하기 때문에 Analyzer가 조금 더 큰 개념
- Elasticsearch는 기본적으로 띄어쓰기로 단어를 구분하는 기본 분석기 `Standard Analyzer`를 제공
- `Standard Analyzer`는 검색 키워드로 `"나무가"` 를 입력하면 `"뿌리가 깊은 나무는"` 에서 분할된 목록(토큰 목록) 중에서 `"나무가"` 를 찾아 매치되면 검색
- 다양한 분석기를 제공하고 커스텀 분석기를 만들 수도 있음
	- `"뿌리가 깊은 나무는"` 을 한글 형태소로 분할 하면 `"뿌리"`, `"가"`, `"깊은"`, `"나무"`, `"는"` 으로 분할 되기 때문에 `"나무"` 라고 검색해도 검색
## Analyzer vs Tokenizer?
- 둘 다 elasticsearch에서 기본 제공하는 설정으로 색인에 대한 분석 구성을 정의
- `tokenizer`는 색인에 대한 토크나이저를 구성
- `analyzer`는 분할된 토큰에 필터링과 정규화 처리 통헤 색인에 추가할 단어의 집합을 만드는 데 사용
# Reference
- [elasticsearch에서 nori, ngram tokenizer를 동시에 활용하기](https://lamttic.github.io/2020/03/10/01.html)
- [Elasticsearch를 검색 엔진으로 사용하기(1): Nori 한글 형태소 분석기로 검색 고도화 하기](https://hanamon.kr/elasticsearch-%EA%B2%80%EC%83%89%EC%97%94%EC%A7%84-nori-%ED%98%95%ED%83%9C%EC%86%8C-%EB%B6%84%EC%84%9D%EA%B8%B0-%EA%B2%80%EC%83%89-%EA%B3%A0%EB%8F%84%ED%99%94-%EB%B0%A9%EB%B2%95/)