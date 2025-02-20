# https://school.programmers.co.kr/learn/courses/30/lessons/42748
```java
import java.util.*; 
import java.util.stream.*; 

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int n = commands.length; 
        int[] answer = new int[n]; 
        for (int i=0; i<n; i++) {
            answer[i] = getResult(array, commands[i]); 
        }
        return answer;
    }
    
    public int getResult(int[] array, int[] command) {
        int[] arr = IntStream
            .range(command[0]-1, command[1])
            .map(i -> array[i])
            .toArray(); 
        Arrays.sort(arr); 
        return arr[command[2]-1]; 
    }
}
```
