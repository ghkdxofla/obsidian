# Abstract
- [[Strapi]]에서 Fuzzy Search가 가능하도록 해주는 Plugin
# Content
## Configuration
```typescript
// config/plugins.ts
export default ({ env }) => ({
	...
	"fuzzy-search": {
	    enabled: true,
	    config: {
	      contentTypes: [
	        {
	          uid: "api::column.column",
	          modelName: "columns",
	          transliterate: true,
	          fuzzysortOptions: {
	            characterLimit: 300,
	            threshold: -600,
	            limit: 10,
	            keys: [
	              {
	                name: "title",
	                weight: 100,
	              },
	              {
	                name: "details",
	                weight: -100,
	              },
	            ],
	          },
	        }
	      ],
	    },
	  },
	  ...
});
```
## Usage
- 위 `columns` model에서 검색 시, 다음과 같이 진행
- `populate` 하려면 `populate[MODEL_NAME]` 형식으로 사용해야 한다
- 
```json
// /api/fuzzy-search/search?query=am&populate[columns]=*

```

# Reference
- [Fuzzy Search](https://market.strapi.io/plugins/strapi-plugin-fuzzy-search)