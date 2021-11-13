``` c
#include <stdio.h> 
#include <string.h>

void FirstFactorial(int num) {
  
  // code goes here  
  int result = 1;
  for (int i = 2; i<= num; i++) {
    result *= i;
  }

  printf("%d", result);

}

int main(void) { 
   
  // keep this function call here
  FirstFactorial(coderbyteInternalStdinFunction(stdin));
  return 0;
    
}
```
