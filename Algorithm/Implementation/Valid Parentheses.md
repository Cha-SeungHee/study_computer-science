``` c
bool isValid(char * s){
    int len = strlen(s);
    
    char stack[len];
    int top = 0;
    
    for (int i = 0; i < len; i++) {
        char ch = s[i];
        switch(ch) {
            case '(': 
            case '{': 
            case '[':
                stack[top] = ch;
                top += 1;
                break;
                
            case ')':
                if (top - 1 < 0) return false;
                if (stack[top - 1] != '(') return false;
                top -= 1;
                break;
                
            case '}':
                if (top - 1 < 0) return false;
                if (stack[top - 1] != '{') return false;
                top -= 1;
                break;
                
            case ']':
                if (top - 1 < 0) return false;
                if (stack[top - 1] != '[') return false;
                top -= 1;
                break;
            
            default:
                break;
        }
    }
    
    if (top != 0) return false;
    return true;
}
```
