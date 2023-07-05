---
layout: post
title: 최빈값 구하기
subtitle: 문제의 조건에 따라 줄어들 수 있는 코드 길이
tags: [java, python, problem-solving]
---
[출처: https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV13zo1KAAACFAYh]


어느 고등학교에서 실시한 1000명의 수학 성적을 토대로 통계 자료를 만들려고 한다.

이때, 이 학교에서는 최빈수를 이용하여 학생들의 평균 수준을 짐작하는데, 여기서 최빈수는 특정 자료에서 가장 여러 번 나타나는 값을 의미한다.

다음과 같은 수 분포가 있으면,

10, 8, 7, 2, 2, 4, 8, 8, 8, 9, 5, 5, 3

최빈수는 8이 된다.

최빈수를 출력하는 프로그램을 작성하여라 (단, 최빈수가 여러 개 일 때에는 가장 큰 점수를 출력하라).

**풀이**  
1. Hashmap(dictionary)를 이용한 풀이. \
점수는 key, 점수 빈도는 value로 저장한다. 이 후 iterator를 사용하여 최빈값을 찾아낼 수 있다.

2. 점수의 범위가 0~ 100, 학생 수가 1000명인 것을 활용\
점수의 범위가 0~ 100인 것을 이용하여, list comprehension을 이용하여 [0, 0 ... 0] 빈 리스트를 만들었다. 점수는 index가 되고, index의 값은 빈도이다.\
문제에서 주어진 조건을 잘 활용하므로서 더 짧은 길이의 코드를 작성할 수 있다.

**팁**  
1. Scanner 클래스의 메소드 nextInt()다음에 nextLine()을 사용할 경우, 정수 뒤의 \n이 같이 읽힐 수 있다.\
사이에 추가적인 nextLine() 메소드를 불러들여 \n을 제외하고 자료를 읽을 수 있다.

2. Map 컬렉션에는 직접적으로 iterator를 사용할 수 없다.\ entrySet() 메소드를 이용하여 set 객체를 반환받은 뒤 iterator 인터페이스를 적용할 수 있다.\
Map.Entry는 키와 값을 동시에 하나의 class에 저장한다. 따라서 키와 값이 둘 다 필요한 경우 유용하게 사용할 수 있다.
```java
for (String key: dictMap.keySet()) {
    System.out.println(key); //key만 반환
}

for (Map.Entry<String, String> entry: dictMap.entrySet()) {
    String k = entry.getKey();
    String v = entry.getValue();
}
```


#### Java 풀이
```java
import java.util.Scanner;
import java.util.Map;
import java.util.Map.Entry;
import java.util.HashMap;
import java.util.Iterator;
 
class Solution
{
    public static void main(String args[]) throws Exception
    {
        Scanner sc = new Scanner(System.in);
        int T;
        T=sc.nextInt();
        
 
        for(int test_case = 1; test_case <= T; test_case++)
        {
            sc.nextInt(); //skip one
            sc.nextLine(); // skip new line character
            HashMap<Integer, Integer> dict = new HashMap<Integer, Integer>();
            String numbers = sc.nextLine();
            String[] splited = numbers.split(" ");
            for (int i = 0; i < splited.length; i++) {
                Integer v = Integer.valueOf(splited[i]);
                if (dict.containsKey(v)){
                    dict.put(v, dict.get(v) +1);
                }
                else{
                    dict.put(v, 1);
                }
            }
            int answer = 0;
            int max = 0;
            Iterator<Entry<Integer, Integer>> iter = dict.entrySet().iterator();
            while(iter.hasNext()){
                Map.Entry<Integer, Integer> en = iter.next();
                if (en.getValue() > max) {
                    answer = en.getKey();
                    max = en.getValue();
                }
                if (en.getValue() == max) {
                    if (answer < en.getKey()){
                        answer = en.getKey();
                    }
                }
            }
             
            System.out.print("#" + test_case + " ");
            System.out.println(answer);
        }
    }
}
```

##### Python 풀이
```py
#학생의 수가 1000명이라는 정보
#점수의 범위가 0~100이라는 정보를 이용
 
t = int(input())
 
for i in range(1, t+1):
    input() #하나 스킵
    scores = list(map(int, input().split()))
    dic = [0 for _ in range(101)]
    for j in range(0, 1000):
        dic[scores[j]] = dic[scores[j]] + 1
    score = 0
    maximum = 0
    for k in range(0, 101):
        if (dic[k] > maximum):
            score = k
            maximum = dic[k]
        elif (dic[k] == maximum):
            score = k
    print("#%d %d" % (i, score))
```

