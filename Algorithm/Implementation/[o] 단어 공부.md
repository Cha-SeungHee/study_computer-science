```` java
class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String word = sc.next();
        int[] count = new int[26];
        int max = 0;
        int numMax = 0;
        int indexMax = 0;
        
        for (int i = 0; i < word.length(); i++) {
            char ch = word.charAt(i);
            
            if (isUpperCase(ch)) {
                int index = ch - 'A';                
                count[index] = count[index] + 1;                 
                max = Math.max(max, count[index]);
            }
            
            if (isLowerCase(ch)) {
                int index = ch - 'a';                
                count[index] = count[index] + 1;                
                max = Math.max(max, count[index]);
            }
        }
        
        for (int i = 0; i < word.length(); i++) {
            if (count[i] == max) {
                numMax = numMax + 1;
                indexMax = i;
            }
        }
        
        if (numMax > 1) {
            System.out.println("?");
        } else {
            System.out.println((char)('A' + indexMax);
        }
    }
    
    private boolean isUpperCase(char ch) {
        return 'A' <= ch && ch <= 'Z';
    }
    
    private boolean isLowerCase(char ch) {
        return 'a' <= ch && ch <= 'z';
    }    
}
````
