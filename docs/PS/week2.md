---
id: week2
title: 2주차
---

# PS 2주차

## 문제번호: 1105(팔)
- [문제링크](https://www.acmicpc.net/problem/1105)
- [깃허브](https://github.com/sksk713/PS/blob/master/2%EC%A3%BC%EC%B0%A8/1105.java)


### 풀이
1. 자리수가 커지면 무조건 0이 된다.
    - 자리수가 커질때 생기는 100, 1000, 10000 ~~~~ 은 8이 없으므로
2. 두개의 수를 큰자리수부터 비교하며 같은지 확인한다.
    - 자리수의 숫자가 모두 다르거나 8이 없으면 8이 없어도 되므로 그냥 0이다.
3. 해당 자리수의 숫자가 다르면 중단한다.
    - 예를들어 819와 830라고 할때, 1과 3은 다르므로 자리수가 바뀔때`(820)` 8이 존재하지 않을 수 있다.
3. 해당 자리수의 숫자가 같으면 그 숫자가 8인지 확인하고 8이면 cnt 하나 올린다.
    - 예를들어 820과 835라고 할때, 앞자리 8은 바뀔 수 없고 2, 3은 `830`이 나올 수 있으므로 stop
    
```java
public class Main {
    static int cnt = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        String x = st.nextToken();
        String y = st.nextToken();

        System.out.println(solution(x, y));
    }
    static int solution(String x, String y){
        if(x.length() == y.length()) {
            for (int i = 0; i < x.length(); i++) {
                if(x.charAt(i) == y.charAt(i)){
                    if(x.charAt(i) == '8'){
                        cnt++;
                    }
                }
                else
                    break;
            }
        }
        return cnt;
    }
}
```

## 문제번호: 1092(배)
- [문제링크](https://www.acmicpc.net/problem/1092)
- [깃허브](https://github.com/sksk713/PS/blob/master/2%EC%A3%BC%EC%B0%A8/1092.java)


### 풀이

1. 배가 옮길 수 있는 무게, 박스의 무게를 역순으로 정렬한다.
2. 가장 큰 박스를 가장 큰 배에 못 실으면 -1 반환
3. 가장 큰 박스부터 가장 큰 배부터 싣는다.
4. 박스 idx, 배 idx 두 가지를 이용한다.
    - 만약 박스의 무게가 배보다 크면 박스 idx를 하나씩 늘려가면서 실을 수 있는지 확인
5. 배에 모두 실으면 cnt를 1올리고 다시 idx들을 초기화하고 실행
6. box에 요소가 다 없어지면 cnt 반환

```java
public class Main {
    static ArrayList<Integer> box = new ArrayList<Integer>();
    static ArrayList<Integer> ship = new ArrayList<Integer>();
    static int cnt = 0;

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int shipcnt = Integer.parseInt(br.readLine());
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        for (int i = 0; i < shipcnt; i++) {
            ship.add(Integer.parseInt(st.nextToken()));
        }
        int boxcnt = Integer.parseInt(br.readLine());
        st = new StringTokenizer(br.readLine(), " ");
        for (int i = 0; i < boxcnt; i++) {
            box.add(Integer.parseInt(st.nextToken()));
        }

        System.out.println(solution(shipcnt));

    }

    static int solution(int s) {
        Collections.sort(box);
        Collections.sort(ship);
        Collections.reverse(box);
        Collections.reverse(ship);

        if (box.get(0) > ship.get(0)) {
            return -1;
        }
        while (!box.isEmpty()) {
            int ship_idx = 0;
            int box_idx = 0;
            while (ship_idx < s) {
                if (ship.get(ship_idx) >= box.get(box_idx)) {
                    box.remove(box_idx);
                    ship_idx++;
                }
                else if (ship.get(ship_idx) < box.get(box_idx)) {
                    box_idx++;
                }
                if(box_idx == box.size()){
                    break;
                }
            }
            cnt++;
        }
        return cnt;
    }
}
```

## 문제번호: 1946(신입사원)
- [문제링크](https://www.acmicpc.net/problem/1946)
- [깃허브](https://github.com/sksk713/PS/blob/master/2%EC%A3%BC%EC%B0%A8/1946.java)


### 풀이
1. 시간 복잡도를 줄이기 위해 서류심사 성적을 오름차순으로 정렬을 한다.
    - (정렬 하는법 제대로 공부하기)
2. 서류심사의 성적이 정렬이 된 상태이기 때문에 2등 부터는 1등의 면접심사 등수보다 높아야 한다.
3. 최소값 변수를 하나 선언하고 1등의 면접심사 등수를 대입한다.(기준값)
4. 2등부터 면접심사 등수를 체크한다
    - 만약 최소값에 저장되어 있는 면접심사 등수보다 높다면 최솟값을 해당 등수 면접심사 등수로 바꾼다.
        - 뒤에 있는 등수 사람들은 서류심사 등수가 낮기때문에 면접은 무조건 높아야 한다. 따라서 최소값보다 항상 커야함.
    - 만약 최소값에 저장되어 있는 면접심사 등수보다 낮다면 해당 인원은 채용되지 않기 때문에 전체 인원에서 1감소


```java
public class Main {
    static ArrayList<point> arr;
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;

    public static void main(String[] args) throws IOException {
        int t = Integer.parseInt(br.readLine());
        for (int i = 0; i < t; i++) {
            int n = Integer.parseInt(br.readLine());
            arr = new ArrayList<point>();
            for (int j = 0; j < n; j++) {
                st = new StringTokenizer(br.readLine(), " ");
                arr.add(new point(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())));
            }
            System.out.println(solution(n));
        }
    }
    static int solution(int n){
        Collections.sort(arr, new Comparator<point>() {
            @Override
            public int compare(point o1, point o2) {
                return o1.x > o2.x ? 1 : -1;
            }
        });
        int cnt = arr.size();
        int min = arr.get(0).y;
        for(int i = 1; i < n; i++){
            if(min < arr.get(i).y){
                cnt--;
            }
            else
                min = arr.get(i).y;
        }

        return cnt;
    }
}
class point{
    int x;
    int y;

    public point(int x, int y){
        this.x = x;
        this.y = y;
    }
}
```

## 문제번호: 1263(시간관리)
- [문제링크](https://www.acmicpc.net/problem/1263)
- [깃허브](https://github.com/sksk713/PS/blob/master/2%EC%A3%BC%EC%B0%A8/1263.java)


### 풀이
1. 일단 가장 우선적으로 처리해야 할일부터 정렬한다.
2. 정렬 후에 임의의 i번 idx에서 끝내는 시간이 x_time이라면 0 ~ i까지의 인덱스들의 걸리는 시간의 합이 x_time을 넘어서는 안된다.
    - 넘는다면 애초에 해당 idx일은 할 수가 없는 일.
3. 가장 처음 해야할일의 걸리는 시간이 y_time 이라면 y_time까지 반복문을 돌려준다.
    - 여기서 2의 조건에 위배되는 사항이 있으면 -1을 반환한다.
    - 그렇지 않다면 해당 반복문의 idx가 답이된다.

- 중첩 반복문 나올때 flag를 이용하자.

```java
public class Main {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static ArrayList<Time> arr = new ArrayList<Time>();
    static int time = 0;
        public static void main(String[] args) throws IOException {
            int n = Integer.parseInt(br.readLine());
            for(int i = 0; i < n; i++) {
                st = new StringTokenizer(br.readLine(), " ");
                arr.add(new Time(Integer.parseInt(st.nextToken()), Integer.parseInt(st.nextToken())));
            }
            System.out.println(solution(n));
        }

        static int solution(int n){
            Collections.sort(arr, new Comparator<Time>() {
                @Override
                public int compare(Time o1, Time o2) {
                    return o1.si > o2.si ? 1 : -1;
                }
            });

            boolean flag = false;
            for(int i = 0; i <= arr.get(0).si; i++){
                int idx = 0;
                int sum = i;
                while(idx < n) {
                    sum += arr.get(idx).ti;
                    if (sum > arr.get(idx).si){
                        if(i == 0){
                            return -1;
                        }
                        flag = true;
                        break;
                    }
                    idx++;
                }
                if(flag == true){
                    break;
                }

                time = i;
            }
            return time;
        }
}

class Time{
    int ti;
    int si;

    public Time(int ti, int si){
        this.ti = ti;
        this.si = si;
    }
}
```

## 문제번호: 1068(트리)
- [문제링크](https://www.acmicpc.net/problem/1068)
- [깃허브](https://github.com/sksk713/PS/blob/master/2%EC%A3%BC%EC%B0%A8/1068.java)


### 풀이

- DFS, BFS 공부
- DFS 풀때 배열 선언 예시.
```java
ArrayList<Integer>[] tree = new ArrayList[개수];
```

1. 입력 받은 개수만큼 ArrayList 선언하고, 각각에 인덱스마다 인접노드를 저장한다.
    - 양방향 입력
    ```java
        - tree[i].add(parent);
        - tree[parent].add(i);
    ```
2. 재귀를 이용하여 DFS 방식으로 트리를 순회하며, 삭제 노드를 순회할 때 재귀 stop.
    - 마지막 leaf를 순회하게 되면 count 하나씩 증가시킨다.

- 실수 한 부분: index[0]이 무조건 root가 되는게 아님.
```java
public class boj_1068 {
    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static StringTokenizer st;
    static ArrayList<Integer>[] tree;
    static boolean[] isvisited;
    static int leaf_cnt = 0;
    static int root = 0;
    static int delete_idx = 0;

    public static void main(String[] args) throws IOException {
        int n = Integer.parseInt(br.readLine());
        isvisited = new boolean[n];
        tree = new ArrayList[n];
        for(int i = 0; i < n; i++) {
            tree[i] = new ArrayList<Integer>();
            isvisited[i] = false;
        }
        st = new StringTokenizer(br.readLine(), " ");
        for(int i = 0; i < n; i++){
            int parent = Integer.parseInt(st.nextToken());

            if(parent != -1) {
                tree[i].add(parent);
                tree[parent].add(i);
            }
            else root = i;
        }
        delete_idx = Integer.parseInt(br.readLine());

        if(delete_idx == root){
            System.out.println(0);
        }
        else{
            DFS(root);
            System.out.println(leaf_cnt);
        }
    }

    static void DFS(int node){
        isvisited[node] = true;
        boolean haschild = false;
        for(int i = 0; i < tree[node].size(); i++){
            if(tree[node].get(i) != delete_idx && !isvisited[tree[node].get(i)]) {
                haschild = true;
                DFS(tree[node].get(i));
            }
        }
        if(!haschild){
            leaf_cnt++;
        }
    }


}
```