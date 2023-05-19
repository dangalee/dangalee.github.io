---
layout: post
title: Queue
subtitle: Prim's algorithm
tags: [algorithm, queue, undirected-graph, greedy, non-cyclic]
---
##### Queue
자료구조의 형태 중 하나인 Queue는 FIFO[First in first out]를 따른다. 따라서 dequeue() 사용시 front 또는 head위치의 element를 꺼낸다. enqueue()는 반대로 queue의 rear 또는 tail 위치에 element를 집어 넣게 된다.

##### linear data structure, Queue의 장단점
**[장점]**\
여러 데이터를 쉽게 관리할 수 있다.\
Insertion and deletion을 Fifo 규칙에 따라 수행한다\
놀이동산 순서, 식당 줄과 같이 특성 서비스에서 사용 시 유용하다\
다른 알고리즘, 자료구조에 활용된다.

**[단점]**\
가운데에 있는 element들의 경우 insertion과 deletion에 많은 시간이 소요된다.\
searching은 O(n)의 시간이 소요된다. \
queue의 최대 크기를 미리 지정해주어야 한다. 즉, If queue is full, we cannot enqueue the element. If queue is empty, we cannot dequeue the element.

##### 우선순위 큐 [Priority Queue] 
Queue의 한 형태인 우선순위 큐는 모든 elements에 우선순위 값이 지정되어 있다. 따라서, enqueue()시, 우선순위 값이 높은 경우 큐의 앞쪽에 배치된다. Priority queue 구성 시 array, linkedlist, heap 또는 binary search tree를 사용할 수 있다.

Priority Queue의 특징 [출처: https://www.geeksforgeeks.org/priority-queue-set-1-introduction/]
- Every item has a priority associated with it. 
- An element with high priority is dequeued before an element  with low priority. 
- If two elements have the same priority, they are served according to their order in the queue.

##### Implementation [Queue]
**Java**
```
import java.util.Queue;
import java.util.LinkedList;
public class Main {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<Integer>();
        int e = 123;

        queue.add(e);
        //Inserts element into this queue if possible. return true upon success
        // and throw IllegalStateException if no space is available

        queue.element(); //retrieve but does not remove the head
        queue.peek(); // retrieve, but does not remove the head, return null if the queue is empty
        queue.remove(); // retrieve and remove the head
        queue.poll(); // retrieve and remove the head. return null if the queue is empty
        queue.clear(); // remove everything
        // superinterface: collection<E>, Iterable<E> 따라서 더 많은 method 사용가능
        // addAll, clear, contains, containsAll, equals, hashCode, isEmpty, 
        // iterator, parallelStream, remove, removeAll, removeIf, 
        // retainAll, size, spliterator, stream, toArray, toArray
        // forEach 
}}
```
<p>&nbsp;</p>
Python 
: list, Collections.deque, queue.Queue 사용가능

- list.
built-in data structure, 편리하나 front element의 insertion과 deletion에 O(n)의 시간이 걸리므로 비효율적이다. enqueue에 append(), dequeue에 pop(0)사용. pop(0) 는 O(n)
- collection.deque  
더 빠른 dequeue와 enqueue, O(1)
```
from collections import deque
queue = deque()
queue.append('a') #deque(['a'])
print(queue.popleft()) # 'a' , deque([])
```
- queue.Queue
파이썬의 모듈 중 하나인 Queue사용. queue.Queue(maxsize)
queue.Queue(0) = infinite queue
```
from queue import Queue
queue = Queue(maxsize = 2)
print(queue.qsize()) #current size: 0
queue.put('a')
print(queue.full()) #return true if full. false
print(queue.get()) #'a', dequeue and remove
print(queue.empty()) #return true if empty. true
```

##### Implementation [Priority Queue]
```
from queue import PriorityQueue
queue = PriorityQueue(maxsize = 2)
queue.put(4)
queue.put(1)
print(queue.get()) #1
print(queue.get()) #4

queue.put((3, 'a'))
queue.put((1, 'b'))
print(queue.get()[1]) #'b'
```
put(), get() 은 O(log n)의 시간복잡도를 지닌다.

##### 위 Priority Queue를 이용하여 Prim's algorithm을 구성해보기
Prim's algorithm은 greedy의 원칙을 따르며,
input으로 connected undirected graph을 입력 할 시, MST(Minimum spanning tree)를 출력하는 알고리즘이다.

시작은 임의의 vertice를 골라 visited 리스트에 추가해준다.
모든 vertice에 대해 최초의 costs는 inf이다.
시작 vertice의 cost를 0으로 지정한다.
while priority queue != empty:
    v = priority queue에서 가장 우선순위인 vertice
    set v as visited
    v 와 인접한 node들에 대해 (단, visited 제외),
    각각의 거리를 구해, priority queue를 업데이트한다. 

시간복잡도: 모든 vertices를 queue에 cost = inf로 추가 (O(n)), 
priority queue의 insertion은 O(log m)의 시간복잡도를 지닌다.
인접한 node들에 대하여 priority queue 업데이트 (O(nlogm))


Graph를 2d array로 표현하였기에, vertices에 해당하는 index값이 필요하여 dictionary를 추가하였다.

```
from queue import PriorityQueue
Vertices = ['A', 'B', 'C', 'D', 'E', 'F', 'G']
VIndex = {'A': 0, 'B': 1, 'C': 2, 'D': 3, 'E': 4, 'F': 5, 'G': 6}
cost = dict()
visited = []

#adjacancy matrix for undirected weighed graph
G = [[0, 2, 3, 3, 0, 0, 0],
     [2, 0, 4, 0, 3, 0, 0],
     [3, 4, 0, 5, 1, 6, 0],
     [3, 0, 5, 0, 0, 7, 0],
     [0, 3, 1, 0, 0, 8, 0],
     [0, 0, 6, 7, 8, 0, 9],
     [0, 0, 0, 0, 0, 9, 0]]
for v in Vertices:
    cost[v] = float('inf')

#pick any initial node, assume 'A' as initial node here
cost['A'] = 0

H = PriorityQueue()
for v in Vertices:
    H.put((cost[v], v))

while H.empty() == False:
    current = H.get()[1] #visited and removed

    visited.append(VIndex[current])
    currentList = G[VIndex[current]]

    #exclude visited nodes
    adjNodes = [d for d in range(len(currentList)) if currentList[d] > 0] #for every connected node from current

    for n in adjNodes: #find the cheapest cost, exclude visited nodes
        if n not in visited:
            if cost[Vertices[n]] > currentList[n]:
                cost[Vertices[n]] = currentList[n]
                #update priority queue, based on new cost
                H1 = PriorityQueue()
                for k, v in cost.items():
                    if VIndex[k] not in visited:
                        H1.put((v, k))
                H = H1
print(cost)
print(visited)

        
```