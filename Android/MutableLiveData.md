#### LiveData와의 차이
LiveData 대비 postValue 및 setValue와 같은 값을 수정할 수 있는 public 메소드들이 추가

```java  
public class MutableLiveData<T> extends LiveData<T> {

    /**
     * Creates a MutableLiveData initialized with the given {@code value}.
     *
     * @param value initial value
     */
    public MutableLiveData(T value) {
        super(value);
    }

    /**
     * Creates a MutableLiveData with no value assigned to it.
     */
    public MutableLiveData() {
        super();
    }

    @Override
    public void postValue(T value) {
        super.postValue(value);
    }

    @Override
    public void setValue(T value) {
        super.setValue(value);
    }
}
```

#### get 및 set
get과 set이 주는 data는 MutableLiveData<T>의 T형 데이터이지, MutableLiveData가 아니다

예시
```java
@Nullable
    public T getValue() {
        Object data = mData;
        if (data != NOT_SET) {
            return (T) data;
        }
        return null;
    }
```

#### setValue vs postValue
- setValue : main thread에서 사용. 즉시 값 변경. notification 또한 즉시 발생  
"If you are working on the main thread, then both setValue and postValue will work in the same manner 
i.e. they will update the value and notify the observers."

- postValue : worker thread에서 사용. 즉시 값 변경 이후 main thread에 task 전달. Main thread 실행 시점에 따라 notification 시점 달라짐. 
따라서 여러번 값을 바뀌더라도 마지막 notification만 수행될 수 있음  
"If working in some background thread, then you can't use setValue. You have to use postValue here with some observer. 
But the interesting thing about postValue is that the value will be change immediately 
but the notification that is to be sent to observers will be scheduled to execute on the main thread via the event loop with the handler."

참고 : https://blog.mindorks.com/livedata-setvalue-vs-postvalue-in-android

#### 객체 생성 관련
LiveData 내부에는 Object 데이터 타입이 존재하며, 그렇기에 LiveData / MutableLiveData 객체를 생성하면 Generic type의 객체를 별도로 생성할 필요가 없음
