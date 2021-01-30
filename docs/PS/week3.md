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

## 문제번호: 1463(1로 만들기)
- [문제링크](https://www.acmicpc.net/problem/1463)
- [깃허브](https://github.com/sksk713/PS/blob/master/3%EC%A3%BC%EC%B0%A8/1463.java)

### 풀이
1. Bottom-up 방식으로 접근
2. dp[4]부터 전 인덱스에 1씩 더해주면서 배열을 만든다
    - 만약 dp 인덱스가 3으로 나누어지고 `해당인덱스 / 3의 인덱스 + 1` 이 dp[해당인덱스] 보다 작다면 최소값을 갱신해준다.
    - 만약 dp 인덱스가 2로 나누어지고 `해당인덱스/ 2의 인덱스 + 1` 이 dp[해당인덱스]보다 작다면 최소값을 갱신해준다.


```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static int[] dp;

    public static void main(String[] args) throws IOException {
        int n = Integer.parseInt(br.readLine());
        dp = new int[1000001];
        dp[0] = 0;
        dp[1] = 0;
        dp[2] = 1;
        dp[3] = 1;

        System.out.println(solution(n));
    }

    static int solution(int n) {
        for (int i = 4; i <= n; i++) {
            dp[i] = dp[i - 1] + 1;
            if (i % 3 == 0 && dp[i] > dp[i/3] + 1) {
                dp[i] = dp[i / 3] + 1;
            }
            if (i % 2 == 0 && dp[i] > dp[i/2] + 1) {
                dp[i] = dp[i / 2] + 1;
            }
        }
        return dp[n];
    }
}
```

## 문제번호: 1697(숨바꼭질)
- [문제링크](https://www.acmicpc.net/problem/1697)
- [깃허브](https://github.com/sksk713/PS/blob/master/3%EC%A3%BC%EC%B0%A8/1697.java)

### 풀이
1. BFS 를 이용한다 -QUEUE
2. 시작점에서 갈 수 있는 다음 단계는 3가지가 존재하며 다음 단계는 이전 단계 + 1을 해준다.
3. QUEUE에 목적지가 들어올때까지 계속 채워준다.

- Arrayoutofindex때문에 엄청난 시간낭비를 했다. 예외를 잘 생각해보자.

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static Queue<Integer> q = new LinkedList<Integer>();
    static int[] visit = new int[100001];
    static int answer;

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine(), " ");
        int x = Integer.parseInt(st.nextToken());
        int y = Integer.parseInt(st.nextToken());

        BFS(x, y);
        System.out.println(answer);
    }

    static void BFS(int x, int y) {
        q.add(x);
        visit[x] = 0;

        while (!q.isEmpty()) {
            int num = q.poll();
            if (num == y) {
                break;
            }
            if (num - 1 >= 0 && visit[num - 1] == 0) {
                visit[num - 1] = visit[num] + 1;
                q.add(num - 1);
            }
            if (num + 1 < 100000 && visit[num + 1] == 0) {
                visit[num + 1] = visit[num] + 1;
                q.add(num + 1);
            }
            if (num * 2 <= 100000 && visit[num * 2] == 0) {
                visit[num * 2] = visit[num] + 1;
                q.add(num * 2);
            }
        }
        answer = visit[y];
    }
}
```

## 문제번호: 1931(회의실 배정)
- [문제링크](https://www.acmicpc.net/problem/1931)
- [깃허브](https://github.com/sksk713/PS/blob/master/3%EC%A3%BC%EC%B0%A8/1931.java)

### 풀이
- 시간복잡도가 O(n^2)이 되면 시간초과가 발생한다

1. 시작시간과 끝나는 시간중 끝나는 시간을 기준으로 정렬을 한다.
    - 아무리 일찍 시작해도 끝나는 시간이 뒤면 손해임
2. 끝나는 시간을 기준으로 정렬이 끝난후에 만약에 끝나는 시간이 동일한 경우
    - `3시에 시작해서 3시`에 끝낼 수 있는 일 / `2시에 시작해서 3시`에 끝낼 수 있는 일 이 있다고 할때 입력을 `3 3`이 먼저 `pivot`에 들어가면 `2 3`은 그냥 통과된다.
    - 따라서 끝나는 시간이 동일한 경우에는 시작 시간에 맞춰 정렬을 해주어야 한다.
3. 한번의 반복문동안 cnt를 통해 최대값을 출력한다.

- Comparator 활용 숙지하기.

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static ArrayList<time> arr = new ArrayList<>();
    static int cnt = 0;
    static int pivot;

    public static void main(String[] args) throws IOException {
        int n = Integer.parseInt(br.readLine());
        for(int i = 0; i < n; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            arr.add(new time(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())));
        }

        System.out.println(solution(n));
    }

    static int solution(int n){
        Collections.sort(arr, new Comparator<time>() {
            @Override
            public int compare(time o1, time o2) {
                if(o1.y == o2.y){
                    return o1.x > o2.x ? 1 : -1;
                }

                return o1.y > o2.y ? 1 : -1;
            }
        });

        pivot = 0;

        for(int i = 0; i < n; i++){
            if(pivot <= arr.get(i).x){
                pivot = arr.get(i).y;
                cnt++;
            }
        }
        return cnt;
    }

    static class time{
        int x;
        int y;

        public time(int x, int y){
            this.x = x;
            this.y = y;
        }
    }
}
```