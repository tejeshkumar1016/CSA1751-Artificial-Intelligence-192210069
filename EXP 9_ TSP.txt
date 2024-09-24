import itertools

# Function to calculate the distance between two cities
def distance(city1, city2, distance_matrix):
    return distance_matrix[city1][city2]

# Function to calculate the total distance of a given route
def total_distance(route, distance_matrix):
    total_dist = 0
    for i in range(len(route) - 1):
        total_dist += distance(route[i], route[i+1], distance_matrix)
    total_dist += distance(route[-1], route[0], distance_matrix)  # Return to the start
    return total_dist

# Brute force approach to solve TSP
def travelling_salesman_problem(cities, distance_matrix):
    shortest_route = None
    min_distance = float('inf')
    for perm in itertools.permutations(cities):
        current_distance = total_distance(perm, distance_matrix)
        if current_distance < min_distance:
            min_distance = current_distance
            shortest_route = perm
    return shortest_route, min_distance

# Example usage
cities = [0, 1, 2, 3]
distance_matrix = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]

route, distance = travelling_salesman_problem(cities, distance_matrix)
print(f"Shortest route: {route}")
print(f"Distance: {distance}")
