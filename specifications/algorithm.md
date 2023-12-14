### Algorithm
We will use a shortest path algorithm (Dijkstra's, A*?) to compute the shortest path in between two points.

The pathing will depend on:
1. The opening hours of buildings
2. Accessibility needs of user
3. Indoor pathing weight

A query for a shortest path can return two paths:
1. True shortest path
2. Shortest path with added weights for outdoor pathing, to prioritize indoor pathing.

#### Pseudocode
```
//shortest path algorithm selects edge
if edge.hasRestrictedAccess == true:
	//case where door can sometimes lock
	if (hasAccess(edge.end_node.hours) == true) {
		// has access, continue algorithm
	}
	//user does not have access, algo continues with next edge
else: //case where you can always cross edge
	//keep running shortest path algorithm with current edge

func hasAccess(access_hours) {
	for (group in user.membership) {
		if group[open] <= current time < group[close] {
			return true;
		}
	}
	return false;
}
```
