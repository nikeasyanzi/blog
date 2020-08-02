
# [10.Dynamic Programming ](/dynamic-programming.md)

# 847. Shortest Path Visiting All Nodes

https://leetcode.com/problems/shortest-path-visiting-all-nodes/description/

欠推導!!  

用數狀圖

1,

# BFS solution

```c
class Solution(object):
    def shortestPathLength(self, graph):
        N = len(graph)
        queue = collections.deque((1 << x, x) for x in xrange(N))
        dist = collections.defaultdict(lambda: N*N)
        for x in xrange(N): dist[1 << x, x] = 0
        #print(queue)
        while queue:
            print(dist)
            cover, head = queue.popleft()
            #print("cover=", cover," head=",head);
            d = dist[cover, head] # the distance of the current visited points to  head
            #print("cover= %d", cover);
            if cover == 2**N - 1: return d  # if we visited all points, the bit vector will be 2 ^(N-1)
            #print(graph[head])
            for child in graph[head]:   #check all the other points connected with head
                cover2 = cover | (1 << child)
                if d + 1 < dist[cover2, child]: # check if the distance decrease by add the child node
                    dist[cover2, child] = d + 1
                    queue.append((cover2, child))
                    #print(bin(cover2))
```		
								
# DP solution

```c
class Solution(object):
    def shortestPathLength(self, graph):
        N = len(graph)
        dist = [[float('inf')] * N for i in xrange(1 << N)]
        for x in xrange(N):
            dist[1<<x][x] = 0

        for cover in xrange(1 << N):
            repeat = True
            while repeat:
                repeat = False
                for head, d in enumerate(dist[cover]):
                    for nei in graph[head]:
                        cover2 = cover | (1 << nei)
                        if d + 1 < dist[cover2][nei]:
                            dist[cover2][nei] = d + 1
                            if cover == cover2:
                                repeat = True

        return min(dist[2**N - 1])
```				
				差不多意思
				
