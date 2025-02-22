```
package main

import (
	"fmt"
)

type Graph struct {
	Vertices []*Vertex
}

type Vertex struct {
	Key          int
	AdjacentList []*Vertex
}

// Add a new vertex to the graph
func (g *Graph) AddVertex(key int) {
	g.Vertices = append(g.Vertices, &Vertex{Key: key})
}

// Print the graph
func (g *Graph) Print() {
	for _, v := range g.Vertices {
		fmt.Printf("Vertex %v = ", v.Key)
		if len(v.AdjacentList) == 0 {
			fmt.Printf("no edges\n")
			continue
		}
		for _, a := range v.AdjacentList {
			fmt.Printf(" edge %v ", a.Key)
		}
		fmt.Println()
	}
}

// Get a vertex by key
func (g *Graph) GetVertex(key int) (*Vertex, bool) {
	for _, v := range g.Vertices {
		if v.Key == key {
			return v, true
		}
	}
	return &Vertex{}, false
}

// Add an edge between two vertices
func (g *Graph) AddEdge(key1, key2 int) {
	v1, ok1 := g.GetVertex(key1)
	v2, ok2 := g.GetVertex(key2)

	if !ok1 || !ok2 {
		fmt.Printf("Error adding edge: vertex %v or %v not found\n", key1, key2)
		return
	}

	if g.CheckEdge(key1, key2) {
		fmt.Printf("Edge already exists between %v and %v\n", key1, key2)
		return
	}

	fmt.Printf("Adding edge from %v to %v\n", key1, key2)
	v1.AdjacentList = append(v1.AdjacentList, v2)
}

// Check if an edge exists between two vertices
func (g *Graph) CheckEdge(key1, key2 int) bool {
	v1, ok := g.GetVertex(key1)
	if !ok {
		return false
	}

	for _, a := range v1.AdjacentList {
		if a.Key == key2 {
			return true
		}
	}
	return false
}

// Perform DFS traversal
func (g *Graph) DFS(startKey int) {
	visited := make(map[int]bool)

	startVertex, ok := g.GetVertex(startKey)
	if !ok {
		fmt.Printf("Starting vertex %v not found\n", startKey)
		return
	}

	fmt.Println("DFS Traversal:")
	g.dfsHelper(startVertex, visited)
}

// Helper function for recursive DFS
func (g *Graph) dfsHelper(vertex *Vertex, visited map[int]bool) {
	visited[vertex.Key] = true
	fmt.Printf("Visited %v\n", vertex.Key)

	for _, neighbor := range vertex.AdjacentList {
		if !visited[neighbor.Key] {
			g.dfsHelper(neighbor, visited)
		}
	}
}

// Perform BFS traversal
func (g *Graph) BFS(startKey int) {
	startVertex, ok := g.GetVertex(startKey)
	if !ok {
		fmt.Printf("Starting vertex %v not found\n", startKey)
		return
	}

	visited := make(map[int]bool)
	queue := []*Vertex{startVertex}

	fmt.Println("BFS Traversal:")

	for len(queue) > 0 {
		// Dequeue the front element
		current := queue[0]
		queue = queue[1:]

		// If already visited, skip
		if visited[current.Key] {
			continue
		}

		// Mark as visited and process the vertex
		visited[current.Key] = true
		fmt.Printf("Visited %v\n", current.Key)

		// Enqueue all unvisited neighbors
		for _, neighbor := range current.AdjacentList {
			if !visited[neighbor.Key] {
				queue = append(queue, neighbor)
			}
		}
	}
}

func main() {
	g := &Graph{}

	// Add vertices
	for i := 1; i <= 6; i++ {
		g.AddVertex(i)
	}

	// Add edges
	edges := [][]int{{1, 2}, {1, 3}, {2, 4}, {3, 5}, {5, 6}}
	for _, edge := range edges {
		g.AddEdge(edge[0], edge[1])
	}

	// Print the graph
	g.Print()

	// Perform DFS traversal starting from vertex 1
	g.DFS(1)

	// Perform BFS traversal starting from vertex 1
	g.BFS(1)
}

```