---
layout: post
title: 시저 암호
subtitle: Ascii Value, Type Casting
tags: [java, problem-solving]
---

목표: Python이외에 Java 언어를 사용하여 코딩 테스트 연습하기.\
[출처: 프로그래머스 https://school.programmers.co.kr/]


어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

제한 조건\
공백은 아무리 밀어도 공백입니다.\
s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.\
s의 길이는 8000이하입니다.\
n은 1 이상, 25이하인 자연수입니다.

##### JAVA 로 풀이
- ASCII VALUE를 활용한다.
![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/dd/ASCII-Table.svg/2522px-ASCII-Table.svg.png)

ASCII 아스키코드란, American Standard Code for Information Interchange의 약자로, 문자를 숫자로 표현할 수 있도록 하는 약속이다.

- Java 내의 String.charAt(index)를 활용하면 char값을 얻을 수 있다.
- 또한 이 char값은 해당되는 Ascii 정수값으로 변환될 수 있다. 
- Java의 타입캐스팅은 크게 widening casting과 narrowing casting이 있다.
- 범위가 적은 타입으로부터 큰 타입으로 변환 시 widening casting을 사용할 수 있다. (byte -> short -> char -> int -> long -> float -> double)
- 반면, 범위가 큰 타입으로부터 적은 타입으로 변환 시 narrowing casting을 사용한다. (double -> float -> long -> int -> char -> short -> byte)
- double myDouble = myInt 또는 int asciValue = myChar은 widening casting의 예시다.
- int myInt = (int) myDouble 또는 char c = (char) asciValue는 narrowing casting의 예시다.
- 이외에도 Integer.valueOf, Double.valueOf, Float.valueOf, Integer.valueOf, String.valueOf와 같은 메소드를 통해 특정 객체형으로 값을 변환해 줄 수 있다.
- parseInt(string, radix) 메소드는 숫자로 변환할 string과 진법(이진법, 십진법 등)을 입력받아 string을 숫자로 변환한다.

```java
class Solution {
    public static String solution(String s, int n) {
        String answer = "";
        int[] before = new int[s.length()];
        for (int i = 0; i < s.length(); i++){
            int ascVal = s.charAt(i); //widening casting
            before[i] = ascVal;
        }
        int[] after = new int[s.length()];
        for (int i = 0; i < s.length(); i++){
            if (before[i] > 64 && before[i] < 91){
                //large letter
                if ((before[i] + n) < 91) {
                    after[i] = before[i] + n;
                }
                else {
                    after[i] = before[i] + n - 26;
                }

            }
            else if (before[i] > 96 && before[i] < 123){
                if ((before[i] + n) < 123) {
                    after[i] = before[i] + n;
                }
                else {
                    after[i] = before[i] + n - 26;
                }
            }
            else {
                //공백
                after[i] = before[i];
            }

        }

        for (int elem: after){
            char c = (char) elem; //narrow casting
            answer += String.valueOf(c);
        }
        return answer;
    }
}
```