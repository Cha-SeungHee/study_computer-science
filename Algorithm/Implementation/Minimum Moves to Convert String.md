``` c
int minimumMoves(char * s){
    int len = strlen(s);
    int count = 0;
    
    for (int i = 0; i < len; i++) {
        if (s[i] == 'X') {
            s[i] = 'O';
            if (i + 1 < len) s[i + 1] = 'O';
            if (i + 2 < len) s[i + 2] = 'O';
            count += 1;
        }
    }
    
    return count;
}
```
