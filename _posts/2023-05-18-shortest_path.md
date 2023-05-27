---
layout: post
title: Dijkstra
subtitle: Directed Graph에 대하여 Shortest path 구하기
tags: [algorithm, directed-graph, greedy, undirected-graph]
---


다익스트라 알고리즘은 그리디 원리를 사용한다.
다익스트라 알고리즘을 이용하여 시작점으로부터 각 노드까지의 최단 거리를 구할 수 있다.

다익스트라 알고리즘은 **edge가 모두 0 이상일 때만 사용가능하다.** \
다익스트라 알고리즘에서, 한번 선택된 node는 visited에 합류하게 된다. \
그리고 visited에 합류하면, 끝이다. 다시 그 노드에 대한 최소거리를 구하지 않는다.

사실 다익스트라와 Prim's 알고리즘은 상당히 유사하다. 둘 다 우선순위 큐가 비지 않은 상태에서\
가장 우선 순위인 vertex를 dequeue하고,\
다익스트라는 시작점으로부터 인접 노드까지의 최소거리를 distance dictionary에 업데이트.\
Prims는 인접 노드를 방문하는 최소 edge값을 업데이트하는 알고리즘이다.



#### 알고리즘

<pre>
Let V be the set of visited nodes 
      For each u ∈ V, we store a distance d(u)  
Initially V = {s} and d(s) = 0
while V ≠ all vertices: 
        select a node u ∉ V with at least one edge from V 
            where d'(u) = mininum d(n ∈ V) + edge , as small as possible 
        add u to V and define d(u) = d'(u)
End while
</pre>

#### Time Complexity
O(v^2), v = vertices
다만, 우선순위 큐를 이용해서 개선 가능하다. O(ElogV)
- Each vertex can be connected to (V-1) vertices. V-1 = E
- Priority Queue에서 enqueue() 후 재정렬 하는데 log(V)

#### Python Implementation [우선순위 큐 활용]

```
from queue import PriorityQueue
Vertices = ['A', 'B', 'C', 'D', 'E', 'F', 'G']
VIndex = {'A': 0, 'B': 1, 'C': 2, 'D': 3, 'E': 4, 'F': 5, 'G': 6}
distance = dict()
visited = []
#adjacancy matrix for undirected weighed graph
G = [[0, 2, 3, 3, 0, 0, 0],
     [2, 0, 4, 0, 3, 0, 0],
     [3, 4, 0, 5, 1, 6, 0]]
while H.empty() == False: #while priority queue is not empty
    current = H.get()[1] #visited and removed

    visited.append(VIndex[current])
    currentList = G[VIndex[current]]

    #exclude visited nodes
    adjNodes = [d for d in range(len(currentList)) if currentList[d] > 0] #for every connected node from current

    for n in adjNodes: #find the cheapest cost
        if n not in visited:
            if distance[Vertices[n]] > distance[current] + currentList[n]:
                distance[Vertices[n]] = distance[current] + currentList[n]

                H1 = PriorityQueue()
                for k, v in distance.items():
                    if VIndex[k] not in visited:
                        H1.put((v, k))
                H = H1
print(distance)
print(visited)


        
```