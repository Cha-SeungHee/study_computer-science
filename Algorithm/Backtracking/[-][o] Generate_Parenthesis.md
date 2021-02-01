```java  
class Solution {
    public List<String> generateParenthesis(int n) {
        if (n == 0) return new ArrayList<String>();
        
        List<String> list = new ArrayList<>();
        char[] brackets = new char[n<<1];        
        
        generateParenthesisHelper(brackets, 0, 0, 0, n, list);
        return list;
    }
    
    public void generateParenthesisHelper(char[] brackets, int idx, int ln, int rn, int n, List<String> list) {
        if (idx == (n<<1)) {
            list.add(new String(brackets));
            return;
        }
        
        if (ln < n) {
            brackets[idx] = '(';
            generateParenthesisHelper(brackets, idx+1, ln+1, rn, n, list);
        }
        
        if (rn < ln) {
            brackets[idx] = ')';
            generateParenthesisHelper(brackets, idx+1, ln, rn+1, n, list);
        }
    }
}
```

#### 확인
new String(brackets); // 처음에는 brackets.toString()으로 시도
