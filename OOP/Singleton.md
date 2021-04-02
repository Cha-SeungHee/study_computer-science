#### Singleton Pattern
- 시스템 내부에 하나의 인스턴스만 생성하고 싶은 경우  (예: 모듈과 관계 없이 시스템 전제에 공통적으로 적용되어야 하는 설정)
- 생성자를 private으로 선언하고 클래스 내부에서 해당 생성자 호출

#### LazyHolder 기법 (Thread-safe)
- 처음부터 instance 생성 x  
- Class 로딩 및 초기화 시점은 thread-safe  

``` java
class Singleton {
    private Singleton() {}

    public static Singleton getInstance() {
        return LazyHolder.INSTANCE;
    }

    private static class LazyHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
}
```

### 최종적으로 LazyHolder 방법이 도출된 과정을 알아보자

#### 일반적인 형태 
``` java
class Singleton {
  private static Singleton instance = null;
  
  public static Singleton getInstance() {
    if (instance == null) {
      instance = new Singleton();
    }
    
    return instance;
  }

  private Singleton() {}
}
```

- Thread-safe x  
- 한 스레드에서 getInstance 메소드를 호출하는 중에 다른 스레드에서 getInstance 메소드를 호출하면 두 개 이상의 instance 생성이 가능  

#### 개선 방법
1) 처음부터 인스턴스 생성 
- 인스턴스를 처음부터 생성하게 되면 불필요한 리소스 낭비 가능  
``` java
public class Singleton {
	private static Singleton instance = new Singleton();

	public static Singleton getInstance() {
		return instance;
	}

	private Singleton() {}
}
```

2) getInstance() 동기화 (Synchronized): 성능의 저하
``` java
class Singleton {
    private static Singleton instance = null;

    public synchronized static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }

        return instance;
    }

    private Singleton() {}
}
```


#### Singleton Pattern (Python)
``` py
class Singleton(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, "_instance"):         # Foo 클래스 객체에 _instance 속성이 없다면
            print("__new__ is called\n")
            cls._instance = super().__new__(cls)  # Foo 클래스의 객체를 생성하고 Foo._instance로 바인딩
        return cls._instance                      # Foo._instance를 리턴

    def __init__(self, data):
        cls = type(self)
        if not hasattr(cls, "_init"):             # Foo 클래스 객체에 _init 속성이 없다면
            print("__init__ is called\n")
            self.data = data
            cls._init = True
```
