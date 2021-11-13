``` c
#include <stdio.h> 
#include <string.h>
#include <stdbool.h>

bool isValidCharacter(char ch) {
  return ('a' <= ch && ch <= 'z') ||
         ('A' <= ch && ch <= 'Z') ||
         ('0' <= ch && ch <= '9') ||
         (ch == '_');
}

void CodelandUsernameValidation(char * str) {
  int len = strlen(str);

  if (len < 4 || len > 26) {
    printf("false");
    return;
  }

  if (isalpha(str[0]) < 1) {
    printf("false");
    return;
  }

  for (int i = 0; i < len; i++) {
    if (!isValidCharacter(str[i])) {
      printf("false");
      return;
    }
  }

  if (str[len - 1] == '_') {
    printf("false");
    return;
  }

  printf("true");
}

int main(void) { 
   
  // keep this function call here
  CodelandUsernameValidation(coderbyteInternalStdinFunction(stdin));
  return 0;
    
}
```
