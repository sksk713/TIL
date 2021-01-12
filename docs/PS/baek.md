---
id: baek
title: 1주차
---

# PS 1주차

## 문제번호: 11407(동전 0)
- [문제링크](https://www.acmicpc.net/problem/11047)
- [깃허브](https://github.com/sksk713/PS/blob/master/1%EC%A3%BC%EC%B0%A8/11047.java)


`문제`
준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.

동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다. 이때 필요한 동전 개수의 최솟값을 구하는 프로그램을 작성하시오.

`입력`
첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)

둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)

`출력`
첫째 줄에 K원을 만드는데 필요한 동전 개수의 최솟값을 출력한다.

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

`문제`
세 개의 장대가 있고 첫 번째 장대에는 반경이 서로 다른 n개의 원판이 쌓여 있다. 각 원판은 반경이 큰 순서대로 쌓여있다. 이제 수도승들이 다음 규칙에 따라 첫 번째 장대에서 세 번째 장대로 옮기려 한다.

한 번에 한 개의 원판만을 다른 탑으로 옮길 수 있다.
쌓아 놓은 원판은 항상 위의 것이 아래의 것보다 작아야 한다.
이 작업을 수행하는데 필요한 이동 순서를 출력하는 프로그램을 작성하라. 단, 이동 횟수는 최소가 되어야 한다.

아래 그림은 원판이 5개인 경우의 예시이다.

`입력`
첫째 줄에 첫 번째 장대에 쌓인 원판의 개수 N (1 ≤ N ≤ 100)이 주어진다.

`출력`
첫째 줄에 옮긴 횟수 K를 출력한다.

N이 20 이하인 입력에 대해서는 두 번째 줄부터 수행 과정을 출력한다. 두 번째 줄부터 K개의 줄에 걸쳐 두 정수 A B를 빈칸을 사이에 두고 출력하는데, 이는 A번째 탑의 가장 위에 있는 원판을 B번째 탑의 가장 위로 옮긴다는 뜻이다. N이 20보다 큰 경우에는 과정은 출력할 필요가 없다.

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