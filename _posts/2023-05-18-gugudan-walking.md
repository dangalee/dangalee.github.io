---
layout: post
title: 구구단 걷기
subtitle: 약수를 이용하여 문제 풀기 [math.sqrt()]
tags: [Programming, python, problem-solving]
---
[출처: SW Expert Academy https://swexpertacademy.com/main/main.do]
당신은 무한히 많은 행과 열이 있는 곱셈표 위에 서 있다. (i, j)셀에는 정수 ixj 가 적혀 있다. \(만약 행과 열이 9개라면 이는 구구단 표와 동일하다.) 현재 당신의 위치는 셀 (1, 1) 이다.

당신은 곱셈표의 오른쪽이나 아래쪽 방향으로 이동할 수 있다. 즉, 당신이 (i, j)에 서 있다면, (i+1, j)나 (i, j+1)로 이동할 수 있다.

정수 N이 주어질 때, N이 적혀 있는 어떤 셀에 도착하기 위해서 최소 몇 번 움직여야 하는가?


처음에 생각해 낸 방식: N x N 테이블 범위 내에서 나오는 i*j의 최솟 거리를 구하려고 했다.\
Dictionary를 만든 뒤, nested for loop을 사용하여 도착하는 모든 값에 대하여 dictionary[i*j] 를 제일 작은 값으로 업데이트. --> 문제에서 찾아야 하는 것은 'N'값만 이므로 너무 오랜 시간이 소요되여 runtime error로 실패.

수정한 방식: 결국 i*j = N에서 i와 j는 N의 약수일 수 밖에 없다. N의 첫번째 약수의 범위는 **1부터 루트 N**까지 밖에 될 수 없고. 이에 따라 두번째 약수는 N 나누기 첫번째 약수가 될 수 밖에 없다.
구해지는 모든 첫번째 약수(i) 그리고 두번째 약수 (j) 에 대한 최소 거리[(i-1) + (j-1)]를 return하였다.

```
import math
 
T = int(input())
# 여러개의 테스트 케이스가 주어지므로, 각각을 처리합니다.
for test_case in range(1, T + 1):
    # ///////////////////////////////////////////////////////////////////////////////////
    goal = int(input())
    shortest = float('inf')
    #어차피 곱해서 goal을 얻기 위해서는 goal의 약수를 이용해야 한다.
    # math.sqrt(goal)보다 작거나 같은 수를 기준으로 increment하며 최소 거리를 구한다.
    for i in range(1, int(math.sqrt(goal)) + 1):
        if goal % i == 0:
            x = goal // i
            y = i
            distance = (x - 1) + (y-1)
            if distance < shortest:
                shortest = distance
    print(f"#{test_case}", shortest)
```