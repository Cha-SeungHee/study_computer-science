O(n^2)
``` c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* twoSum(int* nums, int numsSize, int target, int* returnSize){
    *returnSize = 2;
    int* result = malloc(*returnSize * sizeof(int));
    bool find = false;
    
    for (int i = 0; i < numsSize; i++ ){
        for (int j = i + 1; j < numsSize; j++) {
            if (nums[i] + nums[j] == target) {
                result[0] = i;
                result[1] = j;
                find = true;
                break;
            }
        }
        if (find) break;
    }
    
    return result;
}
```

O(n) - 정렬
``` c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
typedef struct {
    int value;
    int index;    
}map;

int compareMap(void * A, void * B) {
    map mapA = *(map *)A;
    map mapB = *(map *)B;
    
    return mapA.value - mapB.value;
}


int* twoSum(int* nums, int numsSize, int target, int* returnSize){
    *returnSize = 2;
    map mapper[numsSize];
    int* result = malloc(*returnSize * sizeof(int));        
    
    for (int i = 0; i < numsSize; i++) {        
        mapper[i].value = nums[i];
        mapper[i].index = i;
    }
    
    qsort(mapper, numsSize, sizeof(map), compareMap);
    
    int begin = 0, end = numsSize - 1;
    while (begin < end) {
        if (mapper[begin].value + mapper[end].value > target) {
            end -= 1;
        } else if (mapper[begin].value + mapper[end].value < target) {
            begin += 1;
        } else {
            result[0] = mapper[begin].index;
            result[1] = mapper[end].index;
            break;
        }
    }
    
    return result;
}
```
