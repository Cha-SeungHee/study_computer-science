Adapter 패턴은 서로 다른 인터페이스를 제공하는 두 모듈을 결합할 때 유용하다  

#### 문제 상황
class SearchService
- 제공 인터페이스: search()

class TolrQuery
- 제공 인터페이스: query()

#### Adapter 패턴 적용
``` java
interface SearchService {
    void serach();
}

class SearchSedrviceTolrAdapter implements SearchService {
    private TolrClient tolrClient = new TolrClient();

    @Override
    public void serach(String keyword) {
        TolrQuery tolrQuery = new TolrQuery(keyword);
        
        QueryResponse response = tolrClient.query(tolrQuery);
        
        SearchResult result = convertoResult(response);
        
        return result;
    }
    
    private SearchResult convertToResult(QueryResponse response) {
        
    }
}
```

- TolrQuery에서 제공하는 인터페이스를 SearchService에서 제공하는 인터페이스에 맞게 새로운 클래스 정의    
