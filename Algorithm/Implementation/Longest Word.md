``` c
#include <stdio.h> 
#include <string.h>
#include <stdlib.h>

void LongestWord(char * sen) {
  
  // code goes here  
  int len = strlen(sen);
  char * newSen = malloc(sizeof(char) * (len + 1));
  char * max = malloc(sizeof(char) * (len + 1));
  int maxLen = -1;
  strcpy(newSen, sen);

  char *ptr = strtok(newSen, " ");

  while (ptr != NULL) {
    // printf("%s\n", ptr);
    int chunkLen = strlen(ptr);
    char * temp = malloc(sizeof(char) * (chunkLen+1));
    int indexTemp = 0;
    for (int i = 0; i < chunkLen; i++) {
      if (isalpha(ptr[i]) || isdigit(ptr[i])) {
        temp[indexTemp] = ptr[i];
        indexTemp += 1;
      } else {
        break;
      }
    }
    temp[indexTemp] = '\0';
    if (indexTemp > maxLen) {
      maxLen = indexTemp;
      strcpy(max, temp);
      // printf("%s\n", max);
    }
    free(temp);
    ptr = strtok(NULL, " ");
  }

  printf("%s", max);

}

int main(void) { 
   
  // keep this function call here
  LongestWord(coderbyteInternalStdinFunction(stdin));
  return 0;
    
}
```

``` c
#include <stdio.h>
#include <string.h>
void LongestWord(char *sen) {
  char word[20]="";
  char buff[20]="";
  int n=0,i;
  for(i=0;i<strlen(sen);i++)
  {
      if((sen[i]>=97 && sen[i]<=122)||(sen[i]>=65 && sen[i]<=90)||(sen[i]>=48 && sen[i]<=57))
	  buff[n++]=sen[i];
      else
	    n=0;
      if(strlen(buff)>strlen(word))
            strcpy(word,buff);
  }

    printf("%s",word);
```
