#### 배열 index 사용시
- 배열 index 사용할 때 항상 그 값이 배열의 크기보다 작은지 체크하는 습관을 기르자  

#### BFS
- Queue에 offer 할 때 visited 반드시 처리  
- Poll 시점에 처리할 경우, offer와 Poll 사이에 해당 Node에 접근하는 상황이 발생하면 중복 offer 가능  

#### Sort
- String은 Arrays.sort로 바로 sort 할 수 없기에 char[] array로 변경한 뒤에 정렬해야 한다  
   (또는 List에 담은 뒤에 Collections.sort로)  
   
#### String 
- StringBuilder는 숫자를 바로 append 할 수 있기에 Integer.toString(int 변수) 할 필요가 없다  
- 특정 글자가 숫자 또는 문자인지 확인하기 위한 API -> Character.isLetter(char ch)

- replaceAll(정규식, 대체 String)
- trim(): 양쪽 공백 삭제
- split(" . ");
- replace vs replaceAll: replace는 첫번째 인자로 character sequence, replaceAll은 정규식.   
  replaceAll이 불특정하게 섞여있는 문자를 변경할 때 유리. 새로운 String return  

#### String 생성시 
1) 
String A = "ABC";
String B = "ABC"; 

- A와 B는 동일한 객체를 가리킴  

2) 
String B = new String(A); // String B는 A의 내용을 가지는 새로운 객체 생성. 별도의 객체  

#### StringBuilder
- sb.deleteCharAt(int index)  

#### 문자열 뒤집기 (StringBuilder)
- 문자열을 뒤집고 싶은 경우 StringBuilder의 insert(0, 문자) 메소드를 사용할 수 있으나, 이 경우 StringBuilder의 본 목적을 해친다  
- 원래 순서대로 문자열을 집어 넣은 이후에 reverse() 메소드를 사용하자

#### 상태를 저장하는 경우(ex. HashMap, PriorityQueue)
- 개수 또는 index의 위치와 같은 정보를 저장하는 경우, 항상 해당 정보가 변할 수 있고 그럴 경우에는 업데이트를 해줘야 함을 잊지 말자  
 
ex. backtracking  

#### 행렬
- r행 c열 -> A[r][c]  

#### ArrayList
- To replace at specific index -> set(int index, E element) 활용  
- Remove(int index) 가능  

#### HashMap
- map.remove(val) 가능  

#### List의 toArray() 메소드
- String[] stringArray = stringList.toArray(new String[0]);
- 인자로 들어가는 String 배열의 크기보다 실제 리스트 크기가 크면 리스트의 크기대로, 아니면 인자로 전달되는 크기로 생성된다  
