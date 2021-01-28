---
id: pstip01
title: 📄 자바 입출력/메소드
---

## 입출력
- Scanner 대신 메모리 관리가 용이한 BufferedReader를 사용하자.

입력:
```
case 1
N // 테스트 케이스
XYZ // 입력값
```

```java
public static void main(String[] args) throws IOException{
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    int N = Integer.parseInt(br.readLine()); // 개수 입력

    String str = br.readLine();

    for(int i = 0; i < N; i++){
        System.out.println(str.charAt(i)); // '0' 빼주면 int 형
    }
    
}
```

입력:
```
case 2
N // 테스트 케이스
X Y Z // 입력값
```
```java
public static void main(String[] args) throws IOException{
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    int N = Integer.parseInt(br.readLine()); // 개수 입력

    StringTokenizer st = new StringTokenizer(br.readLine(), " ");
    
    for(int i = 0; i < N; i++){
        System.out.println(st.nextToken());
    }
}
```

입력:
```
case 3
N // 테스트 케이스
C R // 행 열
X Y Z // 첫번째 행
A B C // 두번째 행
```
```java
public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        int N = Integer.parseInt(br.readLine()); // 개수 입력
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");

        int C = Integer.parseInt(st.nextToken());
        int R = Integer.parseInt(st.nextToken());

        int[][] map = new int[C][R];

        for(int i = 0; i < C; i++){
            st = new StringTokenizer(br.readLine(), " ");

            for(int j = 0; j < R; j++){
                map[i][j] = Integer.parseInt(st.nextToken());
            }
        }

        for(int i = 0; i < C; i++){
            for(int j = 0; j < R; j++){
                System.out.print(map[i][j]);
            }
            System.out.println();
        }
    }
```
## 메소드

```java
배열
int[] arr = new int[]; //배열선언
char[] chararr = {'a', 'b', 'c'};
int[] intarr = {1, 2, 3};

Arrays.sort(arr); // 오름차순 정렬
Arrays.sort(arr, Collections.reverseOrder()); // 내림차순 정렬

String str = Arrays.toString(intarr); // int[] 문자열로 변환
String str2 = String.valueof(chararr); // char 문자열로 변환
Char[] chararr2 = str2.toCharArray(str); // 문자열 char[]로 변환


문자열

StringBuilder sb = new StringBuilder(); //문자열 선언
sb.trim();
sb.charAt(i); // 해당 인덱스 문자 가져올때 사용 !!!
sb.length();
sb.capacity();
sb.append();
sb.insert(index, " ");
sb.delete();
sb.replace(fromidx, toidx, " ");
sb.reverse();
sb.toString();

값 비교는 == 문자열 비교는 .equals("")메소드 사용한다.
```
### Arraylist
- Arraylist는 가변적으로 변하는 선형 리스트

```java
선언
Arraylist<타입> 이름 = new Arraylist<타입>();

메소드
.add(value)
.add(value, index);
.remove(index) // 앞으로 하나씩 알아서 땡겨짐
.clear() // 리스트 완전히 비우기
.size() // 리스트 크기 구하기
.get(index) // 해당 index 값 가져오기
.contains(index) // true or false
.indexof(index) // index or -1

```

- Char -> int로
```java
int x = Character.getNumericValue(s.charAt(i));
```