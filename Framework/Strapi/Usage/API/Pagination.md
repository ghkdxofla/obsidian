# Abstract
- Pagination을 적용하는 방법을 설명한다
# Content
## 기본 사용법
```markdown
/api/columns/?pagination[page]=1&pagination[pageSize]=10
```
## [[strapi-plugin-fuzzy-search]]에서 사용법
- `pagination[MODEL_NAME]` 으로 사용
```markdown
/api/fuzzy-search/search?query=amittopagination[columns][page]=1&pagination[columns][pageSize]=10
```
# Reference
- [Pagination](https://docs.strapi.io/dev-docs/api/rest/sort-pagination#pagination-by-page)