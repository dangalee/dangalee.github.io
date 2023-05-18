---
layout: post
title: Dijkstra
subtitle: Directed Graph에 대하여 Shortest path 구하기
tags: [algorithm, union-find, graph, non-cyclic]
---

최단거리를 greedy principal로 구하는 다익스트라 알고리즘은 **edge가 모두 0 이상일 때만 사용가능하다.**\
다익스트라 알고리즘에서, 한번 선택된 node는 visited에 합류하게 된다. \
그리고 visited에 합류하면, 끝이다. 다시 그 노드에 대한 최소거리를 구하지 않는다.




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
다만, 우선순위 큐를 이용해서 개선 가능 O(ElogV)
- Each vertex can be connected to (V-1) vertices. V-1 = E
- Priority Queue에서 put(), get() 은 O(log n)의 시간복잡도를 지닌다.

#### Python Implementation

```

Vertices = ['A', 'B', 'C', 'D', 'E', 'F', 'G']

distance = dict()
visited = []

#adjacancy matrix for undirected weighed graph
G = [[0, 2, 3, 3, 0, 0, 0],
     [2, 0, 4, 0, 3, 0, 0],
     [3, 4, 0, 5, 1, 6, 0],
     [3, 0, 5, 0, 0, 7, 0],
     [0, 3, 1, 0, 0, 8, 0],
     [0, 0, 6, 7, 8, 0, 9],
     [0, 0, 0, 0, 0, 9, 0]]

#pick any initial node, assume 'A' as initial node here
distance['A'] = 0
visited.append('A')

while visited != Vertices:
        adjvertices = [(G[v], v) for v in range(0, len(vertices)) if vertices[v] not in visited]
        for i in adjvertices:
            temp_d = float('inf')
            for j in range(0, len(i)):
                if i[0][j] > 0 and Vertices[j] in visited:
                    if temp_d > distance[Vertices[j]] + i[0][j]:
                        temp_d = distance[Vertices[j]] + i[0][j]
            distance[Vertices(i[1])] = temp_d
            visited.append(Vertices(i[1]))
            temp_d = float('inf')

print(distance)



        
```