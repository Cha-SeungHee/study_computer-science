#### newInstance()로 생성하는 이유

Fragment 생성시 부가적인 정보를 전달해야할 때는 생성자가 아닌 newInstance() 메소드 내에서 아래와 같이 Bundle을 통해서 전달하도록 한다. 
```java 
public static MonthFragment newInstance(int pagePosition) {
  MonthFragment fragment = new MonthFragment();
  Bundle args = new Bundle();
  args.putInt(PAGE_POSITION, pagePosition);
  fragment.setArguments(args);
  return fragment;
}
```  
이유는 안드로이드에서 메모리가 부족하면 액티비티를 파기하여 메모리를 확보하고 필요시 재생성한다.  
재생성시 활용하는 것이 매개변수가 없는 생성자 
(매개변수가 있는 생성자의 경우 어떠한 값을 넣어주어야할지 자동으로 선택하기가 어려울 것으로 추정) 
참고로, bundle을 통해 설정한 변수들은 복구되어 다시 설정되기에 문제가 없다.
