# InTaVia Milestone-5

InTaVia Milestone 5 Documentation - Final operational system: The whole system is released, and operational.

### Previous Milestones

https://github.com/InTaVia/milestone-3

https://github.com/InTaVia/milestone-4

## Knowledge Graph & Backend (WP2 & 3)
### Data model InTaVia IDM-RDF

The repository https://github.com/InTaVia/idm-rdf contains the [IDM-RDF](https://github.com/InTaVia/idm-rdf/blob/main/idm-OWL/intavia_idm1.1.owl) at its current state (including ongoing discussions in the issues).

### Ingestion workflows / source datasets

The repository https://github.com/InTaVia/source-dataset-conversion contains the conversion scripts and the datasets in the IDM data model at their current state for the following prosopographical source datasets:

- [Finland](https://github.com/InTaVia/source-dataset-conversion/blob/main/BS_dataset/bs2intavia.ttl) (Aalto / UH)
- [Austria](https://github.com/InTaVia/source-dataset-conversion/blob/main/APIS_dataset/apis_oebl_serialization_2-9-2022.ttl) (OeAW)
- Netherlands [Part1](https://github.com/InTaVia/source-dataset-conversion/blob/main/intavia_biographynet/data/rdf/xaa.zip), [Part2](https://github.com/InTaVia/source-dataset-conversion/blob/main/intavia_biographynet/data/rdf/xab.zip), [Part3](https://github.com/InTaVia/source-dataset-conversion/blob/main/intavia_biographynet/data/rdf/xac.zip) (zipped in three parts for size) (VU)
- [Slovenia](https://github.com/InTaVia/source-data/blob/d17fc232c29de5ff444b47d68d05bc83e552fb37/datasets/sbi_data.ttl) (ZRC SAZU)

There is an improved workflow for ingestion currently implemented. It uses a [GitHub repo](https://github.com/InTaVia/source-data). For every new dataset or dataset version a pull request against main is created in the repo. On PR a validation using shacl is run. Merge of the  PR in main is only allowed when shacl validation succeeds and a review of the new dataset has been submitted. On merge to main another GitHub action is running. This second action pushes the dataset to the triplestore and creates the needed entries in the provenance named graph.

### Triplestore

The datasets are stored in a [Blazegraph](https://blazegraph.com/) triplestore, hosted at the ACDH-CH. Blazegraph provides a SPARQL endpoint for accessing the data.

### JSON API

The repository https://github.com/InTaVia/InTaVia-Backend contains an [OpenAPI](https://swagger.io/specification/) compliant [FastAPI](https://fastapi.tiangolo.com/)-based REST JSON API definitions and implementation for accessing the data in the InTaVia triplestore, at its current state.

Namely The following APIs are provided:

* Query Entities
* Retrieve Entity
* several vocabularies endpoints
* several statistics endpoints
* Reconciliation Service (implementing the [Reconciliation Service API](https://reconciliation-api.github.io/specs/))

The original version of the API is available under https://intavia-backend.acdh-dev.oeaw.ac.at/v1/.

A second and improved version of the API has been deployed under https://intavia-backend.acdh-dev.oeaw.ac.at/v2/docs.

### Read-only InTaVia Knowledge graph

A read-only version of the InTaVia Knowledge graph can be accessed in Blazegraph Workbench: https://intavia-ts.acdh-dev.oeaw.ac.at/, SPARQL endpoint URL: https://intavia-ts.acdh-dev.oeaw.ac.at/sparql.

### ResearchSpace for internal usage

In addition to the resources mentioned above we set up a [ResearchSpace instance](https://mp-playground.acdh-dev.oeaw.ac.at/) that is meant for internal work on and exploration of the knowledge graph. This service is currently for internal use only.

### Prefect workflow component

We deployed [Prefect](https://www.prefect.io/) within the  kubernetes cluster to run conversion, enrichment and ingestion scripts on the cluster. Given that the open-source version of this software solution doesnt come with authentication built in, this component is currently only reachable from within ACDH-CH subnet.

The repository https://github.com/InTaVia/prefect-flows contains implementations for the the following workflows:

* Ingest data
* Entity ID linker
* Reconcile person instances
* Inference
* Enrich CHO data
* Convert GeoSpatial coordinates
* Enrich person instances with wikidata relations
* Enrich person instances with ULAN relations
* Create APIS data directly from API

Prefect V2 has been deployed and flows are moved from v1 to v2 at the moment. The flows for pushing new data to the source-data repo (see above) are already in Prefect v2.

## NLP (WP4)

### Intavia NLP Pipelines

The Milestone 5 version of NLP pipelines and can be found [here](https://github.com/InTaVia/nlp-pipelines). This new version includes processing of English texts. It is also updated to work in a similar fashion with Dutch and Slovenian. The Finnish and German resources are listed as well there.

### From Wikipedia to Intavia

A full pipeline that includes scripts to obtain any biography from Wikipedia with its respective metadata and connected to Wikidata resources was developed. This includes a converter to the Intavia Data Format (IDM) which allows to directly import and display the extracted data in the Intavia Frontend. Several notebooks have been included in order to introduce the user to the use of this. This can be found [here](https://github.com/InTaVia/nlp-pipelines/tree/main/english)

### Dutch Annotated Data

We developed an annotated dataset comprising 346 biographies written in Dutch. These were human annotated for Tokenization, Sentence Splitting, Named Entity Recognition and Relation Extraction. The repository where data can be downloaded is yet to be defined...

### NLP Visualization

In cooperation with WP5 we developed multiple tools for visualizing end exploring a given dataset of Biographies.

#### Performancer & AnnoXplorer

The Performancer approach allows for distant reading and comparison of annotated text corpora and NLP tools. When a number of datapoints in one of the charts is brushed, the AnnoXplorer interface is opened in a new tab, giving the possibility for close reading and detailed analysis of the brushed annotations and texts.
The code and installation instructions can be found [here](https://github.com/InTaVia/Performancer_AnnoXplorer/releases/tag/v2.0.0).

#### Visual Document Explorer

The Visual Document Explorer is a Flask App that allows searching in the corpus for relevant documents, adding NLP annotations to the documents and displaying how different NLP outputs compare to each other. The code fur running the Web App can be found [here](https://github.com/angel-daza/bios-dutch).

#### ChatGPT-based Extraction and Verfication of Events in Biographies.

This work-in-progress prototype offers an interactive tool for biography event extraction and visual verification with ChatGPT to make text-mining tasks approachable for broad user groups. The code can be found [here](https://github.com/InTaVia/chatgpt-ner-vis).

## Frontend (WP5 & WP6)

The Milestone 5 Prototype (v1.0.0) of the InTaVia web client (frontend) is available as a permanent release: https://github.com/InTaVia/web/releases/tag/v1.0.0.

The prototype is available online: https://intavia.acdh-dev.oeaw.ac.at/.

The prototype implements functionalities used across the three top-level components (Data Curation Lab (DCL), Visual Analytics Studio (VAS), and Storytelling Suite (STS) = Story Creator (SC) + Story Viewer (SV)) in a single application (except the SV, which is a seperate application). Shared UI Componetns are managed in a seperate [github repository](https://github.com/intavia/ui) and is provided as a [npm package](https://www.npmjs.com/package/@intavia/ui). The functionalities implemented are:

### Search and find
- A **typed API client** provides data fetching functions (towards the backend = InTaVia JSON API) and defining types of query parameters and types of the response shape ([InTaVia JSON data model](https://github.com/InTaVia/api-client/blob/main/src/models.ts)). The client also provides a zod validation schema to validate responses. The api-client is managed in a seperate [github repository](https://github.com/InTaVia/api-client) and is provided as a [npm package](https://www.npmjs.com/package/@intavia/api-client).
- **Simple search** to query entities of the InTaVia KG by labels.
- **Advanced search** to specifiy target entity type or define related entities.
- **Search result list** with quality indicators (i.e., numbers of related events, media present, biography present)
- **Interactive visual result overview** (entity-histogram) inidcating frequencies by entity type and to adjust search filters of advanced search (i.e. filter for entity type).
- **Detail page** provides an overview of an entity's biography, including visualizations, media resources, a list of biographical events and the text-based biography source.

### Data curation, editing, and local data
[https://intavia.acdh-dev.oeaw.ac.at/search](https://intavia.acdh-dev.oeaw.ac.at/search) 
- **Collections** allow users to group entities and events by any topic of interest. Collections are created in the DCL (manually or from entire search results) and can then be used in the VAS and the SC to access stored data and visualize them with the help of the **data panel**. The data panel provides a list-based view onto the data. The data panel is used in the VAS and the SC as a link to the redux data cache (i.e., collections and the respective events and entities). Users can interacively add data listed to visualizations.
- **Data editing** allows users to edit attributes, relations (events), media resources and biographies of existing entities. Any edits are stored locally and are not saved in the backend.
- **Data creation** allows to create new entities in the frontend and add it to an existing collection.
- **Data import** allows to import InTaVia Excel templates and IDM-JSON formatted data. More details and how-to use the template are explained [here](https://github.com/InTaVia/data-import/tree/main/public/data). The import logic is managed in a seperate [github repository](https://github.com/intavia/data-import) and is provided as a [npm package](https://www.npmjs.com/package/@intavia/data-import).
- **Project export & import** allows to save and load the entire state of a InTaVia browser session. This mechanism allows to continue working later on a project or share the state of a project with others.
- Import/export page: [https://intavia.acdh-dev.oeaw.ac.at/io](https://intavia.acdh-dev.oeaw.ac.at/io)
  
### Visual analysis
The VA studio implements an interactive user interface allowing to create different visualizations for visual analysis of biographical and object data: [https://intavia.acdh-dev.oeaw.ac.at/visual-analytics-studio](https://intavia.acdh-dev.oeaw.ac.at/visual-analytics-studio)
- **Timeline** view implements a component that visually adapts to the number of displayed entities and events and the available display space. To avoid overplotting several aggregation modes were developed. Different modes of color encoding are provided.
- **Geographic map** view implements map layers that (1) are plotting simple markers at a given event location, (2) cluster proximal data points in a visually aggregated form, (3) connect event locations chronologically with trajectories/lines, and (4) show the data in a 3D perspective, where time is plotted along the z-axis (space time cube). Several options for different background maps and color encoding modes are provided. 
- **Network** view allows users to explore the social networks of historical actors and relations between different entities in a force-directed node link diagram. 
- **Visualization wizard** is shown in empty layout panels in the VAS and SC and allows to add/create new visualizations or load already existing visualizations into the respective panel. It also allows to delete visualizations or convert between visualization types.
- **Workspaces** in the VAS can have several predefined layouts containing up to four visualizations implementing multiple, coordinated views.

### Story creation
The ST creator implements an interactive user interface allowing to generate and slide-based stories. The prototype can depict entities and their events on timelines, maps, and networks and provides the otpion to add content elements (i.e., texts, images, videos, quizzes): [https://intavia.acdh-dev.oeaw.ac.at/storycreator](https://intavia.acdh-dev.oeaw.ac.at/storycreator)

- 

### Story viewing
The InTaVia Story Viewer offers a collection of stories curated using the Story Creator. It presents five stories featuring visualisations (e.g timelines, maps, ego-networks) and rich media content (e.g. images, videos, quiz, ...). 

**General Access:** View the complete collection of stories [here](https://intavia.fluxguide.com/fluxguide/app).

#### **Featured Stories:**
1. [Albrecht Dürer's Biography](https://intavia.fluxguide.com/fluxguide/public/content/fluxguide/exhibitions/1/system/app/dist/index.html?storyId=986)
2. [Pier Paolo Vergerio](https://intavia.fluxguide.com/fluxguide/public/content/fluxguide/exhibitions/1/system/app/dist/index.html?storyId=940)
3. [Die Baugeschichte der Wiener Hofburg vom Mittelalter bis zur Neuzeit](https://intavia.fluxguide.com/fluxguide/public/content/fluxguide/exhibitions/1/system/app/dist/index.html?storyId=960)
4. [Tuusula Lake Story](https://intavia.fluxguide.com/fluxguide/public/content/fluxguide/exhibitions/1/system/app/dist/index.html?storyId=993)
5. [Herwig Zens (1943-2019)](https://intavia.fluxguide.com/fluxguide/public/content/fluxguide/exhibitions/1/system/app/dist/index.html?storyId=1012)

