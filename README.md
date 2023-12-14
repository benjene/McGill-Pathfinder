# McGill Pathfinder - WIP 
#### Authors: Nicholas Foisy, Musab Umair (B.Sc CS & SWE @ McGill)
#### This project seeks to map all the indoor paths of McGill. A webapp will be developed where users can pick two spots on campus, indoors or outdoors, and find the shortest path between them.
#### These points could be a  point of interests (e.g. classrooms) or just any lat/long coordinate on campus.

#### As a proof of concept, all of the outdoor paths, as well as several floors of Burnside and the Arts building will be mapped and supported. The rest of the campus will be supported at a later date.

Currently, the project is still at the data collection stage.

### Tech Stack
Frontend: React
Backend: Node.js
Database: PostgreSQL + PostGIS

Libraries:
- Leaflet (displaying OSM map tiles, displaying the desired path (nodes & edges in GEOJSON format))
