---
id: week4
title: 4주차
---

# PS 4주차

## 문제번호: 18870(좌표 압축)
- [문제링크](https://www.acmicpc.net/problem/18870)
- [깃허브](https://github.com/sksk713/PS/blob/master/4%EC%A3%BC%EC%B0%A8/18870.java)

### 풀이
1. 좌표가 들어있는 배열을 두개 만든다
2. 하나의 배열 좌표를 일단 정렬한다.
3. 좌표를 정렬한 후에 Index 0부터 순회하면서 해당 값의 인덱스값이 좌표를 압축한 값이 된다.
    - 정렬했으므로 앞에 있는 숫자 개수가 인덱스가 되므로
4. HashMap을 이용하여 해당 값과 Index값을 `put`
5. 정렬 되지 않은 배열에서 앞에서부터 순회하며 해당 값의 index를 불러온다
6. StringBuilder를 선언해서 한번에 출력해야 한다.
    - for문으로 하나하나 출력하면 시간초과 뜸.

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static HashMap<Integer, Integer> map = new HashMap<>();
    static int[] answer;

    public static void main(String[] args) throws IOException {
        int n = Integer.parseInt(br.readLine());
        int[] arr = new int[n];
        answer = new int[n];

        st = new StringTokenizer(br.readLine(), " ");

        for(int i = 0; i < n; i++){
            arr[i] = Integer.parseInt(st.nextToken());
            answer[i] = arr[i];
        }

        solution(arr);
    }

    static void solution(int[] arr){
        Arrays.sort(arr);
        int pivot = Integer.MAX_VALUE;
        int index = 0;
        for(int i = 0; i < arr.length; i++){
            if(pivot != arr[i]){
                map.put(arr[i], index++);
                pivot = arr[i];
            }
        }
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < answer.length; i++){
            sb.append(map.get(answer[i]) + " ");
        }
        System.out.println(sb);
    }
}
```

## 문제번호: 7576(토마토)
- [문제링크](https://www.acmicpc.net/problem/7576)
- [깃허브](https://github.com/sksk713/PS/blob/master/4%EC%A3%BC%EC%B0%A8/7576.java)

### 풀이

1. BFS로 접근
2. 토마토가 있는 지점부터 큐에 넣고 다음 좌표들은 이전 좌표에 + 1을 해준다.
    - 0인지 아닌지 체크하는 이유는 토마토가 있는 지점이 여러개 일 수 있기 때문에 가운데 지점에서 만남
3. 배열을 순회하면서 최대값을 구한다.
    - 처음 1에서 시작했기 때문에 1빼준다.

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static int[][] arr;
    static Queue<Point> qu = new LinkedList<>();
    static int[] dx = {1, -1, 0, 0};
    static int[] dy = {0, 0, 1, -1};

    public static void main(String[] args) throws IOException {
        st = new StringTokenizer(br.readLine(), " ");
        int x = Integer.parseInt(st.nextToken());
        int y = Integer.parseInt(st.nextToken());

        arr = new int[y][x];

        for (int i = 0; i < y; i++) {
            st = new StringTokenizer(br.readLine(), " ");
            for (int j = 0; j < x; j++) {
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        System.out.println(BFS(arr));


    }

    static int BFS(int[][] arr) {
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[0].length; j++) {
                if (arr[i][j] == 1) {
                    qu.add(new Point(i, j));
                }
            }
        }
        while (!qu.isEmpty()) {
            Point point = qu.poll();
            for (int i = 0; i < 4; i++) {
                int nextx = point.x + dx[i];
                int nexty = point.y + dy[i];

                if (nextx >= arr.length || nextx < 0 || nexty >= arr[0].length || nexty < 0 || arr[nextx][nexty] != 0) {
                    continue;
                }
                arr[nextx][nexty] = arr[point.x][point.y] + 1;
                qu.add(new Point(nextx, nexty));
            }
        }

        int max = Integer.MIN_VALUE;
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[0].length; j++) {
                if (arr[i][j] == 0) {
                    return -1;
                }
                if (arr[i][j] > max) {
                    max = arr[i][j];
                }
            }
        }
        return max - 1;
    }
}

class Point {
    int x;
    int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

## 문제번호: 2606(바이러스)
- [문제링크](https://www.acmicpc.net/problem/2606)
- [깃허브](https://github.com/sksk713/PS/blob/master/4%EC%A3%BC%EC%B0%A8/2606.java)

### 풀이
1. BFS를 이용한다 - 큐 이용
2. 1번 컴퓨터와 연결된 컴퓨터의 개수만 구하면 되므로 1번만 순회하면 된다.

배열 크기 주의

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static int[][] map;
    static boolean[] check;
    static int cnt = 0;

    public static void main(String[] args) throws IOException{
        int n = Integer.parseInt(br.readLine());
        int m = Integer.parseInt(br.readLine());

        map = new int[n+1][n+1];
        check = new boolean[n+1];

        for(int i = 0; i < m; i++){
            st = new StringTokenizer(br.readLine(), " ");
            int x = Integer.parseInt(st.nextToken());
            int y = Integer.parseInt(st.nextToken());

            map[x][y] = 1;
            map[y][x] = 1;
        }

        System.out.println(solution());
    }

    static int solution(){
        Queue<Integer> qu = new LinkedList<>();
        check[1] = true;
        qu.add(1);

        while(!qu.isEmpty()){
            int x = qu.poll();

            for(int i = 1; i < map.length; i++){
                if(map[x][i] == 1 && !check[i]){
                    check[i] = true;
                    qu.add(i);
                    cnt++;
                }
            }
        }
        return cnt;
    }
}
```