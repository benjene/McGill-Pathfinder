# EDGE
{
  "id": "02321", //random int starting with 0
  "name": "Burnside main hallway ?", //descriptive name
  "startNodeId": "node123",
  "endNodeId": "node124",
  "indoor": true, // or false if it's an outdoor path
  "distanceX": 50, // distance in X direction in meters or other units. 
  "distanceY": 10, // distance in Y direction
  "isAccessible": true, // or 'elevator', 'ramp', 'flat', etc.
  "hasRestrictedAccess": true, //we assume restriction is for entering but not exiting. We determine if a user is exiting.
  "publicHours": ["07452200", "07452000", "100018000", "100018000"], // I assume unique hours COULD be Mon-Thurs, Fri, Sat, Sun. e.g. open 7:45-10PM Mon-Thurs, 7:45-8PM Friday, 10-6 Sat, 10-6 Sun
  "specialAccessHours": ["07452200", "07452000", "100018000", "100018000"], // for card holders.
  "specialAccessFaculty": ["Science"] // list of faculties with special access
}

# NODE
{
  "id": "1591203", //random int starting with 1
  "name", //descriptive name
  "latitude": 40.7128, // For indoor maps, X refers to location on custom image map.
  "longitude": -74.0060, // For indoor maps, Y refers to location on custom image map.
  "type": "buildingEntrance",  // or other types like 'classroom', 'staircase', etc.
  "name": "Main Library Entrance"
  "isRestricted": true, //For edges where hasRestrictedAccess=true, when traversing, check the value of isRestricted of the other node..
}


https://www.mcgill.ca/facilities/files/facilities/fall_winter_spring_hours_2023-2024_v12.pdf // opening hours
