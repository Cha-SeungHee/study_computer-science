#### 문제 상황
- 이미지 또는 동영상 등을 로딩 시에 모든 이미지를 다 로딩하도록 구현하면 불필요하게 메모리를 사용하는 문제가 발생   
- 실제 이미지가 필요할 때 이미지를 로딩하도록 코드를 구현할 때 유용한게 Proxy 패턴  

``` java
interface Image {
    void draw();
}

class ProxyImage implements Image {
    private String path;
    private RealImage image;

    public ProxyImage(String path) {
        this.path = path;
    }

    @Override
    public void draw() {
        if (image == null) {
            image = new RealImage(path);
        }
        image.draw();
    }
}

class RealImage implements Image {

    @Override
    public void draw() {

    }
}
```

- 실제 이미지 로딩은 RealImage 객체에게 위임  
- ProxyImage 클래스는 draw() 메소드가 호출되기 전까지 RealImage 객체 생성 x  
- 메모리에 이미지 데이터 로딩 x  


