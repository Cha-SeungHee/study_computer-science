#### NaN 안나는 코드
```java 
class Solution {
    public double pow(double x, int n){
        if(n == 0) return 1;
        if(n == 1) return x;
        if(n % 2 == 0)
            return pow(x * x, n/2);
        return x * pow(x * x, n/2);
    }
    public double myPow(double x, int n) {
        if(n < 0)
            return 1.0/pow(x, -n);
        return pow(x, n);
    }
}
``` 
#### NaN 나는 코드
```java 
class Solution {
    public double myPow(double x, int n) {
        if (n==0) return 1;
        
        int pow = Math.abs(n);
        double result = 0;
        if (pow%2 == 0) {
            result = myPow(x*x,pow/2);            
        } else {
            result = x*myPow(x*x,pow/2);
        }
        
        if (n < 0) result = (double)((double)1/result);        
        
        return result;
    }
}
``` 

차이를 모르겠다...


Runtime Error Message:
java.lang.NumberFormatException: Infinite or NaN
  at line 923, java.base/java.math.BigDecimal.<init>
  at line 900, java.base/java.math.BigDecimal.<init>
	at __Serializer__.serialize(Unknown Source)
  at line 92, __Driver__.main
Last executed input:
2.00000
-2147483648
