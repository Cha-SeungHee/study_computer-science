``` c
#include <string.h>

bool rotateString(char * s, char * goal){
    int len = strlen(s);
    char * rotate = (char *) malloc(sizeof(char) * (len + 1));
    
    for (int i = 1; i <= len; i++) {    
        strncpy(rotate, s + len - i, i);
        strncpy(rotate + i, s, len - i);
        rotate[len] = '\0';
        
        if (strcmp(rotate, goal) == 0) {
            return true;
        }
    }
    
    return false;
}
```
