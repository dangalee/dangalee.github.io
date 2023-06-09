---
layout: post
title: Heaps and Priority Queues
subtitle: 
tags: [queue, heaps, BST]
---
##### 우선순위 큐 [Priority Queue] 
큐의 한 형태인 우선순위 큐는 모든 노드에 우선순위 값이 지정되어 있다. 따라서, enqueue()시, 우선순위 값이 높은 경우 큐의 앞쪽에 배치된다. 우선순위 큐 구성 시 우리는 array, linkedlist, heap 또는 **binary search tree**를 사용할 수 있다.

**Priority Queue의 특징**
[출처: https://www.geeksforgeeks.org/priority-queue-set-1-introduction/]
- Every item has a priority associated with it. 
- An element with high priority is dequeued before an element  with low priority. 
- If two elements have the same priority, they are served according to their order in the queue.


MAX heap 또는 Min heap을 사용하여 우선순위 큐를 구성할 수 있다. \
이때, RemoveMax 또는 RemoveMin이 dequeue와 같다고 생각하면 된다 \
Heap의 높이는 log n + 1이기에 (n은 노드의 수, heap을 사용할 경우 항상 balanced tree!여서 좋다), removeMax에 걸리는 시간은 heap을 재정렬하는 시간, 즉 O(log n)이다. \
마찬가지로 insert에 걸리는 시간도 최대 O(log n)이다. \
따라서, heap을 구성하는데 걸리는 시간은 최대 n * O(log n)이 된다. 



#### HEAP 힙
##### Heap의 특징
1. Complete Binary Tree: 모든 자식(leaf) 노드는 왼쪽부터 채워져 있어야 한다. 즉, 맨 아래 트리 레벨에서 가장 오른쪽 노드가 존재하지 않을 수 있다.  \
* Array를 사용하여 complete binary tree를 나타낼 수 있다. 각 array 의 index는 다음과 같다 [출처: OpenDSA] \
![CompleteBinaryTree](https://opendsa-server.cs.vt.edu/ODSA/Books/Everything/html/_images/BinArray.png)

2.  Heap에 저장된 값들은 부분정렬되어있다. 각각의 노드와, 그 노드에 저장된 값 사이에는 어떠한 relationship이 존재한다. 

* relationship 1: Max Heap \
모든 노드는 자식 노드와 같거나 큰 값을 가져야 한다. Root 노드는 tree 내에서 가장 큰 값을 지닌다.
* relationship 2: Min Heap \
모든 노드는 자식 노드와 같거나 작은 값을 가진다. Root 노드는 tree 내에서 가장 작은 값을 지닌다.

<p>&nbsp;</p>
BST(Binary Search Tree)는 전체 정렬으로, 같은 레벨 노드(leaf)들 내에서도 왼쪽에 위치한 노드가 오른쪽에 위치한 노드보다 작은 값을 가져야 한다. 
Heap은 아무 상관 없으며, 오른쪽 leaf가 왼쪽 leaf보다 큰 값을 가질 수 있다.
