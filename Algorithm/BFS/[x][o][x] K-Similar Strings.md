시간 초과 코드

```java  
/*
1. String 순회하면서 각 글자의 index 구하기
- Linkedlist
- HashMap<Character, LinkedList<Character>>

2. String 순회 (idx)
- B의 글자와 동일하면 pass
- B의 글자와 다르면 해당 글자의 모든 indexd와 swap (backtracking)


recursion
- String이 동일하거나 idx가 끝을 도달하면 0을 return
- 

- 0이 아닌 경우에만 의미 있는 값
*/

class Solution {
    public int kSimilarity(String A, String B) {
        if (A==null || B==null) return 0;
        
        return recursion(A, B, 0);
    }
    
    private int recursion(String A, String B, int idx) {
        if (A.equals(B) || idx == A.length()) return 0;
        
        char charA = A.charAt(idx);
        char charB = B.charAt(idx);
        
        int min = Integer.MAX_VALUE;
        if (charA == charB) {
            return recursion(A, B, idx+1);
        } else {                
            for (int j=idx+1; j<A.length(); j++) {
                if (A.charAt(j) == charB) {
                    String newString = swap(A, j, idx);
                    min = Math.min(min, recursion(newString, B, idx+1)+1);
                }
            }
        }
        
        return min;
    }
    
    private String swap(String A, int idx1, int idx2) {
        char[] chars = A.toCharArray();
        
        char tmp = chars[idx1];
        chars[idx1] = chars[idx2];
        chars[idx2] = tmp;
        
        return new String(chars);
    }
}
```

#### 확인
1. HashMap<Character, ArrayList<Integer>> map 사용의 문제점
- swap 이후 swap된 문자의 list의 index 정보를 변경해줘야 한다. 해주면 되긴 할 듯. 다만 코드가 복잡해질 것 같아서 멈춤.

2. 매번 느끼는 것이지만 최대한 자세히 계획을 세우고 난 뒤에 코드를 짜야한다.

3. 아래의 코드가 유사한 개념으로 짠 코드인데, Set을 이용하여, 중복 계산을 줄일 수 있는 듯 하다.

```java  
public int kSimilarity(String A, String B) {
	Queue<String> q = new ArrayDeque<>();
	q.add(A);
	int cnt = 0;
	Set<String> seen = new HashSet<>();
	while (!q.isEmpty()) {
		int size = q.size();
		for (int k = 0; k < size; k++) {
			A = q.poll();
			if (A.equals(B)) return cnt;
			int i = 0;
			while (A.charAt(i) == B.charAt(i)) i++;
			for (int j = i + 1; j < B.length(); j++) {
				if (A.charAt(i) != B.charAt(j)) continue;
				String tmp = swap(i, j, A);
				if (seen.add(tmp)) q.add(tmp);
			}
		}
		cnt++;
	}
	return -1;
}

private String swap(int i, int j, String s) {
	char[] chs = s.toCharArray();
	char tmp = chs[i];
	chs[i] = chs[j];
	chs[j] = tmp;
	return new String(chs);
}
```
