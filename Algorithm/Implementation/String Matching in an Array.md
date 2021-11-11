``` c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
char ** stringMatching(char ** words, int wordsSize, int* returnSize){
    int index = 0;
    char** substring = malloc(sizeof(char*) * (wordsSize + 1));
    
    for (int i = 0; i < wordsSize; i++) {
        for (int j = 0; j < wordsSize; j++) {
            if (i == j) continue;
            if (strstr(words[j], words[i])) {
                substring[index] = words[i];
                index += 1;
                break;
            }            
        }
    }
    
    *returnSize = index;
    substring[index] = '\0';    
    return substring;
}
```
