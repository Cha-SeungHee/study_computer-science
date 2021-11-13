``` c
#include <stdio.h> 
#include <string.h>

void QuestionsMarks(char str[]){    
    int isthere = 0;
    int suc = 1;
    
    for(int i=0; i<strlen(str); i++){        
        for(int j=i; j<strlen(str); j++){            
            if((str[i] - '0') + (str[j] - '0') == 10){                
                if(i == j){                    
                    continue;                    
                }
                
                isthere = 1;
                int counter = 0;
                for(int h = i+1; h<j; h++){                    
                    if(str[h] == '?'){                        
                        counter++;                        
                    }                    
                }
                if(counter != 3){                    
                    suc = 0;                    
                }
                
                i++;                
            }            
        }        
    }
    
    if(suc == 1 && isthere == 1){        
        printf("true\n");        
    }else{        
        printf("false\n");        
    }    
}

int main(void) { 
  
  // keep this function call here
  QuestionsMarks(gets(stdin));
  return 0;
    
}
```
