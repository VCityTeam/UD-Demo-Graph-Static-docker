# UD-Demo-Graph-Static

A demos for visualizing RDF semantic graphs alongside 3D City models using:
* [UD-Viz](https://github.com/VCityTeam/UD-Viz), a frontend web application for urban data visualization
  * In particular, the [SPARQL module](https://github.com/VCityTeam/UD-Viz/tree/master/src/Widgets/Extensions/SPARQL) is used to visualize semantic urban data in the form of RDF
* [Strabon RDF Store](http://www.strabon.di.uoa.gr/) an RDF Store for storing and serving geospatial semantic graph data in the form of RDF
* [PostGIS](https://postgis.net/) a geospatial database extension of [PostgreSQL](https://www.postgresql.org/) used here as a backend database for Strabon

## Table of contents
- [UD-Demo-Graph-Static](#ud-demo-graph-static)
  - [Table of contents](#table-of-contents)
  - [SPARQL Query Widget User Guide](#sparql-query-widget-user-guide)
    - [Interface](#interface)
      - [Select Query](#select-query)
      - [Show/Hide Query](#showhide-query)
      - [Select Result Visualization Format](#select-result-visualization-format)
  - [For developers](#for-developers)
    - [Component Diagram](#component-diagram)
  - [Installation](#installation)
    - [Pre-requisites](#pre-requisites)
    - [Component Setup](#component-setup)
    - [Build Images and run containers](#build-images-and-run-containers)
    - [Upload RDF-Store Dataset](#upload-rdf-store-dataset)


## SPARQL Query Widget User Guide
This is a user guide for using the SPARQL Widget (currently under development) in a UD-Viz application. This is a Widget for visualizing urban graph data and interacting with objects in the 3D scene.

To open the Widget, click on the SPARQL Query button in the left panel:

![221245183-33a9ada3-ac06-4c10-bb97-a0736e6421fd](https://user-images.githubusercontent.com/23373264/221245352-7ec094e5-5a81-4a3a-a428-44a31bad0bec.png)

### Interface

![Untitled drawing](https://user-images.githubusercontent.com/23373264/193422973-43391ead-2bf9-4113-9e92-216a5426f60e.png)

![image](https://user-images.githubusercontent.com/23373264/221206638-b2d477d9-650d-47c4-be64-eb809f9538a5.png)

#### Select Query
Use this dropdown menu to load one of several prewritten queries to vizualize urban data in UD-Viz. This demo features 5 queries:
1. **Select a buildings and its details from 2015:** Select a specific building building from 2015 and visualize all of the related data points. Clicking on the node with the same color as the `citygml-bldg:Building` entry in the legend will zoom in on the specified building.
2. **Count the number of buildings in each year:** Count the number of buildings in each year from the dataset.
3. **Select All buildings from Gratte-Ciel 2015 (warning big query!):** Visualize the graph of the Gratte-Ciel dataset from 2015. Many of these nodes represent buildings and clicking on any building node will zoom in on the building in the 3D scene.
4. **Select 30 buildings from Gratte-Ciel 2009:** Select 30 random buildings from the Gratte Ciel dataset in 2009.
5. **Select 30 buildings from Gratte-Ciel 2012:** Select 30 random buildings from the Gratte Ciel dataset in 2012.
6. **Select 30 buildings from Gratte-Ciel 2015:** Select 30 random buildings from the Gratte Ciel dataset in 2015.
7. **Select 30 buildings from Gratte-Ciel 2018:** Select 30 random buildings from the Gratte Ciel dataset in 2018.

#### Show/Hide Query
This button can toggle whether the text area for the query to be submitted is shown or not. This also allows the query to be edited before submission.

Queries are written in [SPARQL](https://www.w3.org/TR/sparql11-query/)

#### Select Result Visualization Format
Use this dropdown menu to select how the query result will be visualized.
Note that in the **Graph** visualization format, clicking on a node with the legend color `citygml-bldg:Building` will zoom the camera on the building in the 3D scene.

## For developers
### Component Diagram
![SPARQL POC Component Diagram](https://github.com/VCityTeam/UD-Demo-Workspace-GratteCiel/blob/master/UD-Demo_SPARQL_POC_Component_Diagram.svg)

## Installation

### Pre-requisites 

* [Install Docker](https://docs.docker.com/engine/install/)
* [Install Docker Compose](https://docs.docker.com/compose/install/)

### Component Setup
To configure the demo and the components that support it edit the `.env` file to be launched with docker-compose. By default, the following ports are used by the following services:
- 9006: `UD-Viz`
- 9007: `Strabon`
- 9008: `PostGIS`

The following sections will describe how to configure this file for each component. 

### Build Images and run containers
First, edit the [.env](.env) file to set the credentials used to authenticate user of the strabon frontend.

Then, build the PostGIS, Strabon, and UD-Viz docker images and run their containers:
```
docker-compose up
```

**Note:** Make sure to set the `sparqlModule/url` port in the `./ud-viz-context/config.json` file to the same port for the _Strabon_ container declared in the `.env` file. If these ports are ever changed after building the images, the _UD-Viz_ image must be rebuilt:
```
docker-compose rm udviz
docker-compose build udviz
```

### Upload RDF-Store Dataset
To upload these files into Strabon to be used by UD-Viz:
1. Open a web browser and navigate to [http://localhost:9007/strabon](http://localhost:9007/strabon)
2. From the left menu, click *Explore/Modify operations* then *Store*
3. Copy and paste the following URL into the *URI Input* field and click *Store from URI*. Repeat for each URI. Note you may be asked to enter the Strabon administrative credentials here.
   1. `https://dataset-dl.liris.cnrs.fr/rdf-owl-urban-data-ontologies/Datasets/2009/GratteCiel_2009_split.rdf`
   1. `https://dataset-dl.liris.cnrs.fr/rdf-owl-urban-data-ontologies/Datasets/2012/GratteCiel_2012_split.rdf`
   1. `https://dataset-dl.liris.cnrs.fr/rdf-owl-urban-data-ontologies/Datasets/2015/GratteCiel_2015_split.rdf`
   1. `https://dataset-dl.liris.cnrs.fr/rdf-owl-urban-data-ontologies/Datasets/2018/GratteCiel_2018_split.rdf`

Now the demo is ready and can be accessed from [http://localhost:9006](http://localhost:9006)
