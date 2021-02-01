```java  
class Solution {
    boolean isMatch = false;
    public boolean isMatch(String s, String p) {
        if (p.length() == 0) {
            return s.length() == 0;
        }
        if (p.length() > 1 && p.charAt(1) == '*') {  // second char is '*'
            if (isMatch(s, p.substring(2))) {
                return true;
            }
            if(s.length() > 0 && (p.charAt(0) == '.' || s.charAt(0) == p.charAt(0))) {
                return isMatch(s.substring(1), p);
            }
            return false;
        } else {                                     // second char is not '*'
            if(s.length() > 0 && (p.charAt(0) == '.' || s.charAt(0) == p.charAt(0))) {
                return isMatch(s.substring(1), p.substring(1));
            }
            return false;
        }
    }
}
```

#### 확인
1. 어마어마한 시간을 두고 고민함..
2. 문자 조합 등이 brute force 형태의 재귀일 수도 있지만, build-up 형식의 재귀일 수도 있다는걸 염두해두고 접근해보자
3. 
String a = "A";
a.substring(1); // OK

String B = "";
B.charAt(0); // NOK 

