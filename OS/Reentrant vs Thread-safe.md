#### Reentrant
- 여러 쓰레드에 의해 코드가 '동시에' 실행되더라도 실행 결과가 보장  
- thread 간에 공유하는 자원 자체가 없어야만 하는 코드  

#### Thread-safe 
- 여러 쓰레드에 의해 코드가 실행되더라도 실행 결과가 보장  
- 여러 쓰레드에 의해 실행되더라도 문제가 없으면 된다는 완화된 조건. 공유된 자원이 있더라도 여러 쓰레드가 동시에 접근하지 못하도록 Locking mechanism으로 막아주면 된다  

#### 문제 코드
- f(): g_var 값을 2를 더한다  
- g(): f()값에 2를 더해서 반환한다  

``` c
int g_var = 1;

int f()
{
  g_var = g_var + 2;
  return g_var;
}

int g()
{
  return f() + 2;
}
```
- thread-safe x, reentrant x  
- g_var 변수가 여서 쓰레드에 의해 공유되고 깨질 가능성 있음   

#### Thread-safe 코드
- 전역변수 g_var를 사용하는 구간에 lock을 걸어줌으로써 thread-safe   

``` c
int g_var = 1;
os_specific_lock lck;

int f()
{
  lock(&lck);
  
  g_var = g_var + 2;
  
  unlock(&lck);
  
  return g_var;
}

int g()
{
  return f() + 2;
}
```

#### Reentrant 코드
- 전역변수의 사용이 없도록 변경  

``` c
int f(int i)
{
  int priv = i;
  priv = priv + 2;
  return priv;
}

int g(int i)
{
  int priv = i;
  return f(priv) + 2;
}
```


"Thread-safe한 코드보다는 Reentrant한 코드로 작성하라"  
https://yesarang.tistory.com/m/214
