---
id: doit03
title: 03.검색
---

< Do it! 자료구조와 함께 배우는 알고리즘 입문 자바 편 >

# 검색 알고리즘
> 데이터 집합에서 원하는 값을 가진 요소를 찾아내는 것


1. 선형 검색
- 무작위로 늘어놓은 데이터 모임에서 검색 수행
2. 이진 검색
- 일정한 규칙으로 늘어놓은 데이터 모임에서 아주 빠른 검색 수행
3. 해시법
- 추가, 삭제가 자주 일어나는 데이터 모임에서 아주 빠른 검색 수행
    - 체인법: 같은 해시 값의 데이터를 선형 리스트로 연결하는 방법
    - 오픈 주소법: 데이터를 위한 해시 값이 충돌할 때 재해시하는 방법

## 선형 검색
> 원하는 키 값을 갖는 요소를 찾을때까지 맨 앞부터 순서대로 검색

### 보초법
- 종료조건
    1. 검색할 값을 발견하지 못하고 배열의 끝을 지나간 경우
    2. 검색할 값과 같은 요소를 발견한 경우(중복데이터)

- 위의 비용을 반으로 줄이는 방법을 `보초법(sentinel method)`라고 한다.

```java
static int seqSearchSen(int[] a, int n. int key){
    int i = 0;

    a[n] = key; // 마지막 배열값에 보초 추가

    while(true){
        if(a[i] == key){
            break;
        }
        i++;
    }
    return i == n ? -1 : i;
}
```

## 이진 검색
> 이미 데이터들이 정렬이 되어있는 상황에서 적용
- 간략한 설명
    - 인덱스 3개(처음, 중간, 끝)를 설정하고 key값을 기준으로 앞 뒤 절반씩 자른다.

```java
static int binSearch(int[] a, int n, int key){
    int pl = 0;
    int pr = n - 1;

    do {
        int pc = (pl + pr) / 2;
        if(a[pc] == key){
            return pc;
        }
        else if(a[pc] < key){
            pl = pc + 1; // 검색 범위를 뒤쪽 반으로 좁힘
        }
        else{
            pr = pc - 1; // 검색 범위를 앞쪽 반으로 좁힘
        }while (pi <= pr);

        return -1;
    }
}
```

- 03.연습문제(github 업로드)
    - [CH03_Q1](https://github.com/sksk713/Doit_algorithm/blob/master/Chap3/C3_Q1.java)
    - [CH03_Q2](https://github.com/sksk713/Doit_algorithm/blob/master/Chap3/C3_Q2.java)

## 복잡도
> 알고리즘의 성능을 객관적으로 평가하는 기준
> 1. 시간 복잡도: 실행에 필요한 시간을 평가한 것
> 2. 공간 복잡도: 기억 영역과 파일 공간이 얼마나 필요한가를 평가한 것

### 선형 검색의 시간복잡도
```java
static int seqSearch(int[] a, int n, int key){
    int i = 0;                  // O(1)
    while(i < n){               // 2/N == O(N)
        if(a[i] == key){        // 2/N == O(N)
            return i;           // O(1)
        }
        i++;                    // 2/N == O(N)
    }
    return -1;                  // O(1)
}


### 이진 검색의 시간복잡도
```java
static int binSearch(int[] a, int n, int key){
    int pl = 0;                     //O(1)
    int pr = n - 1;                 //O(1)

    do {
        int pc = (pl + pr) / 2;     //O(LOGN)
        if(a[pc] == key){           //O(LOGN)
            return pc;              //O(1)
        }
        else if(a[pc] < key){       //O(LOGN)
            pl = pc + 1;            //O(LOGN)
        }
        else{
            pr = pc - 1;            //O(LOGN)
        }while (pi <= pr);          //O(LOGN)

        return -1;                  //O(1)
    }
}
```

- java.util.Arrays 클래스의 binarySearch 메서드 제공

## 메서드
1. 인스턴스 메서드(비정적 메서드)
    - static이 붙지 않음
2. 클래스 메서드(정적 메서드)

- 둘의 차이는 `메서드가 인스턴스에 포함되는지`의 여부

### 호출 방식
1. 인스턴스 메서드: 클래스형 변수 이름.메서드 이름
2. 클래스 메서드: 클래스 이름.메서드 이름