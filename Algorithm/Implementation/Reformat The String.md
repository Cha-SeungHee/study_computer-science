``` c
char * reformat(char * s){
    int i =0;
    int alphacount= 0;
    int digitcount = 0;
    while(s[i]!='\0'){
        if(s[i]-'a'>=0){           
            alphacount++;
        }
        else{
            digitcount++;
        }
        i++;
    }    

    if(alphacount-digitcount > 1 || alphacount-digitcount < -1){
        return "";
    }
    
    char* result = malloc(sizeof(char)*(alphacount+digitcount+1));
    int alphaindex = alphacount>=digitcount?0:1;
    int digitindex = digitcount>alphacount?0:1;
    i = 0;
    while(s[i]!='\0'){
        if(s[i]-'a'>=0){           
            result[alphaindex] = s[i];
            alphaindex+=2;
        }
        else{
            result[digitindex] = s[i];
            digitindex+=2;
        }
        i++;
    }
    
    result[alphacount+digitcount] = '\0';
    return result;
}
```
