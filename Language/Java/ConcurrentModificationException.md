이 예외는 흔히 List나 ArrayList를 for 문에 직접 집어넣고 돌리며 remove를 호출했을 때 발생  
List를 순회하는 도중 remove를 호출하면 기존 index 값과 remove 호출로 인해 줄어든 size 값이 맞지 않기 때문에 예외가 발생  

``` java
ArrayList<String> list = new ArrayList<String>();

for(String name : list){
    list.remove(name);
}
```

#### 해결법1 (비효율적)
``` java
ArrayList<String> list = new ArrayList<String>();
            
ArrayList<String> Remove = new ArrayList<String>();
for (String name : list) 
    Remove.add(name);
for (String name : Remove) 
    list.remove(name);
```

#### 해결법2
``` java
ArrayList<String> list = new ArrayList<String>();
 
Iterator<String> iter = list.iterator();
while (iter.hasNext()) {
    String s = iter.next();
    iter.remove();
}
```
