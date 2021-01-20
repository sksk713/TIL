---
id: doit07
title: 07.문자열 검색
---

< Do it! 자료구조와 함께 배우는 알고리즘 입문 자바 편 >


## 문자열 검색
> 어떤 패턴을 찾기 위해서 원본 문자열을 하나하나 처음부터 다 검사한다.
- 효율은 좋지않다.

```java
static int bfMatch(String txt, String pat){
    int pt = 0;
    int pp = 0;

    while(pt != txt.length() && pp != pat.length()){
        if(txt.charAt(pt) == pat.charAt(pp)){
            pp++;
            pt++;
        }
        else{
            pt = pt - pp + 1;
            pp = 0;
        }
    }
    if(pp == pat.length()){
        return pt - pp;
    }
    return -1;
}
```

## KMP
> 브루트-포스는 패턴을 옮기고 다시 처음부터 하나씩 새로 하는 반면 KMP는 내부 중복되는 문자열을 미리 파악한다음 그 다음부터 탐색한다.

```java
static int kmpMatch(String txt, String pat){
    int pt = 1;
    int pp = 0;
    int[] skip = new int[pat.length() + 1];

    skip[pt] = 0;
    while(pt != pat.length()){
        if(pat.charAt(pt) == pat.charAt(pp)){
            ship[++pt] = ++pp;
        }
        else if(pp == 0){
            skip[++pt] = pp;
        }
        else {
            pp = skip[pp];
        }

        pt == pp = 0;
        while(pt != txt.length() && pp != pat.length()){
            if(txt.charAt(pt) == pat.charAt(pp)){
                pt++;
                pp++;
            }
            else if(pp == 0){
                pt++;
            }
            else{
                pp = skip[pp];
            }
            if(pp == pat.length()){
                return pt - pp;
            }
            return -1
        }
    }
}
```
## Boyer-Moore법


---
중요한 내용이 아닌 거 같음 / 나중에 필요하면 하기