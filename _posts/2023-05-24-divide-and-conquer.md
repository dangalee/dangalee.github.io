---
layout: post
title: Merge sort (분할 정렬)
subtitle: divide-and-conquer
tags: [algorithm, divide-and-conquer , sorting]
---

- 정수를 merge sort를 사용하여 O(nlogn)의 시간복잡도로 정렬할 수 있습니다.
- 분할 정복은 주로 recursion을 사용하여 구현할 수 있습니다
- 주어진 array를 반으로 쪼갠 후, 그 각각을 recursion을 통해 정렬합니다.
- merge과정을 통해 정렬된 각각의 조각들을 합쳐줍니다.

##### O(nlogn)

분할: O(1) \
정렬: 2 * 분할 정복의 시간복잡도 \
결합: Linear number of comparison O(n)

따라서, T(n) = 2T(n/2) + O(n)이 됩니다.
분할 정복은 트리 형식으로 표현이 가능하며, 이때 트리의 높이는 logn이 됩니다.
위 식T(n) 을 트리 높이 만큼 진행시키면, 시간복잡도는 O(nlogn)이 됩니다. 

$$T(n) = 2T$$ ($$n\over2$$) $$ + cn$$
$$= 2(2T$$ ($$n\over 4$$) $$ + cn) + cn = 4T$$ ($$n\over4$$) $$ + 2cn$$\
:\
$$= 2^kT$$ ($$n\over2^k$$) $$ + kcn$$\
:\
k에 logn대입\
$$= nT(1) + cnlogn = O(nlogn)$$



##### Algorithm

##### JAVA로 구현
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