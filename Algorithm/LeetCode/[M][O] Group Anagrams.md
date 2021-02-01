``` java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> map = new HashMap<>();
        
        List<List<String>> list = new ArrayList<>();
        
        for (String str : strs) {
            char[] chars = str.toCharArray();
            
            Arrays.sort(chars);
            
            String sortedStr = new String(chars);
            
            if (!map.containsKey(sortedStr)) {
                map.put(sortedStr, new ArrayList<>());
            }
            map.get(sortedStr).add(str);
        }
        
        for (String str : map.keySet()) {
            list.add(map.get(str));
        }
        
        return list;
    }
}
```
