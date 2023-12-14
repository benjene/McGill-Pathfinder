# EDGE
```
{
  "id": "02321",
  "name": "Burnside main hallway ?", //descriptive name
  "type": "hallway",
  "isAccessible": true,
  "startNodeId": "471283",
  "endNodeId": "491382",
  "indoor": true,
  "hasRestrictedAccess": true,
  "distanceX": 50,
  "distanceY": 10, // aka elevation gain
  "weight": 20
}
```

### Edge & Node ID
- Maybe should be a random ID for easier lookups
- 7 digits? Are 1 million unique nodes sufficient?

### Type
- Stores info like if the path is an elevator, staircase, hallway path, cobblestone path, paved road, etc.

### Edge weights
- Used to calculate shortest path.
- What variables make a path more or less desirable? 1 meter of elevation gain is more strenuous than walking forward 1 meter on flat ground. What else?
	- Waiting for an elevator vs walking up one floor? Add weight for elevator nodes?

### Accessibility
- Any other disabilities to consider aside from wheelchairs / crutches?
- Do some paths outdoors become inaccessible during the winter with snow and ice?

### Restricted Access
- Certain buildings have hours where they are closed to all but those with special card access.
	- Where to find this info?
	- CS students have 24/7 access to Trottier
	- Arts students have 24/7 access to Ferrier
	- Science students have 24/7 access to Burnside
	- Engineering students have 24/7 access to Engineering Complex
	- Commerce students have 24/7 access to Bronfman
	- What else?

### Access Hours
- Hours are stored as key-value pairs of a group and their access hours. E.g. the general public, computer science students, arts students, etc.
- - Hours stored as array of length 4:
	- According to McGill Security's building opening hours, we should consider the 4 sets of daily opening hours
		- Monday - Thursday
		- Friday
		- Saturday
		- Sunday
- We store the time as dictionaries with strings for open and close times: {"open": "07:45", "close": "22:00"}
	- Check if open time > current time > closing time

# NODE
```
{
  "id": "1591203", //random int starting with 1. It is more efficient to have small ints as unique identifiers.
  "name", //descriptive name
  "latitude": 40.7128, // For indoor maps, X refers to location on custom image map.
  "longitude": -74.0060, // For indoor maps, Y refers to location on custom image map.
  "type": "buildingEntrance",  // or other types like 'classroom', 'staircase', etc.
  "name": "Main Library Entrance"
  "hasRestrictedAccess": true,
  "hours": { "general_public" = [{"open": "07:45", "close": "22:00"}, {"open": "07:45", "close": "18:00"}, {"open": "10:00", "close": "18:00"}, {"open": "10:00", "close": "18:00"}], science = [ ... ], arts = [ ... ]} // Can we use Factory Design Pattern? Store pointers to objects with this info?
  "tags": {"GIC", "Geographic Information Center"} // extra info about a particular location. e.g. a point. Perhaps used for a search function later?
}
```
### Tags
- Extra info about the node not stored in the descriptive name field
- Used for search functions? e.g. add "GIC" tag to node referring to entrance of GIC, so that if someone searches for GIC in search bar, the node with this tag is returned.
	- Should this be stored on the nodes? Or another way?

# User
```
{ 
  "groups": { "general_public", "arts" }
  "needsAccessibility": true
}
```

### Membership
- By default, all users will only be part of the group `general_public`, which indicates they only have the default level of access to buildings on campus. If the user chooses to, they can select their major and degree, and they will be able to be routed through buildings the general public may not have access to.
