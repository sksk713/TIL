---
id: doit04
title: 04-1.스택
---

< Do it! 자료구조와 함께 배우는 알고리즘 입문 자바 편 >

## 스택
> 데이터를 일시적으로 저장하기 위해 사용하는 자료구조, 데이터의 입출력 순서는 후입선출

- Ex
```java
void x(){}
void y(){}
void z(){
    x();
    y();
}
int main(){
    z();
}
```
1. main 메서드 실행
2. z 메서드 호출
3. x 메서드 호출
4. x 메서드 실행 종료, z 메서드로 컴백
5. y 메서드 호출
6. y 메서드 실행 종료, z 메서드로 컴백
7. z 메서드 실행 종료, main 메서드로 컴백
8. main 메서드 실행 종료

### 스택 구현
```java
class IntStack{
    int max;
    int ptr;
    int[] stk;
}
```
- stk: 스택 본체
> 푸시된 데이터를 저장하는 스택 본체/ idx=0이 bottom이 됨
- max: 스택 용령
> 스택에 쌓을 수 있는 최대 데이터 수
- ptr: 스택 포인터
> 스택에 쌓여 있는 데이터 수를 나타내는 필드
- 생성자
> stk 생성을 하고 스택 과정을 준비
```java
public IntStack(int capacity){
    ptr = 0;
    max = capacity;
    try {
        stk = new int[max];
    } catch (OutOfMemoryError e) {
        max = 0;
    } 
}
```

#### 메서드
- push
```java
public int push(int x) throws OverflowIntStackException {
    if (ptr >= max)
        throw new OverflowIntStackException();
    return stk[ptr++] = x;
}
```
- pop
```java
public int pop() throws OverflowIntStackException {
    if (ptr <= 0)
        throw new EmptyIntStackException();
    return stk[ptr--];
}
```
- peek
> 스택 꼭대기 데이터 확인
```java
public int peek() throws OverflowIntStackException {
    if (ptr <= 0)
        throw new EmptyIntStackException();
    return stk[ptr - 1];
}
```

- indexOf
> stk 내부에 찾는 데이터가 포함되어 있는지, 배열 어디에 있는지 확인
```java
public int indexOf(int x){
for (int i = ptr - 1; i >= 0; i==){
    if (stk[i] == x){
        return i;
    }
    return -1;
}
```
- clear
> 스택 모든 요소 삭제
```java
public void clear(){
    ptr = 0;
}
```
- capacity
> 스택의 용량 반환
```java
public void capacity(){
    return max;
}
```
- size
> 스택에 쌓여 있는 데이터 수 반환
```java
public void size(){
    return ptr;
}
```
- IsEmpty
> 메서드가 비어 있는지 검사
```java
public boolean isEmpty(){
    return ptr <= 0;
}
```
- IsFull
> 스택이 가득 차있는지 검사
```java
public boolean isFull(){
    return ptr >= max;
}
```