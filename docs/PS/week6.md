---
id: week6
title: 6주차
---

# PS 6주차

## 문제번호: 9095(1, 2, 3 더하기)
- [문제링크](https://www.acmicpc.net/problem/9095)
- [깃허브](https://github.com/sksk713/PS/blob/master/6%EC%A3%BC%EC%B0%A8/9095.java)

### 풀이

- DP 문제는 일단 앞의 항들과의 연관성을 찾아보자.
1. 1일때 = 1
2. 2일때 = 2
3. 3일때 = 4
4. 4일때 = 7
5. 5일때 = 13

앞의 세개의 값을 더하면 구하고자 하는 index의 값을 구할 수 있다.

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static int[] result;

    public static void main(String[] args) throws IOException {
        int n = Integer.parseInt(br.readLine());
        result = new int[11];
        result[1] = 1;
        result[2] = 2;
        result[3] = 4;

        for(int i = 4; i < 11; i++){
            result[i] = result[i - 3] + result[i - 2] + result[i - 1];
        }

        for(int i = 0; i < n; i++){
            System.out.println(result[Integer.parseInt(br.readLine())]);
        }
    }
}
```

## 문제번호: 1389(케빈 베이컨의 6단계 법칙)
- [문제링크](https://www.acmicpc.net/problem/1389)
- [깃허브](https://github.com/sksk713/PS/blob/master/6%EC%A3%BC%EC%B0%A8/1389.py)

### 풀이

1. BFS 이용
2. 1번부터 차례대로 돌면서 bacon_num을 result에 저장한다.
    - visited 초기화
3. 0번째 부터 되어있으므로 최소값을 가진 인덱스에 1을 더해서 출력한다.

```python
from collections import deque


def bfs(start):
    visited[start] = True
    qu = deque()
    qu.append((start, 0))
    bacon_num = 0

    while qu:
        k, v = qu.popleft()

        for i in arr[k]:
            if not visited[i]:
                visited[i] = True
                qu.append((i, v + 1))
                bacon_num += v + 1

    return bacon_num


n, m = map(int, input().split())
arr = [list() for _ in range(n + 1)]
result = list()

for _ in range(m):
    i, j = (map(int, input().split()))
    arr[i].append(j)
    arr[j].append(i)


for i in range(1, n + 1):
    visited = [False for _ in range(n + 1)]
    result.append(bfs(i))

print(result.index(min(result)) + 1)
```

## 문제번호: 5430(AC)
- [문제링크](https://www.acmicpc.net/problem/5430)
- [깃허브](https://github.com/sksk713/PS/blob/master/6%EC%A3%BC%EC%B0%A8/5430.py)

### 풀이

```python
from collections import deque
T = int(input())

for _ in range(T):
    func = input()
    arr_num = int(input())
    arr = input()[1:-1]
    if len(arr) == 0:
        print("error")
        continue

    arr_list = deque(map(int, arr.split(",")))

    flag = False

    for i in func:
        if i == 'R':
            arr_list.reverse()
        else:
            if len(arr_list) == 0:
                flag = True
                break
            else:
                arr_list.popleft()
    
    if flag:
        print("error")
    else:
        print(list(arr_list))


```

## 문제번호: 1629(곱셈)
- [문제링크](https://www.acmicpc.net/problem/1629)
- [깃허브](https://github.com/sksk713/PS/blob/master/6%EC%A3%BC%EC%B0%A8/1629.py)

### 풀이
1. pow(x, y, z)가 x를 y번 곱하고 z로 나눈 나머지를 출력한다고 알고 있어서 사용해보았는데 바로 풀려서 pass..

```python
a, b, c = map(int, input().split())

print(pow(a, b, c))
```

## 문제번호: 9663(N-Queen)
- [문제링크](https://www.acmicpc.net/problem/9663)
- [깃허브](https://github.com/sksk713/PS/blob/master/6%EC%A3%BC%EC%B0%A8/9663.py)

### 풀이

