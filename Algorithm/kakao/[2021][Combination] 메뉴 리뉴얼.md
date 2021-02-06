``` java
import java.util.*;

class Solution {
    HashMap<String, Integer> map;
    HashSet<String> set;

    public String[] solution(String[] orders, int[] course) {
        ArrayList<String> list = new ArrayList<>();
        String[] answer;
    
        for (int num : course) {
            map = new HashMap<>();
            int max = Integer.MIN_VALUE;
            
            for (String o : orders) {
                set = new HashSet<>();
                StringBuilder sb = new StringBuilder();
                char[] array = o.toCharArray();
                Arrays.sort(array);
                
                combination(array, 0, sb, num);
            }
            
            for (String key : map.keySet()) {
                max = Math.max(max, map.get(key));
            }
            
            for (String key : map.keySet()) {
                if (max >= 2 && map.get(key) == max) {
                    list.add(key);
                }
            }
        }
        
        answer = new String[list.size()];
        for(int i = 0; i < list.size(); i++) {
            answer[i] = list.get(i);
        }
        
        Arrays.sort(answer);
        
        return answer;
    }
    
    private void combination(char[] charArray, int index, StringBuilder sb, int num) {
        if (sb.length() == num) {
            String menu = sb.toString();
            if (set.add(menu)) {
                if (!map.containsKey(menu)) {
                map.put(menu, 0);
                }
                map.put(menu, map.get(menu) + 1);
            }
        }
        
        if (index == charArray.length) return;
        
        sb.append(charArray[index]);
        combination(charArray, index + 1, sb, num);
        sb.deleteCharAt(sb.length() - 1);
        combination(charArray, index + 1, sb, num);
    }
}
```


``` java
class Solution {
    static HashMap<String,Integer> map;

    public static void combination(String str, StringBuilder sb, int idx, int cnt, int n){
        if(cnt == n) {
            map.put(sb.toString(),map.getOrDefault(sb.toString(),0)+1);
            return;
        }

        for(int i = idx ; i<str.length();i++){
            sb.append(str.charAt(i));

            combination(str,sb,i+1,cnt+1,n);

            sb.delete(cnt,cnt+1);
        }
    }

    public ArrayList<String> solution(String[] orders, int[] course) {
        ArrayList<String> answer = new ArrayList<>();

        for(int i =0;i<orders.length;i++){
            char[] charArr = orders[i].toCharArray();

            Arrays.sort(charArr);

            orders[i] = String.valueOf(charArr);
        }

        for(int i =0;i<course.length;i++){
            map = new HashMap<>();

            int max = Integer.MIN_VALUE;

            for(int j =0;j<orders.length;j++){
                StringBuilder sb = new StringBuilder();

                if(course[i]<=orders[j].length()) {
                    combination(orders[j],sb,0,0,course[i]);
                }
            }

            for(Entry<String,Integer> entry : map.entrySet()){
                max = Math.max(max,entry.getValue());
            }

            for(Entry<String,Integer> entry : map.entrySet()){
                if(max >=2 && entry.getValue() == max) answer.add(entry.getKey());
            }
        }

        Collections.sort(answer);

        return answer;
    }
}
```
