``` c
int balancedStringSplit(char * s){
    int i = 0;
    int count = 0, balance = 0;
    
    while (s[i] != '\0') {
        if (s[i] == 'R') {
            balance += 1;
        } else {
            balance -= 1;
        }
        
        if (balance == 0) count += 1;
        
        i += 1;
    }
    
    return count;
}
```
