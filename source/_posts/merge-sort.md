---
title: Merge Sort (합병 정렬)
date: 2024-01-05 15:15:36
tags:
---

#### Goal 💡
- Merge Sort란 무엇인가?
- Merge Sort를 Java로 구현하기
- Merge Sort의 시간복잡도 이해하기
- Merge Sort의 공간복잡도 이해하기


[1] Merge Sort란 무엇인가?

> In computer science, merge sort (also commonly spelled as mergesort) is an efficient, general-purpose, and comparison-based sorting algorithm. Most implementations produce a stable sort, which means that the relative order of equal elements is the same in the input and output. Merge sort is a divide-and-conquer algorithm that was invented by John von Neumann in 1945.
[출처: Wikipedia]

합병 정렬은 <span style='background-color:#f6f8fa'>비교</span>를 기반으로 한 정렬 방법입니다. 합병 정렬은 <span style='background-color:#f6f8fa'>Stable Sorting (안정 정렬) 알고리즘</span>에 속합니다. 1945년 John von Neumann이 개발했으며, <span style='background-color:#f6f8fa'>divide-and-conquer(분할 정복) 알고리즘</span>의 한 종류입니다.

[2] Merge Sort를 Java로 구현하기

Merge Sort (합병 정렬)을 구현하기 위해 두 개의 함수가 필요합니다. 

1. 분할 함수 (재귀, recursion)
주어진 입력값 (ex. 리스트)을 절반으로 분할한 뒤, 각각을 재귀 호출합니다. 이 때 base case는 더 이상 리스트를 쪼갤 수 없는 경우 (리스트의 길이 = 1)일 때입니다. 분할된 리스트는 결합 함수에 대입합니다.

2. 결합 함수
나누어진 두 개의 [], [] 리스트 내의 값들을 비교하여 하나의 리스트를 리턴합니다. 값을 비교하기 위해 인덱스 포인터를 사용합니다.

```java
import java.util.Arrays;


public class Main {


    public static int[] merged(int[] A, int[] B) {
        //comparison, merge
        int[] result = new int[A.length + B.length];
        int n1 = 0;
        int n2 = 0;
        int i = 0;
        while (n1 < A.length && n2 < B.length) {
            if (A[n1]< B[n2]){
                result[i] = A[n1];
                n1++;
            }
            else {
                result[i] = B[n2];
                n2++;
            }
            i++;
        }
        while (n1 < A.length) {
            result[i] = A[n1];
            n1++;
        }


        while (n2 < B.length) {
            result[i] = B[n2];
            n2++;
        }
        return result;
    }
    public static int[] mergesort(int[] lst) {
        int arrLen = lst.length;
        int[] result = lst;
        if (arrLen == 1){
            return lst;
        }
        else{
            //divide
            int half = arrLen / 2;
            int[] left = Arrays.copyOfRange(lst, 0, half);
            int[] right = Arrays.copyOfRange(lst, half, arrLen);
            int[] A = mergesort(left);
            int[] B = mergesort(right);
            result = merged(A, B);
        }
        return result;


    }




    public static void main(String[] args) {
        int[] complexArr = {5, 7, 4, 3, 2, 6, 8, 4, 2, 4, 2, 6, 1};
        int[] arr = {1, 2, 0, 4};
        int[] item = mergesort(complexArr);
        for (int  j = 0; j < item.length;  j++){
            System.out.print(item[j] + " ");
        }
    }
}
```
[3] Merge Sort의 시간복잡도 이해하기



분할: O(1) \
정렬: 2 * 분할 정복의 시간복잡도 \
결합: 선형 탐색 O(n)


따라서, T(n) = 2T(n/2) + O(n)이 됩니다.
분할 정복은 트리 형식으로 표현이 가능하며, 이때 트리의 높이는 logn이 됩니다.
위 식T(n) 을 트리 높이 만큼 진행시키면, 시간복잡도는 O(nlogn)이 됩니다.

[4] Merge Sort의 공간복잡도 이해하기

 int[] result = new int[A.length + B.length];
 두 개의 배열을 병합한 결과를 담아 둘 배열이 추가로 필요하기 때문에 O(n)의 추가 메모리를 요구합니다.
