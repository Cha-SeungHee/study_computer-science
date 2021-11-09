``` c
#include <string.h>

char * restoreString(char * s, int* indices, int indicesSize){
    int len = strlen(s);
    char * restore = (char *) malloc(sizeof(char) * len + 1);
    
    strcpy(restore, s);
    for (int i = 0; i < indicesSize; i++) {
        restore[indices[i]] = s[i];
    }
    
    return restore;
}
```
