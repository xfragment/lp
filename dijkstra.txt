import heapq

def dijkstra(graph, start):
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    queue = [(0, start)]
    
    while queue:
        current_distance, current_node = heapq.heappop(queue)
        
        # Ignore if we have already found a shorter path
        if current_distance > distances[current_node]:
            continue
        
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight
            
            # If a shorter path is found, update the distance and enqueue the neighbor
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(queue, (distance, neighbor))
    
    return distances


# Get user input to define the graph
def create_graph():
    graph = {}
    vertex_count = int(input("Enter the number of vertices: "))
    for i in range(vertex_count):
        vertex = input("Enter vertex: ")
        neighbors_count = int(input(f"Enter the number of neighbors for vertex {vertex}: "))
        neighbors = {}
        for j in range(neighbors_count):
            neighbor = input(f"Enter neighbor {j+1}: ")
            cost = int(input(f"Enter cost for the edge ({vertex} - {neighbor}): "))
            neighbors[neighbor] = cost
        graph[vertex] = neighbors
    return graph

graph = create_graph()
start_node = input("Enter the starting vertex: ")

# Run Dijkstra's algorithm
distances = dijkstra(graph, start_node)
print("Shortest distances:")
for node, distance in distances.items():
    print(f"Distance from {start_node} to {node}: {distance}")
