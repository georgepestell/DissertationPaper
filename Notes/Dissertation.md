# Abstract

This integrated masters dissertation project develops an approach to an off-road, terrain-centred routing task. A first attempt at developing a development framework for developing personalised user-preferences and feature-relationships using various data-sources to define a custom cost function for Dijkstra's routing algorithm on a mesh derived from satelite terrain-height data. This project demonstraits the real potentiality for a real human-centred, inclusive routing algorithm that is unrestricted to pre-defined roads and paths, whilst addressing the problems and barriers that need to be overcome to be a viable tool for everyday usage. A huge number of interesting future projects are outlined and their potential utility are explored.

# Declaration

I declare that the material submitted for assessment is my own work except where credit is explicitly given to others by citation or acknowledgement. This work was completed during the current acaemic year. The text of this report is [TODO: WORD_COUNT] words long, including the appendices. In submitting this report to the University of St. Andrews, I give permission for it to be made available for use in accordance with the regulations of the University Library. I also give permission for the report to be made aaiable on the Web for this work to be used in research within the University of St. Andrews and for any software to be released on an open-source basis. I retain copywrite of this work and ownership of any resulting intellectual property.

# Introduction

Existing route planning applications are exceedingly popular in both consumer and business settings, with over 1 billion people using Google Maps [@google2019keyword].

