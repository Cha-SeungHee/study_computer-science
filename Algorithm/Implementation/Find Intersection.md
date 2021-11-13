``` c
#include <stdio.h> 
#include <string.h>
#include <stdlib.h>

void FindIntersection(char * strArr[], int arrLength) {
  int indexA = 0;
  int lenA = strlen(strArr[0]), lenB = strlen(strArr[1]);
  char *strA = malloc(sizeof(char) * (lenA + 1));
  char *strB = malloc(sizeof(char) * (lenB + 1));
  strcpy(strA, strArr[0]);
  strcpy(strB, strArr[1]);

  char arrayA[lenA][5];
  
  char *ptrA = strtok(strA, " ,");
  while (ptrA != NULL) {
    strcpy(arrayA[indexA], ptrA);
    ptrA = strtok(NULL, " ,");
    indexA += 1;
  }
  
  char* result = malloc(sizeof(char) * lenA);
  char *ptrB = strtok(strB, " ,");
  while (ptrB != NULL) {
    for (int i = 0; i < lenA; i++) {
      if (strcmp(arrayA[i], ptrB) == 0) {
        if(strlen(result) == 0) {
          strcpy(result, arrayA[i]);
        } else {
          strcat(result, ",");
          strcat(result, arrayA[i]);          
        }
        break;
      }
    }
    ptrB = strtok(NULL, " ,");    
  }

  if (strlen(result) == 0) {
    printf("false");
  } else {
    printf("%s\n", result);
  }
}

int main(void) { 
   
  // keep this function call here
  char * A[] = coderbyteInternalStdinFunction(stdin);
  int arrLength = sizeof(A) / sizeof(*A);
  FindIntersection(A, arrLength);
  return 0;
    
}
```
