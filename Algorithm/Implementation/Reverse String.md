``` c
void reverseString(char* s, int sSize){
    int begin = 0, end = sSize - 1;
    
    while (begin < end) {
        char temp = s[begin];
        s[begin] = s[end];
        s[end] = temp;
        begin += 1;
        end -= 1;
    }
}
```
