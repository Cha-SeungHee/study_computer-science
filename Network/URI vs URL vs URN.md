#### URI (Uniform Resource Identifier) - 통합 지원 식별자  
- 서버 리소스 이름은 URI라고 지칭  
- 인터넷의 우편물 주소 같은 것  
- 정보 리소스의 고유 식별 및 위치 지정 가능  
- URI의 두 가지 형태: URL, URN  

#### URL - (Uniform Resource Locator) - 통합 자원 지시자
- URI의 가장 흔한 형태  
- 특정 서버의 한 리소스에 대한 구체적인 위치 명시    
- 리소스의 위치 및 접근 방법에 대해 명시  
- URL은 주소이지 실제 이름이 아니기에 리소스의 위치가 변경되면 기존 URL로 검색 시에 해당 리소스를 찾을 수 없음 (URN의 등장 이유)  

예시
http://naver.com - 네이버 사이트의 URL
http://img.naver.net/static/www/dl_qr_naver.png - 네이버 앱 QR 코드의 이미지에 대한 URL

#### URN (Uniform Resource Name, URN) 
- URI의 두 번째 형태는 유니폼 리소스 이름  
- 이 위치 독립적인 URN은 리소스를 여기저기로 옮기더라도 문제없이 동작  

예시
urn:ietf:rfc:2141 - 'RFC 2141' 문서


#### 결론
- URL과 URN은 URI의 종류  
- URI는 규약, URL과 URN은 이의 구현방식

출처: https://mygumi.tistory.com/139 [마이구미의 HelloWorld]
