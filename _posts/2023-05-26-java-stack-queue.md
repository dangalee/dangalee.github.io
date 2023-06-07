---
layout: post
title: 자바 Stack and Queue
# subtitle: 비고- bufferedReader, bufferedWriter
# cover-img: /assets/img/path.jpg
# thumbnail-img: /assets/img/thumb.png
# share-img: /assets/img/path.jpg
tags: [java, stack, queue]
---

목표: 자바 내에서 Stack과 Queue를 어떻게 사용하는 지 알아보자

##### Queue (FIFO) 사용법
자바에서 queue는 linkedlist를 활용하여 생성합니다.
```
import java.util.LinkedList;
import java.util.Queue;
Queue<Integer> q1 = new LinkedList<>();
```
<p>&nbsp;</p>

**Queue에 값을 추가하는 방법: Offer과 add** \
Offer와 add 모두 성공 여부에 따라 boolean 값을 출력합니다. \
그러나, add는 실패 시 IllegalStateException을 반환합니다.
```
q1.add(3); 
q1.offer(4);
```

**Queue 값을 삭제하는 방법: remove와 poll** \
remove와 poll모두 헤드값을 반환합니다. \
remove와 다르게 poll은 큐가 비었을 때 null을 반환합니다.
```
q1.poll();
q1.remove();
```

**Queue 비우는 법: clear**
```
q1.clear();  //초기화
```

**Queue 값을 반환하되, 삭제하지 않는 메서드: peek**\
poll과 유사하게 큐가 비었을 때 null을 반환합니다.
```
q1.peek();
```

<p>&nbsp;</p>

##### Stack (LIFO) 사용법
자바에서 지원하는 라이브러리 중 하나인 java.util을 import하여 Stack을 생성합니다.
```
import java.util.stack;
Stack<String> stack = new Stack<>();

```
Stack에 값 추가하는 방법: push\
Stack에서 값 삭제하는 방법: pop\
Stack에서 값을 참조하는 방법: peek\
Stack이 비었는지 확인하는 방법: empty\
Stack에서 값의 위치 반환하는 방법: search
```
    public static void main(String[] args) {
        Stack<Integer> s = new Stack();
        s.push(1);
        s.push(2);
        s.push(3);
        System.out.println(s.search(3)); //1을 반환
    }
```