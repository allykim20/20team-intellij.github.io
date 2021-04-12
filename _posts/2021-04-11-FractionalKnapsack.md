---
layout: post
title:  "FractionalKnapsack.md"
date:   2021-04-11 11:43:44 +0900
---

# 배낭(Knapsack) 문제

> 담을 수 있는 최대 무게가 정해진 배낭과 함께 각각의 무게와 가치가 주어진 아이템의 집합이 주어졌을 때,    배낭에 담은 아이템들의 가치의 합이 최대가 되도록 하는 아이템들의 부분집합을 찾는 문제이다.
> + 위의 내용을 간단한 그림으로 나타내면 다음과 같다:

![](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fd/Knapsack.svg/375px-Knapsack.svg.png)

> 배낭에 담을 수 있는, 정해진 최댓값에 맞춰 일정 가치와 무게가 있는 짐들을 배낭에 넣을 때, 가치의 합이 최대가 되도록 짐을 고르는 방법을 찾는다.

​    

---

​    

## 부분 배낭 (Fractional Knapsack) 문제

> –물건을 부분적으로 담는 것을 허용
>
> –그리디 알고리즘으로 해결

​    

---

​    

## 0-1 배낭 문제 (0/1 배낭 문제)
 
 ![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FITqjC%2FbtqCrjQKeFT%2FcY9kKEb3jQnkZgRjFxmss1%2Fimg.png)
(*물건을 부분적으로 배낭에 넣을 수 없다) 
 
> –부분 배낭 문제의 원형으로 물건을 통째로 배낭에 넣어야 한다.
> 
> –부분 배낭 문제와 모든 조건이 같으나, 물건을 부분적으로 배낭에 넣을 수 없다.
>
> –그리디 알고리즘으로 해결할 수 없으며, 동적 계획 알고리즘, 백트래킹(Backtracking) 기법, 분기 한정 기법(Branch-and-Bound)으로 해결
> 
> –최소의 비용으로 자원을 할당하는 문제

​    

---

​    

## 부분배낭 문제

> + 부분 배낭 문제에서는 물건을 부분적으로 배낭에 담을 수 있으므로,     
>
>   최적해를 위해서 ‘욕심을 내어’ 단위 무게 당 가장 값나가는 물건을 배낭에 넣고,    
>
>   계속해서 그 다음으로 값나가는 물건을 넣는다.
> + 그런데 만일 그 다음으로 값나가는 물건을 ‘통째로’ 배낭에 넣을 수 없게 되면,     
>
>   배낭에 넣을 수 있을 만큼만 물건을 부분적으로 배낭에 담는다.

​    

---

​    

## 알고리즘

> 입력: n개의 물건, 각 물건의 무게와 가치, 배낭의 용량 capacity
>
> 출력: 배낭에 담은 물건 리스트 iVal과 배낭에 담은 물건 가치의 합 totalValue

> 1. 각 물건에 대해 단위 무게 당 가치를 계산한다.
>2. 물건들을 단위 무게 당 가치를 기준으로 내림차순으로 정렬하고, 정렬된 물건 리스트를 ItemValue 라고 하자.
> 3. iVal=∅, wt=0, totalValue=0 iVal은 배낭에 담을 물건 리스트,    (3-1) wt는 배낭에 담긴 물건들의 무게의 합, totalValue는 배낭에 담긴 물건들의 가치의 
>4. ItemValue에서 단위 무게 당 가치가 가장 큰 물건 x를 가져온다.
> 5. while ( (wt+x의 무게) ≤ capacity ) { 
>6. x를 iVal에 추가시킨다.
> 7. wt = wt+x의 무게
>8. totalValue = curVal+x의 가치
> 9. x를 ItemValue에서 제거한다.
>10. ItemValue에서 단위 무게 당 가치가 가장 큰 물건 x를 가져온다. }
> 11. if ((capacity-wt) > 0) { // 배낭에 물건을 부분적으로 담을 여유가 있으면 
>12. 물건 x를 (capacity-wt)만큼만 iVal에 추가한다.
> 13. totalValue = totalValue +(capacity-wt)만큼의 x의 가치 }
>14. return iVal, totalValue

​    

## 수행과정

