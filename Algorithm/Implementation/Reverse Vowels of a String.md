``` c
bool isVowel(char ch);

char * reverseVowels(char * s){
    int index = 0;
    int len = strlen(s);
    char vowel[len];
    
    for (int i = 0; i < len; i++) {
        if (isVowel(s[i])) {
            vowel[index] = s[i];
            index += 1;
        }        
    }
    
    index = 0;
    for (int i = len - 1; i>= 0; i--) {
        if (isVowel(s[i])) {
            s[i] = vowel[index];
            index += 1;
        }
    }
    
    return s;
}

bool isVowel(char ch) {
    return ch == 'a' ||
           ch == 'e' || 
           ch == 'i' || 
           ch == 'o' || 
           ch == 'u' ||
           ch == 'A' || 
           ch == 'E' || 
           ch == 'I' || 
           ch == 'O' || 
           ch == 'U';
}
```
