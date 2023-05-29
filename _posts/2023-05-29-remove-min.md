---
layout: post
title: 제일 작은 수 제거하기
subtitle: 자바와 친해지기
tags: [Programming, java, problem-solving]
---

목표: Python이외에 Java 언어를 사용하여 코딩 테스트 연습하기.\
[출처: 프로그래머스 https://school.programmers.co.kr/]

정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

제한 조건\
arr은 길이 1 이상인 배열입니다.\
인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.
(즉, arr내에 중복된 값은 없다.)

##### JAVA 로 풀이
- Double.POSITIVE_INFINITY 또는 Double.NEGATIVE_INFINITY;를 통해 무한대 값을 지정해 줄 수 있다.
- 문제를 풀면서 시도했던 여러 방법 중, sort()가 있었으나, 문제에서 정렬된 결과를 출력하면 에러가 나서 풀이를 수정하였다.
- Arrays.sort(arr) 사용사 Collections 라이브러리를 이용하여 내림차순 정렬도 가능하다. 
- 예시: Arrays.sort(arr, Collections.reverseOrder())
- 단, 이 때, collections.reverseOrder()는 Integer object에만 적용 가능하다. int 타입에 사용 시 에러가 발생한다.
- Arrays.copyOfRange(array, startIndex, endIndex)를 사용하여 array복사가 가능하다


```java
class Solution{
    public int[] solution(int[] arr) {
        int[] answer = {-1};
        double smallest = Double.POSITIVE_INFINITY;

        if (arr.length > 1) {
            for (int i = 0; i < arr.length; i++) {
                if (smallest > arr[i]) {
                    smallest = arr[i];
                }
            }
            answer = new int[arr.length -1];
            int index = 0;
            for (int elem: arr){
                if (elem != smallest){
                    answer[index] = elem;
                    index++;
                }
            }
        }
        return answer;
    }
}
```