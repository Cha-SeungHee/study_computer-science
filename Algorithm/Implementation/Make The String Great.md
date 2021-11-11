``` c
#include <stdlib.h>
#include <stdbool.h>

#define OFFSET ('a' - 'A')

char * makeGood(char * s){    
    bool bad = true;
    
    while (bad) {
        bad = false;
        int len = strlen(s);
        char* temp = malloc(sizeof(char) * (len + 1));
        int indexTemp = 0, index = 0;

        while (index < len) {
            if (s[index] - s[index + 1] == OFFSET || s[index + 1] - s[index] == OFFSET)  {                   bad = true;
                index += 2;
                continue;
            }

            temp[indexTemp] = s[index];
            index += 1;
            indexTemp += 1;
        }    

        temp[indexTemp] = '\0';
        strcpy(s, temp);
    }
    
    return s;
}
```
