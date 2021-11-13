``` c
#include <stdio.h> 
#include <string.h>
#include <stdlib.h>

void FirstReverse(char * str) {
  
  // code goes here  
  int len = strlen(str);
  int begin = 0, end = len - 1;

  char * newStr = (char *) malloc(sizeof(char) * len);
  strcpy(newStr, str);
  
  while (begin <= end) {
    char temp = newStr[begin];
    newStr[begin] = newStr[end];
    newStr[end] = temp;
    begin += 1;
    end -= 1;
  }
  
  printf("%s", newStr);
}

int main(void) { 
   
  // keep this function call here
  FirstReverse(coderbyteInternalStdinFunction(stdin));
  return 0;
    
}
```

``` c
#include <stdio.h> 
#include<string.h>
void FirstReverse(char str[]) { 
  
  // code goes here 
  int l=0,i;
  l=strlen(str)-1;
  for(i=l;i>=0;i--)
      putchar(str[i]);
}

int main(void) { 
  
  // keep this function call here
  FirstReverse(gets(stdin));
  return 0;
    
}
```
