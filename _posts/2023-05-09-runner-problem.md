---
layout: post
title: 달리기 경주
subtitle: 딕셔너리와 시간복잡도
tags: [Programming, python, problem-solving]
---
[출처: 프로그래머스 https://school.programmers.co.kr/]

얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.

선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 players와 해설진이 부른 이름을 담은 문자열 배열 callings가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

시간복잡도 최대 O(n) 내에서 문제 풀기.
문제 풀이에서 시간 복잡도 제한이 있는 경우 Hash map을 이용하여 시간을 단축할 수 있다.

##### Python Dictionary
1. immutable, unordered
2. declare 
```
d = {}
d = dict()
d = dict("a" = 5, "b" = 6, "c" = 7)
```
3. list of lists 나 tuple of lists를 dict으로 변형가능
```
dict([["a", 5], ["b", 6]])
#{'a': 5, 'b': 6}
```
4. For 문 **Unordered, 순서임의**
```
for key in d: #key값 출력
for val in d.values: #value값 출력
for key, val in d.items(): #key와 value동시 출력
```
5. 값 추가, 값 삭제, 값 변형
```
d[key] = value #추가 및 변형
del d[key] #값 삭제
```

#### Dictionary 시간복잡도 vs List 시간복잡도

| Code | Time complexity |
| :----- |:---------------- |
| len(d) | O(1) | 
| d[key]| O(1) | 
| d[key] = value | O(1) | 
| key in d | O(1) | 

<p>&nbsp;</p>

| Code | Time complexity |
| :----- |:----------------- |
| len(lst) | O(1) | 
| lst[i] | O(1) | 
| lst[i:j] | O(슬라이스의 길이) | 
| i in lst | O(n) | 
| lst.index(i) | O(n) |
| lst.append(elem) | O(1) |
| lst.pop() | O(1) |
| lst.pop(0) | O(n) |
| lst.sort() | O(nlogn) |
| min(lst), max(lst) | O(n) |
| lst.revers() | O(n) |

이렇듯, 딕셔너리 이용을 통해 시간을 훨씬 단축시킬 수 있다. \
이 문제에 대한 나의 풀이: \
key: index, value: name인 딕셔더리 d와 \
key: name, value: index인 딕셔너리 dr을 선언하고 \
callings에 있는 이름들에 대하여, 바로 앞 선수와 index 교체 후
두 딕셔너리에 반영해 주었다. 
```
def solution(players, callings):
    answer = []
    d = dict()
    dr = dict()
    
    for i in range(len(players)):
        answer.append("")
        d[i] = players[i] # 3: kai
        dr[players[i]] = i # kai: 3
    for j in callings:
        dr[d[dr[j]-1]] += 1
        d[dr[d[dr[j]-1]]] = d[dr[j]-1]
        dr[j] -= 1 
        d[dr[j]] =j
        
    for k in dr.keys():
        answer[dr[k]] = k
        
            
    return answer
```
