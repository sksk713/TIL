---
id: week3
title: 3주차
---

# PS 3주차

## 문제번호: 1012(유기농 배추)
- [문제링크](https://www.acmicpc.net/problem/1012)
- [깃허브](https://github.com/sksk713/PS/blob/master/3%EC%A3%BC%EC%B0%A8/1012.java)

### 풀이
1. DFS를 이용해 지렁이가 있는 곳을 발견하면 DFS 호출
2. 좌표가 배열을 초과하지 않도록 예외를 선언해주고 지렁이가 없는곳도 그냥 PASS
3. 지렁이 있는곳을 지나가면 해당 좌표를 0으로 바꿔주고 계속 반복한다.
4. 하나의 덩어리가 끝나면 count 1증가 시킴

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static int[][] arr;
    static boolean[][] visited;
    static int x = 0;
    static int y = 0;
    static int[] dx = {-1, 1, 0, 0};
    static int[] dy = {0, 0, -1, 1};
    static int count = 0;

    public static void main(String[] args) throws IOException {
        int T = Integer.parseInt(br.readLine());
        for (int i = 0; i < T; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            x = Integer.parseInt(st.nextToken());
            y = Integer.parseInt(st.nextToken());
            int n = Integer.parseInt(st.nextToken());
            count = 0;
            arr = new int[y][x];
            for (int j = 0; j < n; j++) {
                st = new StringTokenizer(br.readLine(), " ");
                int a = Integer.parseInt(st.nextToken());
                int b = Integer.parseInt(st.nextToken());
                arr[b][a] = 1;
            }
            for (int k = 0; k < y; k++) {
                for (int l = 0; l < x; l++) {
                    if (arr[k][l] == 1) {
                        DFS(k, l);
                        count++;
                    }
                }
            }
            System.out.println(count);
        }
    }

    static void DFS(int X, int Y) {
        for (int i = 0; i < 4; i++) {
            int new_x = X + dx[i];
            int new_y = Y + dy[i];

            if (new_x < 0 || new_y < 0 || new_x >= y || new_y >= x) {
                continue;
            }
            if (arr[new_x][new_y] == 0) {
                continue;
            }

            arr[new_x][new_y] = 0;
            DFS(new_x, new_y);
        }
    }
}
```

## 문제번호: 1541(잃어버린 괄호)
- [문제링크](https://www.acmicpc.net/problem/1541)
- [깃허브](https://github.com/sksk713/PS/blob/master/3%EC%A3%BC%EC%B0%A8/1541.java)

### 풀이
1. -를 기준으로 뒤에 있는 수들의 합을 -로 묶어주면 최소값을 만들 수 있다.
2. 따라서 -를 기준으로 문자열을 일단 자른다.
3. -를 기준으로 자르면 - 사이에 숫자와 +연산자가 섞여있기 때문에 +연산자로 또 자른다.
4. +연산자로 자른 이후에 각각의 토큰을 더해준다
5. 첫번째항을 제외하고 뒤에 있는 항은 모두 -로 묶어주면 되기 때문에 첫번째 항은 양수 나머지 항은 음수로 한다.


```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static ArrayList<Integer> answer = new ArrayList<>();
    static int result = 0;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine(), "-");
        ArrayList<String> arr = new ArrayList<>();

        int i = 0;
        while(st.hasMoreTokens()){
            arr.add(st.nextToken());
            StringTokenizer str = new StringTokenizer(arr.get(i),"+");
            result = 0;
            while(str.hasMoreTokens()){
                result += Integer.parseInt(str.nextToken());
            }
            if(i == 0){
                answer.add(result);
            }
            else{
                answer.add(-(result));
            }
            i++;
        }
        int solution = 0;
        for(int x = 0; x < answer.size(); x++){
            solution += answer.get(x);
        }
        System.out.println(solution);

    }
}
```