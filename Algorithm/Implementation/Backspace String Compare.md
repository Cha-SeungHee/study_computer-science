``` c
#include <string.h>

char * backspace(char * s);

bool backspaceCompare(char * s, char * t){
    char * a = backspace(s);
    char * b = backspace(t);
    
    return strcmp(a, b) == 0;
}

char * backspace(char * s) {
    int index = 0;
    int sLen = strlen(s);
    char * newS = (char *) malloc(sizeof(char) * (sLen + 1));
    
    for (int i = 0; i < sLen; i++) {        
        if (s[i] == '#') {
            if (i == 0) {
                index = 0;
                continue;
            } else {
                if (index > 0) index -= 1;
            }
        } else {
            newS[index] = s[i];
            index += 1;
        } 
    }
    
    newS[index] = '\0';
    
    return newS;
}
```
