---
id: week1
title: 1주차
---

# PS 1주차

## 문제번호: 11047(동전 0)
- [문제링크](https://www.acmicpc.net/problem/11047)
- [깃허브](https://github.com/sksk713/PS/blob/master/1%EC%A3%BC%EC%B0%A8/11047.java)


### 풀이
1. 동전을 오름차순으로 입력하기 때문에 따로 정렬할 필요는 없다
2. 가장 큰 동전부터 탐색을 하며 K보다 작을 시에 해당 동전이 K원을 만들 수 있는 가장 큰 동전이다.
3. 입력 K원이 0원이 될때까지 빼주며 K보다 작은 동전이 발견될 시에 계속 cnt를 1씩 증가시킨다.

```java    
import java.util.Scanner;

class Main {
    public static void main(String[] args){
        Scanner stdin = new Scanner(System.in);
        
        int n = stdin.nextInt();
        int k = stdin.nextInt();
        int cnt = 0;
        
        int[] coin = new int[n];
        
        for(int i = 0; i < n; i++){
            coin[i] = stdin.nextInt();
        }
        
        for(int j = n - 1; j >= 0; j--){
            while(true){
                if(k >= coin[j]){
                    k -= coin[j];
                    cnt++;
                }
                else
                    break;
            }
        }
        System.out.print(cnt);
    }
}
```

## 문제번호: 1914(하노이 탑)
- [문제링크](https://www.acmicpc.net/problem/1914)
- [깃허브](https://github.com/sksk713/PS/blob/master/1%EC%A3%BC%EC%B0%A8/1914.java)

### 풀이(시간초과)
1. 재귀를 이용하여 풀이 N-1개의 원판을 첫번째에서 중간 기둥으로 옮긴다
2. 첫번째 기둥 맨아래 원판은 세번째 기둥으로 옮긴다.
3. 재귀를 이용하여 중간 기둥으로 옮겼던 N-1개의 원판을 세번째 기둥으로 옮긴다.

- 재귀
    - 원판이 2개일 시, 위에서 한개를 하나의 그룹으로 본다.
    - 원판이 3개일 시, 위에서 두개를 하나의 그룹으로 보면 위에서 두개를 옮기는 방법을 이용
    - 원판이 4개일 시, 위에서 세개를 하나의 그룹으로 보면 위에서 세개를 옮기는 방법을 이용
 

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class boj_1914 {
    static int cnt = 0;

    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        hanoi(N, 1, 3);
        System.out.println(cnt);
        if(N <= 20) {
            hanoi_print(N, 1, 3);
        }
    }

    static void hanoi(int n, int x, int y){
        if(n > 1){
            hanoi(n-1, x, 6 - x - y);
        }
        cnt += 1;
        if(n > 1){
            hanoi(n-1, 6 - x - y, y);
        }
    }
    static void hanoi_print(int n, int x, int y){
        if(n > 1){
            hanoi_print(n-1, x, 6 - x - y);
        }
        System.out.printf("%d %d\n",x, y);
        if(n > 1){
            hanoi_print(n-1, 6 - x - y, y);
        }
    }
}
```
- cnt = 2^N - 1인데 N을 100까지 표현하려면 시간초과가 뜬다.
- BigInteger를 이용해서 cnt 값을 출력한다. 

### 풀이수정
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
import java.math.BigInteger;

public class Main {

    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        BigInteger cnt = new BigInteger("2");
        cnt = cnt.pow(N);
        cnt = cnt.subtract(BigInteger.ONE);
        System.out.println(cnt);
        if(N <= 20) {
            hanoi_print(N, 1, 3);
        }
    }


    static void hanoi_print(int n, int x, int y){
        if(n > 1){
            hanoi_print(n-1, x, 6 - x - y);
        }
        System.out.println(x + " " + y);
        if(n > 1){
            hanoi_print(n-1, 6 - x - y, y);
        }
    }
}
```

## 문제번호: 1449(수리공 항승)
- [문제링크](https://www.acmicpc.net/problem/1449)
- [깃허브](https://github.com/sksk713/PS/blob/master/1%EC%A3%BC%EC%B0%A8/1449.java)

### 풀이
1. 구멍의 개수와 테이프의 길이를 입력한다.
2. 처음에 구멍의 개수에 맞게 테이프 칠을 하도록 cnt를 올린다.
3. 그 다음 테이프의 길이와 구멍 사이의 길이를 체크
    1. 구멍을 먼저 오름차순으로 정렬 `Arrays.sort()`
    2. 그 다음 가장 첫 구멍을 값에 저장한 다음, 뒤에 있는 값들과 비교
    3. `뒤 구멍 - 앞 구멍 + 1`이 테이프의 길이보다 짧으면 cnt 1을 빼준다. (테이프 하나로 막을 수 있으므로)
    4. 그 다음 뒤에있는 구멍과도 비교를 해서 그 길이가 테이프 길이보다 크다면 index를 해당 구멍부터 시작하도록 옮겨준다.
    
```java
import java.util.Arrays;
import java.util.Scanner;

import static java.lang.Math.abs;

public class boj_1449{
    public static Scanner stdin = new Scanner(System.in);
    static int cnt;

    public static void main(String[] args){
        int n = stdin.nextInt();
        int l = stdin.nextInt();

        int[] hole = new int[n];
        for(int i = 0; i < n; i++){
            hole[i] = stdin.nextInt();
        }

        System.out.println(solution(hole, l));

    }
    static int solution(int[] hole, int l) {
        Arrays.sort(hole);
        int a = hole[0];
        cnt = hole.length;

        for(int i = 1; i < hole.length; i++){
            if((abs(a - hole[i]) + 1 <= l)){
                cnt--;
            }
            else {
                a = hole[i];
            }
        }
        return cnt;
    }
}
```

## 문제번호: 1080(행렬)
- [문제링크](https://www.acmicpc.net/problem/1080)
- [깃허브](https://github.com/sksk713/PS/blob/master/1%EC%A3%BC%EC%B0%A8/1080.java)

### 풀이
1. 3x3의 행렬을 한꺼번에 뒤집기 때문에 만약 크기가 6x6인 행렬이라면 index 0 ~ 3 을 확인하고 4부터는 확인할 필요가 없다.
2. 따라서 `index 0 ~ index N - 3` 까지만 확인을 해주면 된다.
3. `index 0 ~ index N - 3` 에서 행렬a와 행렬b의 값이 다르면 해당 인덱스로부터 3x3 만큼 reverse 한다.
4. reverse 과정이 끝난 후에 행렬a와 행렬b가 동일한지 확인을 해야한다.
    - 6x6에서 index 0 ~ 3까지 확인하고 reverse를 수행한 후에, index 4와 index 5가 행렬끼리 서로 다르다면 이 연산으로는 같은 행렬이 될 수 없음을 의미한다.


```java
public class Main {
    static int n;
    static int m;
    static int cnt = 0;
    static int[][] a;
    static int[][] b;

    public static void main(String[] args) {
        Scanner stdin = new Scanner(System.in);

        n = stdin.nextInt();
        m = stdin.nextInt();

        a = new int[n][m];
        b = new int[n][m];

        for (int i = 0; i < n; i++) {
            String str = stdin.next();
            for (int j = 0; j < m; j++) {
                a[i][j] = str.charAt(j) - '0';
            }
        }
        for (int i = 0; i < n; i++) {
            String str = stdin.next();
            for (int j = 0; j < m; j++) {
                b[i][j] = str.charAt(j) - '0';
            }
        }
        System.out.println(solution());
    }

    static void reverse(int x, int y) {
        for (int i = x; i < x + 3; i++) {
            for (int j = y; j < y + 3; j++) {
                if (a[i][j] == 1) {
                    a[i][j] = 0;
                }
                else {
                    a[i][j] = 1;
                }

            }
        }
    }

    static int solution(){
        for (int i = 0; i < n - 2; i++) {
            for (int j = 0; j < m - 2; j++) {
                if (a[i][j] != b[i][j]) {
                    reverse(i, j);
                    cnt++;
                }
            }
        }
        for (int i = 0 ; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (a[i][j] != b[i][j]) {
                    return -1;
                }
            }
        }

        return cnt;
    }
}
```
## 문제번호: 1174(줄어드는 숫자)
- [문제링크](https://www.acmicpc.net/problem/1174)
- [깃허브](https://github.com/sksk713/PS/blob/master/1%EC%A3%BC%EC%B0%A8/1174.java)

Arraylist, collection 공부하기

### 풀이
- 최고로 큰 줄어드는 숫자인 987654321은 `2^N-1번째` 이므로 index 1024부터는 -1을 출력
- 987654321은 `int`타입으로는 표현할 수 없기 때문에 `long`타입 사용

1. 0 ~ 9 는 줄어드는 숫자이므로 0 ~ 9로 시작하며 재귀를 이용한다
2. 만약 `solution(5, 1, list)`가 실행된다면 list에 5, 50, 51, 510, 52, 520, 521, 5210, 53, 530, 531, 5310, 532, 5320, 5321, 53210 ...... 이 재귀적으로 계속 추가된다
    - 일의자리 수보다 작은 숫자들이 뒤로 계속 붙게됨
3. 자릿수가 10자리가 되면 `list`를 리턴한다
4. 현재 `list`에 존재하는 요소들은 정렬되지 않는 상태이므로 정렬시킨다.
5. 0이 제일 가장 작은 첫번째 줄어드는 숫자이므로 0번 index에 0이 저장되어 있으므로 1번 인덱스부터 출력되게 한다. 

```java
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int T = Integer.parseInt(br.readLine());
        ArrayList<Integer> list = new ArrayList<>();

        for(int num = 0; num < 10; num++) {
            solution(num, 1, list);
        }
        Collections.sort(list);

        if(T > 1023){
            System.out.println(-1);
        }
        else {
            System.out.println(list.get(T - 1));
        }
    }

    static ArrayList solution(long num, int digit, ArrayList list){
        if(digit > 10){
            return list;
        }
        list.add(num);
        for(int i = 0; i < 10; i++){
            if(num % 10 > i){
                solution(num * 10 + i, digit + 1, list);
            }
        }
        return list;
    }
}
```