# EDGE
```
{
  "id": "02321",
  "name": "Burnside main hallway ?", //descriptive name
  "type": "hallway",
  "startNodeId": "471283",
  "endNodeId": "491382",
  "indoor": true,
  "distanceX": 50,
  "distanceY": 10, // aka elevation gain
  "weight": 20,
  "hasRestrictedAccess": true,
  "hours": { "general_public" = [{"open": "07:45", "close": "22:00"}, {"open": "07:45", "close": "18:00"}, {"open": "10:00", "close": "18:00"}, {"open": "10:00", "close": "18:00"}], science = [ ... ], arts = [ ... ]} // Can we use Factory Design Pattern? Store pointers to objects with this info?
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
	- Other faculties...
		- Dentistry?
		- Education?
		- Agricultural, Env. sciences?
		- Law?
		- Music?
		- Medicine/health sci?
- Model for describing and storing access restrictions
	- Nodes have attribute restrictionLevel, integer values describing access restriction.
		- Non-locking nodes have restrictionLevel=0. This is true outdoors and indoors for the nodes that can be traversed through at any time (assuming you are inside)
		- The doors to enter all buildings have restrictionLevel > 0
		- Some buildings have areas with greater restrictions.
			- e.g. Engineering complex has limited opening hours. But, part of FDA is accessible for longer to give access to the Schulich library. However, the rest of the doors lock and users cannot leave the Schulich lobby area.
			- Thus, Schulich library has restrictionLevel=1. The rest of the McConnell Engineering complex has restrictionLevel=2.
	- Assumptions
		- You can always enter an area of lesser restriction. ie the doors will always be unlocked

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
  "id": "1591203", //random int starting with 1. I realize that it is more efficient to have small ints as unique identifiers.
  "name", //descriptive name
  "latitude": 40.7128, // For indoor maps, X refers to location on custom image map.
  "longitude": -74.0060, // For indoor maps, Y refers to location on custom image map.
  "type": "buildingEntrance",  // or other types like 'classroom', 'staircase', etc.
  "name": "Main Library Entrance"
  "restrictionLevel": 0, //For edges where hasRestrictedAccess=true, when traversing, check if the value of restrictionLevel is greater or lesser than the other node.
  "tags": {"GIC", "Geography Information Center", "Geography Information Centre"} // extra info about a particular location. e.g. a point 
}
```

### Latitude and Longitude
- Outdoor nodes have their latitude and longitude stored here to display on the map
- For indoor nodes, we are not able to get their GPS locations. We will give them X and Y values that show where they are on our not-to-scale floor plans.

### Tags
- Extra info about the node not stored in the descriptive name field
- Used for search functions? e.g. add "GIC" tag to node referring to entrance of GIC, so that if someone searches for GIC in search bar, the node with this tag is returned.
	- Should this be stored on the nodes? Or another way?
