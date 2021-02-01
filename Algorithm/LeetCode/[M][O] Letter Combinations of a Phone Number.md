``` java
class Solution {
    public List<String> letterCombinations(String digits) {
        List<String> list = new ArrayList<>();
        
        if (digits == null || digits.length() == 0) return list;
        
        String[] numDigit = new String[10];
        numDigit[2] = "abc";
        numDigit[3] = "def";
        numDigit[4] = "ghi";
        numDigit[5] = "jkl";
        numDigit[6] = "mno";
        numDigit[7] = "pqrs";
        numDigit[8] = "tuv";
        numDigit[9] = "wxyz";
        
        StringBuilder sb = new StringBuilder();
        
        dfs(list, sb, numDigit, 0, digits);
        
        return list;
    }
    
    private void dfs(List<String> list, StringBuilder sb, String[] numDigit, int index, String digits) {
        if (index == digits.length()) {
            list.add(sb.toString());
            return;
        }
        
        String string = numDigit[digits.charAt(index) - '0'];
        
        for (int i = 0; i < string.length(); i++) {
            sb.append(string.charAt(i));
            dfs(list, sb, numDigit, index + 1, digits);
            sb.deleteCharAt(sb.length() - 1);
        }        
    }
}
```
