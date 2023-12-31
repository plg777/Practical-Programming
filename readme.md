# Floyd Warshall Algorithm
### to obtain the shortest path algorithm between two nodes of a graph

INF=float("inf")
G = [[0, 7, INF, 8],
     [INF, 0, 5, INF],
     [INF, INF, 0, 2],
     [INF, INF, INF, 0]]
nV=len(G[0])



def floyd_recursive(distance, start_node, end_node, intermediate):
    if intermediate == nV:
        return distance[start_node][end_node]
    
    direct_distance = distance[start_node][end_node]
    through_intermediate_distance = (
        floyd_recursive(distance, start_node, end_node, intermediate + 1),
        floyd_recursive(distance, start_node, intermediate, intermediate + 1) +
        floyd_recursive(distance, intermediate, end_node, intermediate + 1)
    )
    
    return min(direct_distance, min(through_intermediate_distance))

def compute_shortest_paths(distance):
    shortest_paths = [[0] * nV for _ in range(nV)]
    
    for start_node in range(nV):
        for end_node in range(nV):
            shortest_paths[start_node][end_node] = floyd_recursive(distance, start_node, end_node, 0)
    
    return shortest_paths

result = compute_shortest_paths(G)
for row in result:
    print(row)


Check Requirements File [here](./requirements.txt)