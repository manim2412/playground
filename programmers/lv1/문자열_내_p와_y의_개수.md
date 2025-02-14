# https://school.programmers.co.kr/learn/courses/30/lessons/12916
## java
```java
class Solution {
    boolean solution(String s) {
        s = s.toLowerCase(); 
        int countP = 0; 
        int countY = 0;
        for (int i=0; i<s.length(); i++) {
            char ch = s.charAt(i); 
            if (ch == 'p') {
                countP += 1;
            }
            if (ch == 'y') {
                countY += 1;
            }
        }
        return countP == countY;
    }
}
```
## javascript
```js
function solution(s){
    s = s.toLowerCase();
    countP = 0; 
    countY = 0;
    for (let i=0; i<s.length; i++) {
        ch = s.substring(i, i+1); 
        if (ch === 'p') {
            countP += 1;
        }
        if (ch === 'y') {
            countY += 1;
        }
    }
    return countP === countY;
}
```
