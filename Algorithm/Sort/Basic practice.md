### 위에서 아래로
``` py
n = int(input())

array = [int(input()) for _ in range(n)]

print(sorted(array, reverse=True))
```


### 성적이 낮은 순서로 학생 출력하기
``` py
n = int(input())

student = []

for i in range(n):
    name, score = input().split()
    student.append((name, int(score)))

student.sort(key=lambda s: s[1])

for s in student:
    print(s[0], end=' ')

```

### 두 배열의 원소 교체
``` py
n, k = map(int, input().split())

A = sorted(list(map(int, input().split())))
B = sorted(list(map(int, input().split())), reverse=True)

for i in range(k):
    if A[i] < B[i]:
        A[i], B[i] = B[i], A[i]

print(sum(A))
```
