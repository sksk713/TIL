---
id: doit08
title: 08.리스트
---

< Do it! 자료구조와 함께 배우는 알고리즘 입문 자바 편 >

## 리스트
> 데이터를 순서대로 나열한 자료구조

### 배열 선형 리스트

1. 쌓이는 데이터의 크기를 미리 알아야 한다.
2. 데이터의 삽입, 삭제에 따라 데이터를 모두 옮겨야 하기 때문에 효율이 좋지 않다.

```java
class Person{
    int memNo;
    String name;
    String phoneNo;
}
Person [] data = {
    new Person(a);
    new Person(b);
    new Person(c);
    new Person(d);
    new Person(e);
    new Person(x);
    new Person(x);
}
```

### 포인터로 연결 리스트 만들기

```java
class Node<E>{ // 제네릭
    E data; // 데이터
    Node<E> next; // 다음 노드를 가리키는 포인터
}
```
- `Node<E>`는 제네릭으로 구현되므로 데이터형 E는 임의의 클래형이 허용된다.

```java
public class LinkedList<E>{
    class Node<E>{
        private E data;
        private Node<E> next;

        Node(E data, Node<E> next){
            this.data = data;
            this.next = next;
        }
    }
    private Node<E> head; //머리노드
    private Node<E> crnt; //현재노드
}
```
#### 포인터로 탐색
```java
public E search(E obj, Comparator<? super E> c){
    Node<E> ptr = head; // 현재 스캔 중인 노드

    while(ptr != null){
        if(c.compare(obj, ptr.data) == 0){ // 검색 성공
            crnt = ptr;
            return ptr.data;
        }
        ptr = ptr.next; // 다음 노드 선택
    }
    return null; // 검색실패
}
```

### 커서로 연결 리스트 만들기
> 노드용 객체를 위해 메모리 영역을 만들고 해제하는 비용 때문에 배열을 이용해 연결리스트를 사용한다.

