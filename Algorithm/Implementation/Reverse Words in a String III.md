``` c
char * reverseWords(char * s){
    int len = strlen(s);
    int walker = 0, runner = 0;
    
    while (runner <= len) {
        if (s[runner] == ' ' || s[runner] == '\0') {
            int begin = walker;
            int end = runner - 1;
            
            while (begin < end) {
                char temp = s[begin];
                s[begin] = s[end];
                s[end] = temp;
                
                begin += 1;
                end -= 1;
            }
            
            runner += 1;
            walker = runner;
        } else {
            runner += 1;
        }
    }
    
    return s;
}
```
