---
layout: post
title:  "ShortestPath.md"
date:   2021-04-04 16:43:44 +0900
---

# Shortest Path <최단경로찾기>

---

– 주어진 가중치 그래프에서 어느 한 출발점에서 또 다른 도착점까지의 최단 경로를 찾는 문제이다.

​    

##  다익스트라(Dijkstra) 의 최단 경로 알고리즘

​    

* 단일 시작점 최단 경로 알고리즘
* 시작 정점 S에서 부터 다른 정점까지의 최단 거리를 계산

---

​    

## 다익스트라 알고리즘 동작 과정

​    

![이미지](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcofnIo%2FbtqEuY3ZsSW%2FTnQX9kZ9RpyYtvElsrkMz1%2Fimg.gif)

​    

---

​    

## Shortest Path(G,s)   

​    

> + 입력: 가중치 그래프 G=(V,E), (V)=n, (E)=m
>
> + 출력: 출발점 s로부터 (n-1)개의 점까지 각각 최단 거리를 저장한 배열 D
>
> ---
>
> ​    
>
> 1. 시작 정점 자신을 제외한 모든 정점까지의 거리를 무한대로 초기화한다.
> 2. 시작 정점을 우선순위 큐에 삽입한다.
> 3. 우선순위 큐에서 정점 하나를 꺼낸 후 해당 정점에서 갈 수 있는 모든 인접한 정점들을 확인한다.    
>    3-1. 인접 정점까지의 거리가 이미 기록된 해당 정점까지의 거리보다 더 짧다면 거리 값을 갱신한다.    
>    3-2. 이미 기록된 인접 정점까지의 거리가 더 짧다면 넘어간다.
> 4. 3-1에서 거리 값이 갱신된 정점들을 우선순위 큐에 삽입한다.
> 5. 우선순위 큐에 더 이상 정점이 없을 때까지 3~4번 과정을 반복한다.

---

​    

## 시간 복잡도

​    

### while-루프가 (n-1)번 반복되고, 1회 반복될 때

> – 최소의 D[v]를 가진 점 vmin을 찾는데 O(n) 시간이 걸린다.
>
> – vmin에 연결된 점의 수가 최대 (n-1)개이므로, 각 D[w]를 갱신하는데 걸리는 시간은 O(n)이다.
>
> ![수식](https://user-images.githubusercontent.com/80369791/113504812-8a5d1380-9575-11eb-8523-7cd908f519db.gif)    

---

# 소스코드

​    

### 시작 정점 방문 표시

```
distance[v] = 0;
        visit[v] = true;
```

​    

## distance 초기값 저장

```
 for(int i = 0; i<g.n; i++) {
            if(!visit[i] && g.weight[v][i] !=0){
                distance[i] = g.weight[v][i];
            }
        }
```

​    

## 모든 정점을 방문 하면서 최단 경로 찾기

```
for(int j = 0; j<g.n-1; j++){
            int min = Integer.MAX_VALUE;
            int min_pos = -1;

            //방문하지 않은 정점 중에서 최단 거리의 정점 고르기
            for(int i = 0; i<g.n; i++){
                if(distance[i] < min && !visit[i]){
                    min = distance[i]; // 최단 거리
                    min_pos = i; // 최단 거리의 인덱스(정점)
                }
            }

            visit[min_pos] = true; // 선택된 정점은 방문 표시해줌
            for(int i = 0; i<g.n; i++){
                if(!visit[i] && g.weight[min_pos][i]!=0) // 방문하지 않은 정점일 때만
                    if(distance[min_pos] + g.weight[min_pos][i] < distance[i]) // 선택된 정점을 통한 거리(distance 값)가 원래 거리보다 짧으면
                        distance[i] = distance[min_pos] + g.weight[min_pos][i]; // 인접 정점의 distance 값 업데이트
            }
        }
```

​    

## 최단 경로의 거리 출력

```
for(int i = 0; i<g.n; i++) {
            System.out.print(distance[i]+" ");
        }
```

​    

## Graph

```
private static class Graph {
        int n; // 정점의 개수
        int[][] weight; // 가중치
        public Graph(int n){
            this.n = n;
            weight = new int[n][n];
        }
        public void value(int i, int j, int w){
            weight[i][j] = w;
            weight[j][i] = w;
        }
    }
```

​    

## Main

```
public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        System.out.print("정점의 개수 : ");
        int n = scanner.nextInt();
        Graph g = new Graph(n);
        int edge = random.nextInt(5) + n;

        int num = 0;
        for(int i = 0; i<edge; i++) {
            int x = num;
            if(num>n-1){
                x = random.nextInt(n);
            }
            int y = random.nextInt(n);
            if(x == y){
                while(x==y){
                    y = random.nextInt(n);
                }
            }
            int z = random.nextInt(20) + 1;
            System.out.println(x+" "+y+" "+z);
            g.value(x,y,z);
            num++;
        }

        System.out.print("시작 정점 : ");
        int v = scanner.nextInt();
        dijkstra(g, v);
    }
```

​    

## 코드 설명

: 정점의 개수를 입력하면 그래프와 가중치를 랜덤으로 생성된다.    

시작 정점을 입력하면 최단 거리를 dijkstra함수를 통해 구한다.    

+ 입력 : 정점의 개수, 시작 정점    

- 출력 : 그래프, 최단 경로의 거리    

​    ![capture](https://postfiles.pstatic.net/MjAyMTA0MDRfMTQ2/MDAxNjE3NTI5NzExNTg5.AYELsbteeO_EXfzp9mbJ_wih8JABUs99bMDif3qJxAEg.KrYYCsXVMc4J0J6bFpA8Ve-EgRm54M8ShXOvp-_RTXog.PNG.hongsubakgame/image.png?type=w966)![capture](https://postfiles.pstatic.net/MjAyMTA0MDRfMTk2/MDAxNjE3NTMwMjY4MTMy.Ai4tldF-BwMHEXAx-7f8x5y5r39YzCazVwlViF5hTgYg.LtbRIRfUNJJ7p-q8qyXsdINz6VetUkWbs4HVg8MaWNYg.PNG.hongsubakgame/image.png?type=w966)





## 실행시간 측정

- 실행 전 시간과 실행 후 시간의 차이
```java
long beforeTime = System.currentTimeMillis();
        dijkstra(g, v);
        System.out.println();
        long afterTime = System.currentTimeMillis();
        long secDiffTime = (afterTime - beforeTime);
        System.out.println("시간차이 : "+secDiffTime);
```

