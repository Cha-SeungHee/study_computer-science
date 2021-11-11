``` c
char * largestOddNumber(char * num){
    int len = strlen(num);
    int last = -1;
    
    for (int i = len - 1; i >= 0; i--) {
        if (num[i] % 2 == 0) {
            continue;
        } else {
            last = i;
            break;
        }
    }
    
    char* result = malloc(sizeof(char) * (last + 2));
    if (last == -1) {
        result = "";
    } else {
        strncpy(result, num, last + 1);    
        result[last + 1] = '\0';
    }
    
    printf("%s", result);
    
    return result;
}
```
