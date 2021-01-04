---
id: doit02
title: 02.기본 자료구조
---

< Do it! 자료구조와 함께 배우는 알고리즘 입문 자바 편 >

## 자료구조
>데이터 단위와 데이터 자체 사이의 물리적 또는 논리적인 관계
- 자료를 효율적으로 이용할 수 있도록 컴퓨터에 저장하는 방법


## 배열
```java
- 선언: 형식A를 더 많이 사용한다.
int[] a; // 형식A
int a[]; // 형식B

- 자료형이 int 구성요소 개수가 5개인 배열 선언
a = new int[5]; // 변수 a가 참조하는 형식
a.length; // 배열 a의 길이
- 배열의 구성요소는 자동으로 0으로 초기화 된다.
```

- 배열 복제
```java
int[] b = a.clone(); // clone 메서드 사용
- b는 a를 참조하는 것이 아니라 복제를 참조하므로 다른 값 대입 가능
```
- 접근 제한자
    - 객체의 멤버에 대한 접근을 제한
    - 제한자 종류
        1. public: 모든 접근 허용
    	2. protected: 같은 패키지의 객체, 상속 관계의 객체 허용
    	3. default: 같은 패키지의 객체 허용
    	4. private: 현재의 객체 안에서만 허용
    - 접근 제한자 사용
    	1. 클래스: public, default
        2. 생성자: public, protected, default, private
        3. 멤버 변수: public, protected, default, private
        4. 멤버 메서드: public, protected, default, private
        5. 지역 변수: 접근 제한자를 사용할 수 없음


- String 클래스는 문자열 리터럴이고 String형 인스턴스에 대한 참조
    - 대표 메서드
```java
char charAt(int i)
int length()
boolean equals(String s)
```

## 다차원 배열
>"int형을 구성 자료형으로 하는 배열"을 구성 자료형으로 하는 배열

```java
선언
int[][] x = new int[2][4]; // 2행 4열
```

- 02.연습문제(github 업로드)
    - [CH02_Q1](https://github.com/sksk713/Doit_algorithm/blob/master/Chap2/C2_Q1.java)
    - [CH02_Q2](https://github.com/sksk713/Doit_algorithm/blob/master/Chap2/C2_Q2.java)
    - [CH02_Q3](https://github.com/sksk713/Doit_algorithm/blob/master/Chap2/C2_Q3.java)
    - [CH02_Q4](https://github.com/sksk713/Doit_algorithm/blob/master/Chap2/C2_Q4.java)
    - [CH02_Q6](https://github.com/sksk713/Doit_algorithm/blob/master/Chap1/C2_Q6.java)
    