#### Context는 어플리케이션에 대한 여러 기본 정보
영어권에서 context는 속성(용량, 이름, 생성 날짜 등)을 뜻한다  
또한 운영체제에서의 context(현 프로세스의 수행 상태를 나타낼 수 있는 레지스터 등 여러 값)를 생각해보면 context가 어떤 의미로 사용되었을 지 유추해볼 수 있다  

#### 대표적인 Context
- Activity Context, Application Context  
- Service, Broadcast Receiver, Content Provider 등도 Context를 가지며 이는 Activity Context,  Application Context와 조금 차이가 있다   

#### Activity Context와 Application Context
- Activity Context와 Application Context 모두 Context 클래스 상속  
- 상속 이후 구현한 내용과 생명 주기가 조금 다름  
- Application Context는 Activity Context 대비 좀 더 포괄적 (Activity Context가 내부의 상세한 사항)  

#### Activity Context
- Activity Context는 주로 Activity 내에서 사용  
- Activity의 생명주기를 따른다 (onCreate시 생성, onDestroy시 제거)  
- Activity 안에서 사용되는 View (TextView, ImageView)들의 Context는 기본적으로 묶여있는 Activity의 Context를 참조  

- Intent로 새로운 Activity로 넘어갈 때 Context를 넘겨주는 이유: 바로 전에 호출한 Activity에 대한 정보가 필요하기 때문  
- 스택에 Activity 관련 정보들이 쌓이고 새로운 Activity가 사라질 때 이전 Activity로 돌아갈 수 있음 (스택)  
- 하지만 Application Context과 Activity Context는 공통적으로 갖고 있는 내용이 있으며 Intent의 인자로 Application Context를 넘겨줘도 무방  

#### Application Context
- getPackageName(), getResource() 등 앱에 대한 정보가 필요한 경우에는 Activity Context가 아닌 Application Context를 통한다  
- 추가적으로 안드로이드는 프로세스와 어플리케이션을 분리해서 관리하는데 ActivityManagerService가 관리하는 어플리케이션에 대해 필요한 정보가 Application Context  

#### *안드로이드는 프로세스와 어플리케이션을 따로 관리
- 일반적으로 프로그램을 실행하면 이에 맞는 프로세스가 돌아가고 OS에서 프로세스 정보를 관리  
- 하지만 안드로이드는 이와 달리 프로세스와 어플리케이션을 따로 관리  
- 예를 들어, 취소 버튼 두 번 눌러서 앱을 종료시키더라도 홈키 왼쪽 버튼을 눌러서 보면 앱이 아직 돌고 있음  
- 프로세스는 종료되었지만 어플리케이션은 남아있기 때문  

이러한 방식이 필요한 두가지 상황 예시
- 중요한 파일을 다운받고 있는 도중 사용자가 강제 종료하면 문제가 발생. 앱이 종료되더라도 백그라운드에서 필요한 데이터를 마저 다운  
- 메모리가 부족하여 앱을 강제시켰을 때 사용자가 해당 앱을 다시 사용하려고 하면 강제종료 전의 여러 정보가 필요  

#### 메모리 누수
- Singleton 패턴의 클래스에서 생명주기가 있는 Activity 또는 Service의 Context를 참조하는 경우 메모리 누수가 발생할 수 있다  
- Singleton 패턴의 클래스는 static으로 선언되고 이로 인해 참조되는 context까지 메모리 해제 되지 않을 수 있다  
- 이러한 경우에는 ApplicationContext가 참조되도록 해야 한다  

- 스레드 또는 Handler 등 백그라운드 작업시에도 ApplicationContext를 참조하도록 사용해야 한다  

#### 관련 함수
1) getBaseContext()
- Activity의 Context  
- 생성자나 Context에서 기본 설정 된 Context  

2) getApplicationContext()
- Service의 Context  
- 어플리케이션의 종료 이후에도 활동 가능한 글로벌한 Application의 Context   
- 앱 종료 후 메모리 유지를 피하기 위해서 getBaseContext를 사용  
