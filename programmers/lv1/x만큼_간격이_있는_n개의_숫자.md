# https://school.programmers.co.kr/learn/courses/30/lessons/12954?language=java
## java
```java
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n]; 
        for (int i=0; i<answer.length; i++) {
            answer[i] = (long) (i+1) * x;
        }
        return answer;
    }
}
```
## javascript
```js
function solution(x, n) {
    let answer = [];
    for (let i=0; i<n; i++) {
        answer.push(x*(i+1));
    }
    return answer;
}
```
