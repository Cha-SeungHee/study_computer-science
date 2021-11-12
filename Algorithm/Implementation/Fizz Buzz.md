``` c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
char ** fizzBuzz(int n, int* returnSize){
    *returnSize = n;
    char buf[9];
    char** result = malloc(n * sizeof(char *));    
    
    for (int i = 0; i < n; i++) {
        if ((i + 1) % 3 == 0 && (i + 1) % 5 == 0) {
            sprintf(buf, "%s", "FizzBuzz");            
        } else if ((i + 1) % 3 == 0) {
            sprintf(buf, "%s", "Fizz");
        } else if ((i + 1) % 5 == 0) {
            sprintf(buf, "%s", "Buzz");
        } else { 
            sprintf(buf, "%d", i + 1);
        }
        
        result[i] = malloc(sizeof(buf));
        strcpy(result[i], buf);
        memset(buf, "", 9);
    }    
    
    return result;
}
```

- sprintf
- memset
- strcpy
- memcpy