> + 다음 그림과 같은 4개의 물건이 있고, 배낭의 최대 용량은 50(KG)이다.
>
> <img src="https://user-images.githubusercontent.com/80369791/114262191-8881cd00-9a19-11eb-9107-f533c192af47.PNG" alt="가방" style="zoom:80%;" />
>
> |             | 물건1 | 물건2 | 물건3 | 물건4 |
> | ----------- | ----- | ----- | ----- | ----- |
> | 무게(kg)    | 10    | 40    | 20    | 30    |
> | 가치(만원)  | 60    | 40    | 100   | 120   |
> | 무게당 가치 | 6     | 1     | 5     | 4     |
>
> + 먼저 물건 KG당 가치를 구한다음에 가장 가치가 높은 물건1을 배낭에 넣는다.
>
>   <img src="https://user-images.githubusercontent.com/80369791/114262192-8881cd00-9a19-11eb-83f1-fcc622fc0a6d.PNG" alt="가방 1" style="zoom:80%;" />
>
> + 그리고 나서 배낭에 남은 무게를 그 다음으로 무게당 가치가 높은 물건3을 넣는다.
>
>   <img src="https://user-images.githubusercontent.com/80369791/114262193-8881cd00-9a19-11eb-873e-7bc965ec3be2.PNG" alt="가방 2" style="zoom:80%;" />
>
> + 그리고 나서 배낭에 남은 무게를 그 다음으로 무게당 가치가 높은 물건4를 넣는데    물건이 다 들어갈 수 없으므로 물건4를 나눈다..
>
>   <img src="https://user-images.githubusercontent.com/80369791/114262190-8750a000-9a19-11eb-9ad8-6649d246260f.PNG" alt="가방 3" style="zoom:80%;" />
>
> + 나누어진 물건 4에서 배낭에 최대로 들어갈 수 있는 물건 4-1을 넣는다.
>
>   <img src="https://user-images.githubusercontent.com/80369791/114262196-8c155400-9a19-11eb-9403-e561d2d95e79.PNG" alt="가방 4" style="zoom:80%;" />
>
> + 배낭에 더 이상 들어갈 공간이 없으므로 현재 배낭에 들어 있는 현재 가치금액을 리턴한다.
>
>   ​    

---

   

## 시간 복잡도

> 알고리즘의 시간복잡도는 O(nlogn)이다.    
>
> 실제로 시간들을 보면 다르게 나온다.
>
> ``` 
> long start = System.currentTimeMillis();
> double maxValue = getMaxValue(wt, val, capacity);
>         System.out.println("총 용량의 가치 = "+ maxValue + "만원");
> long end = System.currentTimeMillis();
> System.out.println( "실행 시간 : " + ( end - start ));
> ```
>
> |             | 1개  | 10개  | 100개  |
> | ----------- | ---- | ----- | ------ |
> | 이론시간(s) | 0    | 33.21 | 664.38 |
> | 실제시간(s) | 0.04 | 2.7   | 17     |
>
> <img src="https://user-images.githubusercontent.com/80369791/114289591-2b872500-9ab4-11eb-8519-bf77fe28cfab.PNG" alt="그래프" style="zoom:80%;" />

​    

---

​    

## 소스코드

### main

```
public static void main(String[] args)
    {

        int[] wt = { 10, 40, 20, 30};
        int[] val = { 60, 40, 100, 120};
        int capacity = 50;

        double maxValue = getMaxValue(wt, val, capacity);

        // Function call
        System.out.println("총 용량의 가치 = "
                + maxValue + "만원");

    }
```

​    

### ItemValue

```
static class ItemValue {
        Double cost;
        double wt, val, ind;
		public ItemValue(int wt, int val, int ind)
        {
            this.wt = wt;
            this.val = val;
            this.ind = ind;
            cost = new Double((double)val / (double)wt);
        }
```

​    

### 배낭에 물건이 들어갈 수 있으면 넣고 아니면 나누어서 넣기

```
 for (ItemValue i : iVal) {

            int curWt = (int)i.wt;
            int curVal = (int)i.val;

            if (capacity - curWt >= 0) {
                // this weight can be picked while
                capacity = capacity - curWt;
                totalValue += curVal;
            }
            else {
                // item cant be picked whole
                double fraction
                        = ((double)capacity / (double)curWt);
                totalValue += (curVal * fraction);
                capacity
                        = (int)(capacity - (curWt * fraction));
                break;
            }
        }
```

​    

---

​    

## 결론

+ 배낭에 총 50KG이 들어가는데 물건1,물건3,물건4-1이 들어가는데    물건1(60만원) + 물건3(100만원) + 물건4-1(80만원)을 더하면 240만원이 나온다.

  ![결과](https://user-images.githubusercontent.com/80369791/114277215-441c1e80-9a65-11eb-8bf1-4330c033da39.PNG)
  
## 출처
  그림 위키피디아 https://en.wikipedia.org/wiki/Knapsack_problem
  티스토리 블로그 https://source-sc.tistory.com/26
  책 알기 쉬운 알고리즘, 생능출판사, 양성봉
