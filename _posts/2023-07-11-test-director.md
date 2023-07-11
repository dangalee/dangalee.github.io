---
layout: post
title: <백준 13458> 시험 감독
subtitle: Long 타입을 활용하기
tags: [java, problem-solving]
---
[출처: https://www.acmicpc.net/problem/13458]

총 N개의 시험장이 있고, 각각의 시험장마다 응시자들이 있다. i번 시험장에 있는 응시자의 수는 Ai명이다.

감독관은 총감독관과 부감독관으로 두 종류가 있다. 총감독관은 한 시험장에서 감시할 수 있는 응시자의 수가 B명이고, 부감독관은 한 시험장에서 감시할 수 있는 응시자의 수가 C명이다.

각각의 시험장에 총감독관은 반드시 1명 있어야 하고, 부감독관은 여러 명 있어도 된다.

각 시험장마다 응시생들을 모두 감시해야 한다. 이때, 필요한 감독관 수의 최솟값을 구하는 프로그램을 작성하시오.

<p>&nbsp;</p>

**문제의 조건**  

첫째 줄에 시험장의 개수 N(1 ≤ N ≤ 1,000,000)이 주어진다.

둘째 줄에는 각 시험장에 있는 응시자의 수 Ai (1 ≤ Ai ≤ 1,000,000)가 주어진다.

셋째 줄에는 B와 C가 주어진다. (1 ≤ B, C ≤ 1,000,000)

<p>&nbsp;</p>

**문제 주요 특징**

1. **long타입을 반드시 이용해야 한다.** \
JAVA TYPES, 특히 Int 정수 범위와 Long 정수 범위에 대해 알지 못하면 절대 이 문제를 풀 수 없다.\
시험장의 개수가 100만개이며,각 시험장 응시자 수가 모두 100만명이라면?\
이 와중에 한 감독관이 한 명씩만을 감독할 수 있나면?\
총 100만 * 100만 = 1,000,000,000,000 명의 감독관이 필요할 것이다.\
int타입은 이 값을 포함할 수 없다.

2. **범위가 크기 때문에 시간 단축을 위해서는 for문 사용을 최소화 해야 한다.** \
HashMap을 활용하여 중복된 값을 또 계산하지 않도록 설계했다.

<p>&nbsp;</p>

**JAVA TYPE (Primitive)**

| Type   | 설명               |
| :------ |:----------------------------------------------------------------------- |
| int | 정수 타입, -2,147,483,648  ... +2,147,483,648| 
| byte | 정수 타입, -128 ... 127 | 
| short | 정수 타입, -32768 ... 32767 | 
| long | 정수 타입, -9,223,372,036,854,775,808 ... 9,223,372,036,854,775,808| 


<p>&nbsp;</p>

**정답 코드**

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Map;
import java.util.StringTokenizer;
import java.io.IOException;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map.*;


class Main{

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        long N = Long.parseLong(br.readLine()); //시험장의 개수
        StringTokenizer st = new StringTokenizer(br.readLine(), " ");
        HashMap<String, Long> count = new HashMap<>(); //key: 응시자 수, val: 해당 응시자 수인 시험장 수

        for (long i = 0; i < N; i++) {
            //입력값을 읽으며, count HashMap업데이트
            String j = st.nextToken();
            if (count.containsKey(j)) {
                count.put(j, count.get(j) + 1);
            }
            else{
                count.put(j, Long.valueOf(1));
            }
        }
        StringTokenizer st2 = new StringTokenizer(br.readLine(), " ");
        long D = Long.parseLong(st2.nextToken()); //B, 총감독관
        long d = Long.parseLong(st2.nextToken()); //C, 부감독관

        long answer = 0;
       
        Iterator<Entry<String, Long>> iter = count.entrySet().iterator();
        while (iter.hasNext()){
            Map.Entry<String, Long> en = iter.next();
            String key = en.getKey();
            long val = en.getValue();
             //총 감독관 1명씩은 반드시 필요하다.
            long temp = 1;
            long _key = Long.parseLong(key) - D;

            if (_key > 0){ //아직 감독관이 더 필요한 경우에만 한하여, 
                temp += (_key / d);
                if ((_key % d) > 0) { //부감독관 수로 나누어서 필요한 감독관 수를 구한다.
                    temp += 1;  
                }
            }
            answer += (temp * (long) val);

        }
        System.out.println(answer);

    }
}
```