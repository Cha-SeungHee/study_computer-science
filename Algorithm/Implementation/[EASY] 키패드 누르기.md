``` java
import java.util.*;    

class Solution {
    public String solution(int[] numbers, String hand) {
        int currentLeft = 10;
        int currentRight = 12;
        
        StringBuilder sb = new StringBuilder();
        
        for (int number : numbers) {
            switch(number) {
                case 1:
                case 4:
                case 7:
                    sb.append("L");
                    currentLeft = number;
                    continue;
                    
                case 3:
                case 6:
                case 9:
                    sb.append("R");
                    currentRight = number;
                    continue;
                    
                case 2:
                case 5:
                case 8:
                case 0:
                    int diff = distance(number, currentLeft) - distance(number, currentRight);
                    if (diff < 0) {
                        sb.append("L");
                        currentLeft = number;
                    } else if (diff > 0) {
                        sb.append("R");
                        currentRight = number;
                    } else {
                        if (hand.equals("left")) {
                           sb.append("L");
                           currentLeft = number; 
                        } else {
                            sb.append("R");
                            currentRight = number;
                        }
                    }
                    continue;
                    
                default :
                    continue;
            }
            
        }
        
        
        return sb.toString();
    }
    
    private int distance(int target, int current) {
        Point pointTarget = convertToPoint(target);
        Point pointCurrent = convertToPoint(current);
        
        return Math.abs(pointTarget.y - pointCurrent.y) + Math.abs(pointTarget.x - pointCurrent.x);
    }
    
    private Point convertToPoint(int num) {
        Point point;
        
        if (num == 0) {
            point = new Point(3, 1);
        } else {
            point = new Point((num - 1) / 3, (num - 1) % 3);
        }
        
        return point;
    }
}

class Point {
    int y, x;
    
    Point (int y, int x) {
        this.y = y;
        this.x = x;
    }
}
```
