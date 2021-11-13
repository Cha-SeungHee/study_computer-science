``` c
#include <stdio.h> 
#include <string.h>
#include <stdbool.h>

void BracketMatcher(char * str) {
  int top = 0;
  int len = strlen(str);
  char stack[len];
  bool isCorrect = true;

  for (int i = 0; i < len; i++) {
    if (str[i] == '(') {
      stack[top] = str[i];
      top += 1;
    } else if (str[i] == ')') {
      if (top - 1 < 0) {
        isCorrect = false;
        break;
      }
      top -= 1;
    } else {
      continue;
    }
  }  
  if (top != 0) isCorrect = false;
  printf(isCorrect ? "1" : "0");
}

int main(void) { 
   
  // keep this function call here
  BracketMatcher(coderbyteInternalStdinFunction(stdin));
  return 0;
    
}
```
