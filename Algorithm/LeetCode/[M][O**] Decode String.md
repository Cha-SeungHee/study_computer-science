``` java
class Solution {
    public String decodeString(String s) {
        Deque<Character> queue = new LinkedList<>();
        for (char c : s.toCharArray()) queue.offer(c);
        return helper(queue);
    }
    
    public String helper(Deque<Character> queue) {
        StringBuilder sb = new StringBuilder();
        int num = 0;
        while (!queue.isEmpty()) {
            char c= queue.poll();
            if (Character.isDigit(c)) {
                num = num * 10 + c - '0';
            } else if (c == '[') {
                String sub = helper(queue);
                for (int i = 0; i < num; i++) sb.append(sub);   
                num = 0;
            } else if (c == ']') {
                break;
            } else {
                sb.append(c);
            }
        }
        return sb.toString();
    }
}
```

- Stack을 이용해서 풀었으나 재귀로 풀었을 때 훨씬 효율적

``` java
class Solution {
    public String decodeString(String s) {
        
        Stack<String> sol = new Stack(); //stack to hold the intermediate solutions
        Stack<Integer> multiplier = new Stack(); //stack to hold the number of times to multiply string
        
        String solution = ""; //resulting solution string
        int number = 0; // keep track of the multiplier
        
        for (int i = 0; i < s.length(); i++) {
            if (Character.isDigit(s.charAt(i))) {
                number = number * 10 + Character.getNumericValue(s.charAt(i)); 
            } else if (s.charAt(i) == '[') {
                multiplier.push(number);
                number = 0;

                sol.push(solution);
                solution = "";               
            } else if (s.charAt(i) == ']') {
                int mul = multiplier.pop();
                String poper = sol.pop();

                solution = poper + repeat(solution, mul);
            } else {
                solution += s.charAt(i);
            }
        }
        return solution;
    }
    
    public String repeat(String toRepeat, int repeatCount) {
        StringBuilder sb = new StringBuilder();
        int i = 0;
        while (i < repeatCount) {
            sb.append(toRepeat);
            i++;
        }
        return sb.toString();
    }
}
```
