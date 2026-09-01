<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: A Nandha      </h3>
<h3>Register Number: 212225040271   </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

``````
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

``````

<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'F', 'G', 'I', 'J']


<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'E', 'D', 'G']

## code:
```py
from collections import defaultdict

H_dist = {}

def aStarAlgo(start_node, stop_node):
    open_set = set(start_node)
    closed_set = set()

    g = {}               
    parents = {}         

    g[start_node] = 0
    parents[start_node] = start_node

    while len(open_set) > 0:
        n = None

        
        for v in open_set:
            if n is None or g[v] + heuristic(v) < g[n] + heuristic(n):
                n = v

       
        if n is None:
            print("Path does not exist!")
            return None

        
        if n == stop_node:
            path = []
            while parents[n] != n:
                path.append(n)
                n = parents[n]
            path.append(start_node)
            path.reverse()

            print('Path found:', path)
            return path

        
        for (m, weight) in get_neighbors(n):

            if m not in open_set and m not in closed_set:
                open_set.add(m)
                parents[m] = n
                g[m] = g[n] + weight

            else:
                if g[m] > g[n] + weight:
                    g[m] = g[n] + weight
                    parents[m] = n

                    if m in closed_set:
                        closed_set.remove(m)
                        open_set.add(m)

        
        open_set.remove(n)
        closed_set.add(n)

    print("Path does not exist!")
    return None



def get_neighbors(v):
    """
    Retrieves neighbors of node 'v' from Graph_nodes dictionary.
    Returns list of (neighbor, cost) pairs.
    """
    return Graph_nodes[v]


def heuristic(n):
    return H_dist[n]



graph = defaultdict(list)

n, e = map(int, input("Enter number of nodes and edges (e.g., '10 14'): ").split())     # number of nodes, number of edges

for i in range(e):
    u, v, cost = map(str, input(f"Enter edge {i+1}/{e} (u v cost, e.g., 'A B 6'): ").split())
    cost = float(cost)
    graph[u].append((v, cost))
    graph[v].append((u, cost))       

for i in range(n):
    node, h = map(str, input(f"Enter heuristic for node {i+1}/{n} (e.g., 'A 10'): ").split())
    H_dist[node] = float(h)

print("Heuristics:", H_dist)

Graph_nodes = graph
print("Graph:", graph)


aStarAlgo('S', 'G')
```

## output:
<img width="1466" height="396" alt="image" src="https://github.com/user-attachments/assets/c6b7312a-65a7-444f-98bf-112f09391b2a" />

## Result:
Implement A* search algorithm for a Graph executed successfully.
