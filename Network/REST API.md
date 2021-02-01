#### REST API (Representational State Transfer)
- HTTP를 좀 더 효율적으로 사용하기 위한 아키텍처   

#### 구성
- 자원(Resource) : URI
- 행위(Verb) : HTTP Method
- 표현(Representations)

#### REST 특징
- Uniform Interface: URI로 지정한 리소스에 대한 조작 인터페이스를 통일  
- Stateless: 작업을 위한 상태정보를 따로 저장하고 관리 x  
- Cacheable: 캐시 가능 (Last-modified 태그 또는 E-Tag 이용)  
- Self-descriptiveness: 메시지만 보고도 동작을 쉽게 이해 할 수 있는 구조  
- Client-Server: Server와 Client의 역할을 확실히 구분. 서로간 의존성 감소  
- Hierarchy: REST API Server는 다중 계층으로 구현  

#### HTTP Method
- POST: 리소스 생성  
- GET: 리소스 조회 및 획득  
- PUT: 리소스 수정  
- DELETE: 리소스 삭제  

#### REST API 가이드
1. URI는 리소스의 정보를 표현  
- https://sample.com/cafe/menu/americano  

2. 리소스에 대한 행위는 HTTP Method(POST, GET, PUT, DELETE)로 표현합니다.
- GET /members/insert/1 (X)
- POST /members/1 (O)



참고
https://jungwoon.github.io/android/2019/07/11/Retrofit/
