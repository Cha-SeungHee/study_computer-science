#### DP

``` java
class Solution {
    public int countSubstrings(String s) {
        if (s == null || s.length() == 0) return 0;
        
        int count = 0;
        int sLen = s.length();        
        int[][] dp = new int[sLen][sLen];
        
        for (int i = 0; i < sLen; i++) {
            dp[i][i] = 1;
            count = count + 1;
        }
        
        for (int i = 0; i < sLen - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = 1;
                count = count + 1;
            }
        }
        
        for (int i = 2; i < sLen; i++) {
            for (int j = 0; j < sLen - 1; j++) {
                if (j + i < sLen && s.charAt(j) == s.charAt(j + i) && dp[j + 1][j + i - 1] == 1) {
                    dp[j][j + i] = 1;
                    count = count + 1;
                }
            }
        }
        
        return count;
    }
}
```

dp 값 base 설정시 개수가 홀수인 경우, 짝수인 경우에 대해서 모두 설정해주고 build-up 필요  

#### extendPalindromes
``` java
class Solution {
    public int countSubstrings(String s) {
        int count=0;
        for(int i=0;i<s.length();i++){
            count+=extractPalindrome(s,i,i);//odd length
            count+=extractPalindrome(s,i,i+1);//even length
        }
        return count;
    }
    public int extractPalindrome(String s, int left, int right){
        int count=0;
        while(left>=0 && right<s.length()&& (s.charAt(left)==s.charAt(right))){
            left--;
            right++;
            count++;
        }
        return count;
    }
}
```
