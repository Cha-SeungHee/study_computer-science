1) 시간 초과 
``` py
import sys

sys.setrecursionlimit(10**6)

def solution(k, room_number):
    rooms = [i for i in range(k+1)]
    result = []
    
    for number in room_number:
        result.append(findParent(rooms, number))                           
    
    return result


def findParent(rooms, child):        
    if rooms[child] == child:
        rooms[child] = child + 1
        return child
    
    rooms[child] = findParent(rooms, rooms[child])
    return rooms[child]
```

2) 통과 (차이: 배열 대신 dictionary 사용)
- dictionary에서는 불필요한 배열 생성 과정이 시간을 더 오래 걸리게 만드는 영향일까? 

``` py
import sys

sys.setrecursionlimit(10 ** 6)


def solution(k, room_number):
    rooms = {}
    result = []

    for number in room_number:
        result.append(findParent(rooms, number))

    return result


def findParent(rooms, child):
    if child not in rooms:
        rooms[child] = child + 1
        return child

    rooms[child] = findParent(rooms, rooms[child])
    return rooms[child]
```
