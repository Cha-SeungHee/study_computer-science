``` c
#include <stdio.h> 
#include <string.h>
#include <stdbool.h>

typedef struct {
  int parent;
  int left;
  int right;
}node;

void TreeConstructor(char * strArr[], int arrLength) {
  
  bool isValid = true;
  // code goes here  
  node nodeList[10000];
  for (int i = 0; i < 10000; i++) {
    nodeList[i].left = -1;
    nodeList[i].right = -1;
    nodeList[i].parent = -1;
  }

  for (int i = 0; i < arrLength; i++) {
    int child = 0, parent = 0;
    sscanf(strArr[i], "(%d,%d)", &child, &parent);
    
    if (nodeList[child].parent != -1) {
      isValid = false;
      break;
    } else {
      nodeList[child].parent = parent;
    }

    if (child > parent) {      
      if (nodeList[parent].right != -1) {
        isValid = false;
        break;
      }
      nodeList[parent].right = child;
    } else {
      if (nodeList[parent].left != -1) {
        isValid = false;
        break;
      }
      nodeList[parent].left = child;
    }
  }

  printf(isValid ? "true" : "false");
}

int main(void) { 
   
  // keep this function call here
  char * A[] = coderbyteInternalStdinFunction(stdin);
  int arrLength = sizeof(A) / sizeof(*A);
  TreeConstructor(A, arrLength);
  return 0;
    
}
```
