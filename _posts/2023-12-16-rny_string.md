---
categories: [Programmers, Java]
tags: [Programmers, Java] 
---

<https://school.programmers.co.kr/learn/courses/30/lessons/181863>{:target="_blank"}

![문제](/assets/img/programmers/java/rny_string(1).png)
![문제](/assets/img/programmers/java/rny_string(2).png)

- 문제 풀이

```java
class Solution {
    public String solution(String rny_string) {           
        if(rny_string.contains("m"))
            rny_string = rny_string.replace("m", "rn");
        
        return rny_string;
    }
}
```
```java
class Solution {
    public String solution(String rny_string) {
        return rny_string.replace("m", "rn");
    }
}
```
