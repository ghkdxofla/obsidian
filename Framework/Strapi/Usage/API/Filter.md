# Abstract
- API에서 Filtering을 어떻게 하는지 설명한다
# Content
## 기본 사용법
- 여러 filter를 사용하려면 `&`로 여러 개를 이어 사용한다
- model의 관계 및 hierarchy에 따라 검색하려면 `[]` 로 사용한다
- Operator는 다음이 존재한다

	  |Operator|Description|
	  |---|---|
	  |`$eq`|Equal|
	  |`$eqi`|Equal (case-insensitive)|
	  |`$ne`|Not equal|
	  |`$nei`|Not equal (case-insensitive)|
	  |`$lt`|Less than|
	  |`$lte`|Less than or equal to|
	  |`$gt`|Greater than|
	  |`$gte`|Greater than or equal to|
	  |`$in`|Included in an array|
	  |`$notIn`|Not included in an array|
	  |`$contains`|Contains|
	  |`$notContains`|Does not contain|
	  |`$containsi`|Contains (case-insensitive)|
	  |`$notContainsi`|Does not contain (case-insensitive)|
	  |`$null`|Is null|
	  |`$notNull`|Is not null|
	  |`$between`|Is between|
	  |`$startsWith`|Starts with|
	  |`$startsWithi`|Starts with (case-insensitive)|
	  |`$endsWith`|Ends with|
	  |`$endsWithi`|Ends with (case-insensitive)|
	  |`$or`|Joins the filters in an "or" expression|
	  |`$and`|Joins the filters in an "and" expression|
	  |`$not`|Joins the filters in an "not" expression|
```json
// api/portfolios?filters[marketings][name][$eq]=브랜드 마케팅&filters[marketings][name][$eq]=바이럴 마케팅&filters[status][$eq]=main
```
# Reference
- [Filtering - 1](https://docs.strapi.io/dev-docs/api/rest/filters-locale-publication#filtering)
- [Filtering - 2](https://docs.strapi.io/dev-docs/api/query-engine/filtering)