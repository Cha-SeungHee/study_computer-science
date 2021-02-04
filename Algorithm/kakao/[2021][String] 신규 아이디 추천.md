``` java
import java.util.*;

class Solution {
    public String solution(String new_id) {
        String string = new_id.toLowerCase();
        string = string.replaceAll("[^-_.a-z0-9]", "");
        string = string.replaceAll("[.]{2,}", ".");
        string = string.replaceAll("^[.]|[.]$", "");
        string = (string.length() == 0) ? "a" : string;
        string = (string.length() >= 16) ? string.substring(0, 15) : string;
        string = string.replaceAll("[.]$", "");
        
        while (string.length() <= 2) {
            string += string.charAt(string.length() - 1);
        }
        
        return string;
    }
}
```

- .을 \.이 아니라 [.]로 표현
- [.]{2,}
- [^-_.a-z0-9]
- ^[.]|[.]$
