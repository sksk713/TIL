---
id: doit01
title: 01.기본 알고리즘
# sidebar_label: 01.기본 알고리즘
# slug: /
---

< Do it! 자료구조와 함께 배우는 알고리즘 입문 자바 편 >

# 정의

>문제를 해결하기 위한 것으로, 명확하게 정의되고 순서가 있는 유한 개의 규칙으로 이루어진 집합

## 입출력


### Scanner
```java
Scanner stdIn = new Scanner(System.in);

stdIn.nextInt(); // 정수입력
stdIn.next(); // 문자열(스페이스, 줄 바꿈 문자로 구분)
stdIn.nextLine(); // 문자열 1줄
```
- stdIn은 표준 입력 스트림(System.in)에서 문자나 숫자를 꺼내는 장치 역할을 한다.
- System.in의 리턴값은 InputStream이며 byte단위로 데이터를 읽는다.

### BufferedReader
```java
BufferedReader stdIn = new BufferedReader(new InputStreamReader(System.in));
string[] s = stdIn.readLine().split(" ");
```
- InputStreamReader는 byte단위로 처리하던 걸 char단위로 처리하도록 변환해준다.
- BufferedReader는 InputStreamReader로 변환된 스트림에 버퍼 기능을 추가한 것을 말한다.
- 버퍼로 인해 속도가 가장 빠르다.
- 01_1.연습문제(github 업로드)
    - [CH01_Q1](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q1.java)
    - [CH01_Q2](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q2.java)
    - [CH01_Q3](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q3.java)



## 반복
- 하나의 변수를 사용하면 for문을 사용하는 것이 편하다.
- for문 내에 선언된 변수는 for문 내에서만 유효하다.

1. do while문 - 사후 판단 반복문
2. for, while문 - 사전 판단 반복문

- 01_2.연습문제(github 업로드)
    - [CH01_Q7](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q7.java)
    - [CH01_Q8](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q8.java)
    - [CH01_Q9](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q9.java)
    - [CH01_Q10](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q10.java)
    - [CH01_Q11](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q11.java)
    - [CH01_Q12](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q12.java)
    - [CH01_Q13](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q13.java)
    - [CH01_Q14](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q14.java)
    - [CH01_Q15](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q15.java)
    - [CH01_Q16](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q16.java)
    - [CH01_Q17](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C1_Q17.java)



