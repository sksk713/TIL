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