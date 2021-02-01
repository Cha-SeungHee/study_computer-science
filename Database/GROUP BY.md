#### 고양이와 개는 몇 마리일까? - GROUP BY

``` SQL
SELECT ANIMAL_TYPE, COUNT(ANIMAL_ID) AS COUNT 
FROM ANIMAL_INS 
GROUP BY ANIMAL_TYPE 
ORDER BY ANIMAL_TYPE
```

#### 특정 수 이상의 동물 이름 및 수 찾기 - COUNT, GROUP BY, HAVING
``` SQL
SELECT NAME, COUNT(NAME) AS COUNT 
FROM ANIMAL_INS 
GROUP BY NAME 
HAVING COUNT(NAME) >= 2
ORDER BY NAME
```

- COUNT와 같은 집계함수 (COUNT, AVG, SUM, MAX, MIN)을 쓰면 WHERE 절에서 WHERE COUNT(NAME) >= 2 같은 절을 사용할 수 없음   
- WHERE 절은 행에 조건을 걸어 가져오는데 집계함수를 사용하면 이미 조건을 걸어서 가져온 것이기에 불가  
- HAVING을 사용하면 집계함수를 사용했더라도 조건을 걸어 조회 가능

``` SQL
SELECT NAME, COUNT 
FROM (
    SELECT NAME, COUNT(NAME) AS COUNT 
    FROM ANIMAL_INS
    GROUP BY NAME
    ) SQ1
WHERE COUNT >= 2
ORDER BY NAME
```

- 또는 서브쿼리를 활용하고 집계함수는 서브쿼리 내에서 사용하는 방법 또한 있다  
- 서브 쿼리는 괄호만 만들면 되는 것이 아니고 이름까지 정해주어야 한다는 점을 잊지 말자  

#### 입양 시각 구하기(1) - COUNT, GROUP BY, HAVING
``` SQL
SELECT HOUR(DATETIME) AS HOUR, COUNT(DATETIME) FROM ANIMAL_OUTS 
GROUP BY HOUR HAVING HOUR >= 9 AND HOUR <= 19
ORDER BY HOUR
```
- 이 경우에는 존재하는 값에 대해서만 값이 출력되는 듯 하다  

#### 입양 시각 구하기(2) - SET
``` SQL
SET @hour := -1; -- 변수 선언

SELECT (@hour := @hour + 1) as HOUR,
(SELECT COUNT(*) FROM ANIMAL_OUTS WHERE HOUR(DATETIME) = @hour) as COUNT
FROM ANIMAL_OUTS
WHERE @hour < 23
```

- SET 옆에 변수명과 초기값을 설정 가능  
- @가 붙은 변수는 프로시저가 종료되어도 유지. 이를 통해 값을 누적하여 0부터 23까지 표현 가능  
- @hour은 초기값을 -1로 설정. PL/-SQL 문법에서 :=은 비교 연산자 =과 혼동을 피하기 위한의 대입 연산  
- SELECT (@hour := @hour +1) 은 @hour의 값에 1씩 증가시키면서 SELECT 문 전체를 실행  
- WHERE @hour < 23일 때까지, @hour 값이 계속 + 1씩 증가  
