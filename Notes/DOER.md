# Description

Traditional GPS routing technologies are ubiquitous in today's car-centred society. However, radical problems such as the climate and heath emergencies require radical changes to the ways we get around. Humans can traverse a much wider range of terrain than cars, yet mapping systems rely solely on pre-defined paths and roads. In rural environments, paths can be sparse, leaving those without experience with an area to stick to longer, more arduous, and potentially dangerous road-routes. Modern advances such as OS Maps and Google Maps' Terrain View offer some terrain-sensitive routing information, such as difficulty ranking, yet are still locked to the same pre-defined paths and roads.

This project aims to create a more generalizable form of routing algorithm; one not restricted to any pre-defined paths; and one that can take into consideration the needs and abilities of different users.

# Objectives

## Primary

### Modular Routing Algorithm

The core artifact this project aims to create is the terrain sensitive routing algrithm. This will take as input two points: the start and end points which will be given using their latitude and longitude. The output will give the optimal route based on a ranking algorithm. The ranking algorithm will consider each potential step from the start to target, and determine how "good" the considered steps are, where "goodness" will be defined as the predicted speed. It will store the overal route "goodness", and progress along the route with the highest score. At it's most basic, the following data sources must be considered:

- **elevation/gradient** - both forwards and perpendicular gradient impact the viability and speed of a given route
- **terrain type** - water and land is the most basic form of terrain distinction, but additional data sources will allow distinction between rocky terrain, forests, etc.
- **distance to target** - some metric representing distance to the target point will be an essential component in determining the next optimal step on the route.

An essential design feature of this algorithm will be the ability to adapt to the differing needs and abilities of it's users. The impact of the different data sources available to the ranking algorihtm has on the overal route rank will have to be explicitly defined. Representing these as function curves, and allowing these to be created and customized will allow users to change the importance of certain data on the feasibility of a certain route.

### Route Visualisation

The routing algorithm itself will need to output the suggested route. However, to aid in the use of the algorithm for actual planning and support for users following the route, the ability to see the output projected onto the terrain is a desireable feature.

### Generated Route Evaluation

Ultimately, the usefulness of the routing algorithm will be determined by the quality of the routes generated. Successful evaluation of the suggested routes will aid in the creation of the ranking algorithm configuration pre-sets. To do this, routes humans have already taken between the same two points should be used to compare to those the algorithm suggests.

## Secondary

### More Complex Data Sources

To increase the usefulness of the algorithm, incorporating additional data sources to the ranking algorithm will be useful as it allows more realistic modelling of route planning. These data sources may include:

- **current weather conditions**
- **historical weather conditions**
- **water sources** - For long journeys, ensuring water sources are available at regular intervals is important.
- **surrounding terrain gradient** - For many, traversing along a thin flat ridge with a sharp gradient adjacent is much slower than traversing along a large flat area

### Ranking Configuration Presets

In aid of allowing different mobility users to specify the terrain and features impacting their routing decisions, creating presets for these users would allow for less-experienced users to find utility in this tool.

## Tertiary

### Interactive Configuration Interface

To allow less technologically-experienced users to create their own custom configurations, an interactive interface, allowing connections to be made between data, and the definition of custom relationship curves determining the data and it's impact on the speed of the potential route will be useful.

### Live GPS Tracking

Modern route finding tools like Google Maps allow live route tracking which is useful as it helps those following the route to verify their location along the route, and prevent getting lost. This objective may be met by simply allowing the exporting of generated routes to a format that can be imported by these live routing tools.

### Animated Route Generation

A technically interesting, but less useful feature to include is to generate an animation (e.g. GIF) which shows the routes considered and decisions made by the ranking algorithm. This may give insights into the thinking of the algorithm and even aid in determining further improvements to the algorithm.

# Ethics

Below this document contains the draft version of the full ethics application, as I wish to use Strava Metro's API to evaluate the routes generated by the algorithm against the most popular routes between the same points. 

# Resources

No resources beyond standard lab provision required.

# Risks

To evaluate the routes generated by the routing algorithm, I have requested access to Strava Metro's API which offers a "most popular route" between two points. This application is pending. To mitigate the risk of this application failing or not being approved in time, if this situation occurs, I have planned to go to popular off-road walking destinations, and tracking my own routes to use to compare to the generated routes.