In addition, 1 in 5 people in the U.K. over the age of 16 say they run, with around 30% of those aged between 35 to 44 saying they run at least monthly. In 2024, Strava saw over 135 million active users 190 countries. [#](https://press.strava.com/articles/strava-releases-annual-year-in-sport-trend)

With the increasing imperative to tackle the climate and health emergencies, many people are seeking alternative, healthier forms of getting around such as cycling an walking.

However, all existing route planner applications rely solely on pre-existing paths and roads. Whilst ideal when travelling by car, in many places across the U.K., public footpaths are sparse to non-existent, and many feel unsafe walking or cycling on roads due to: a lack of pavements / cycle lanes; blind corners; and an overall lack of confidence in sharing the road with cars. 

This project designed and developed a route planner application unrestricted to pre-defined paths and roads. A modular framework enables the opportunity for future research to add additional data sources, and define more complex research-lead data relationships, hopefully improving the quality of the routes generated. An initial attempt at definining a pre-set for this ranking algorithm was created, using a research-based methology to quantify the impacts of various terrain features.

A detailed evaluation of the quality of the routes was conducted, finding that further research into quantifying the relationships between terrain features and walking speed are required. In addition, weaknesses in the underlying design are discussed, along with potential solutions and work-arounds. Many areas for future development are explored, with concrete steps and ideas that could allow this to serve as the groundwork for many future research projects.






In it's design, a modular framework was created, where features that impact the quality of a particular route can be created and integrated easily. 

In this project, an off-road route planner application was developed, with a particular focus on creating a framework for future reasearch to quickly and easily integrate new data sources that play a role in route selection. 

# Literature Review

## On-Road Routing Algorithms

The most well known route planners are on-road planners, generating routes between two given points across pre-defined roads and paths connected by junctions.

They work by applying some routing algorithm such as some variation of A*, with nodes in the search graph representing the endpoints of, and junctions between, roads/paths. The edges of the graph represent sections of roads between these nodes, and are weighted often by their overal distance, 

# Requirements Specification

## Original Specification

The following gives the original requirements specification developed for the project before development began. In following an AGILE development philosophy with constant reearch and development, some of these requirements changed during development to reflect a furthering understanding of the problem, and to maximize the potential utility of this project. 

## Updated Requirements Specification

The following gives the final requirements specification, emerging throughout the development process as new insights were gained into the best ways to achieve the main aim of the project.

## Routing Algorithm

## API Interface
### Chunking

### Data Caching

Data caching is completed

# Design

This section gives insight into the design decisions and challenges that were met in the creation of this project.

## Graph Representation

The task of finding safe routes over the terrain is best represented as a path finding search algorithm. These algorithms fundamentally require a graph node structure connected by edges. It is therefore necessary to define those elements.

Traditional routing algorithm represent the terrain topologically, searching between the connections between roads and paths. This requires significantly fewer search nodes than representing the geometry, and is suitable for traditional routing algorithms as a user cannot leave a road without moving to a different road at a junction/connection. However, off-road traversal should allow users to exit a road/path to a section of off-road terrian at an arbitrary point along the road/path. In addition, the geometric features matter when traversing off-road, not just the topological features, and so creating a graph network representing both is essential.

Therefore, a graph structure fundamentally built upon the geometric features was used, with topological features such as roads, terrain types, and areas of water are added without affecting it's geometric accuracy. To do so, a 3D terrain mesh is created from data representing the search area.

Nodes in the search graph represent the vertices of this mesh, and edges of the graph represent the edge and face being traversed in the mesh. This is because there are many different types of data that need to be represented in the mesh, and so both faces and edges are weighted. This will be discussed in further detail in the mesh derivation section,.

. Some research has used faces as nodes [TODO: research using faces as nodes]

To create this graph, a 3-dimensional terrian mesh is created from a digital elevation map (DEM), giving elevation points across a particular area. The 



Unfortunately, it is not feasible to represent the search graph in the efficient manner traditional routing algorithms use. Their representation using the connections and end points of roads/paths as search nodes, with edges representing the roads/paths themselves, as the connections are where decisions of whether to change road/path are made. This is independent of the geometry of the roads, and thus significantly reduces the number of search nodes. However, this method is unnapplicable to a terrain sensitive routing algorithm as an on-foot user may leave a road/path at any point along it, not just at junctions.

In many places, leaving paths and roads is either not feasible, or clearly inefficient due to the dangers and complications of off-road traversal. 

An alternative approach would be to create the search nodes by creating nodes at junctions, and adding intermediary nodes through some method along the way where users could split off from the path. 


There are various options for creating the search graph from the terrain. A naiive approach could simply create a uniform grid of points, and fetch the data values from each data source. However, with a small grid size, the number of search nodes would be very large, and with a large grid size, the quality of the resulting mesh in terms of it's representation of the real world would be low.

Instead, creating a graph structure that is dynamically sized depending on the complexity of the data at each point on the graph would enable high resolution where there is a lot of small details, but reduce the number of nodes required to search in areas where values are consistent, or data is low resolution.


As we are planning to search for routes over a particular portion of terrain, it makes sense that this graph represents the terrain in some way, but there are various options:

- **Triangular Irregular Network (TIN)** - Represent a continuous surface using 2-dimensional triangles in 3-dimensional space.
	- Search graph nodes can represent vertices, triangle center points, or the triangles themselves, with search edges representing edges, or segments of these triangles.
- Tetrahedral mesh - Represents 



## Mesh 

Similarly to Evans' approach to mesh derivaiton

## Data Sources

There are two fundamental GIS data types: raster, and vector data. Raster dataset layers consist of a grid of values, where each pixel corresponds to the value at a particular coordinate, which can be calculated using the metadata, storing the bounding box coordinates, and the pixel resolution. Vector datasets can contain any vector data (e.g. an array of coordinates representing contours of a river). GIS raster data is often in GeoTIFF format, preserving exact values, whereas vector data either in XML or GeoJson formats.

### DEM Data

There are various different potential sources of the DEM data required for mesh creation. Resolution varies between datasets, but high-resolution datasets are less publicly accessible.

- **opentopology.org** offers a permissive [TODO: LICENSE] for various DEM datasets, from global to regional, ranging from 1000m resolutions to 1m resolutions. An API key is required, and individual requests are limited in size depending on the dataset resolution (capped on average to [TODO: POINT CAP] data points). [#](https://opentopography.org/developers)
- **sentenel**

## API

For all of the data sources used in this project, storing the dataset for the entirety of the UK is both wasteful and unfeasible in terms of bandwidth and storage requirements. The 30m resolution DEM data alone would cover roughly

Having the program automatically fetch and process data from the relevant APIs was desired,

## Chunking

The data sources given above provide API endpoints which can be fetched using HTTP GET requests. 

## Caching

With DEM data and some data features calling APIs, caching data can greatly improve subsequent mesh generation times. 

### Chunking

With the search boundary directly proportional to the distance between the two points, requests spanning a larger area may require quite a large amount of data to be fetched and processed by the API. In addition, caching requests ca

With the mesh extent proportional to the distance between the start and end points, and data sources having various data resolutions, some requests will the amount of data that needs to be loaded and processed from the APIs 

Depending on the distance between the start and end points given to the router, and the radii multiplier set, the search boundary may span a very large area. In addition, data sources often have varying levels of resolution. Making calls to each data source API fetching the entire search boundary in one request may result in an an extremely large amount of data to be requested. Many APIs have request size limits, and the inherent lack of alignment to this naiive approach makes creating useful caches difficult - requiring a large amount of processing when used in different searches.

# Implementation

Many interesting implementation-specific challenges were met and decisions made in the completion of this project. This section details the specifics of the approach taken.

## Mesh

### Shape (triangle vs square, hexagon, etc.)

There are an infinite number of meshes that can represent the exact same terrain / DEM data. With the DEM satelite data, a single height position for each latitude, longitude point given means our mesh is particularly suited for a 2.5D mesh. These are meshes formed of 2D shapes, where there is a single z-position for each x,y point.

### Derivation (Constrained Delaunay Triangulation vs. Grid-based approach)

The DEM data from opentopology is regular, meaning point spacing is constant, creating a regular grid of elevation points. This gives the opportunity for many mesh derivation techniques to be used, as the points are neatly aligned.

Evans' (2023) approach utilized a square-based grid for mesh derivation. This approach is suited to the opentopography regular DEM data as points are aligned consistantly onto a grid, allowing regular squares to be generated.

However, square meshes have a number of significant draw-backs, which makes them less commonly used for terrain mesh representations in the fields of robotics, video-games, and geology. Firstly, squares (and to a similar degree rectangles), offer no variation 

Evans' approach used a custom approach, taking the grid values, and building the mesh manually. This project used Delaunay Triangulation for this process, using the CGAL library. CGAL provides a Delaunay_triangulation_2 object, which can be adapted for 2.5D models using the Projection_traits_xy_3 trait.
### Mesh Processing

The DEM data used for this project has a resolution of 

## Path Finding - Uniform Cost Search

## Cost Function

In this lengthy section, I will discuss the cost function. A parimary objective for this project both original and updated was to create a configurable cost function, allowing more knowledgeable users to define their own preferences and abilities, and for those to be taken into consideration when determining the goodness of routes.

## Features

### Distance
### Gradient

### API Data Features
#### Water (OSM)

There are various different potential sources to identify and tag water. 

For the majority of casual users, traversing water is undesired, and so there is an initial check in the base preset, which automatically returns an infinite cost for traversal over any amount of water.

[TODO: SHOW BASE WATER PRESET]

However, more adventurous travellers may desire to swim. For this, the SWIM_PRESET does not reject water entirely, but adds a speed penalty to traversing over water, as humans tend to travel around [TODO: SPEED COMP SWIM vs WALK] times slower when swimming as opposed to walking.

[TODO: SHOW SWIM PRESET]

One could imaging planning a triathalon-like event, where running is considered the base-speed. This is significantly faster than walking, and thus the penalty is more significant when swimming. This can all be modelled through changing the swim_penalty multiplier constant node in the preset configuration.
#### Terrain Type (CEH)
#### Paths (OSM)
## API and Caching
### Chunking

### API
### Caching
# Results & Analysis

Objectively analysing the routes generated by the router is only partially possible due to the subjective nature of route preference. However, given a particular preset created with a set of aims in mind


# Evaluation & Critical Appraisal

The routing pre-sets generated are difficult to evaluate fully within the categories of 

## Merits
## Limitations


# Further Improvements & Potential Projects

## Preset Editor Interactive UI

In the original requirements specification, a preset user interface was described, giving less technologically advanced users to define their own preferences and settings for the cost function features.

Here, I will discuss in more detail how this project could be easily extended so that feature presets could be configured iteractively.

Features are designed to be created with required configurations, and then initialized, where they can modify the underlying search graph, and then preprocessed with the final search mesh, where feature tagging may take place.

A user interface could be designed similar to a compositor in rendering pipelines. Often, these have nodes which can be dragged and dropped onto a workspace, with static configuration values as constant input boxes on nodes, and depenency inputs as connection anchors on the left side of the node, and it's output on the right side of each node. This allows a DAG diagram to be created by creating dependency relationships between features. \autocite{#fig-presetUI#diagram} demonstrates how this could look. This graph could then be processed upon completion into c++ code, where each static setting corresponds to a constructor parameter, and input connections correspond to named dependencies. \autocite{#fig-presetUI#code} demonstrates an example of a preset graph and the resulting generated code.

This code would have to be entered and compiled, but alternatives such as JSON serialisation of presets being created, and then parsing and deserialization by the routing application would require no additional compilation.

This would benefit the project in line with one of the core goals to create an inclusive and personalised route planner, and so further research could explore other ways of improving the user experience.

## 

## Performance

As discussed, the performance of this application was not a primary objective and there are many areas where performance gains could be found.

Firstly, further optimisations in the processing of the underlying mesh could be made to reduce the number of total vertices. This in turn reduces the number of unnecessary cost-evaluations that need to be carried out, as vertexes represent the search nodes in the uniform cost search.

# Conclusion
# Appendices

## User Manual

### Compilation

There are two parts to the source code: a command line utility made with C++ to be built and compiled with cmake/ninja, and a web interface which should be built for production, but is unnecessary for demonstration / development environments.

To compile the command-line utility, first setup the build directory:

```bash
cd tsr-cli
mkdir build && cd build
```

Then run the following build command, setting the configuration options as appropriate
- `TSR_TEST=ON/OFF` - specify whether tests should be built
- `CMAKE_BUILD_TYPE=Release/Debug` - far more performant in release mode, but debug mode increases logging information such as TRACE messages.

```bash
cmake .. -G Ninja -DCMAKE_BUILD_TYPE= -DTSR_TEST=
```

Afterwards, compile everything by running

```bash
ninja
```

### Command-Line Utility

See usage below:

```
Usage: 
  tsr-cli [options] <start_lat> <start_lng> <end_lat> <end_lng>
							   Route between the given start and end
							   points
  tsr-cli [options] --example  Route between the example start and
 						       end points

Options:
  --radii-multiplier  Radii multiplier to apply to domain size
  --output-dir        Directory to put output files
  --cache-dir         Tile cache directory
  --quiet             Quiet mode

```

### Web Interface

Note: Before the web interface can call the router, the command line utility must be built.

For development and demonstration, running the frontend web application and backend can be done together through the following:

```bash
cd tsr-ui
npm run dev
```

The backend can be ran on it's own with the following:

```bash
npm run server
```

The backend port can be changed by modifying the `PORT` variable in `tsr-ui/server/index.js`.

## Ethics


# References
European Space Agency (2024).  <i>Copernicus Global Digital Elevation Model</i>.  Distributed by OpenTopography.  https://doi.org/10.5069/G9028PQB. Accessed: 2025-01-01