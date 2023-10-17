# InTaVia Milestone-5

InTaVia Milestone 5 Documentation - Final operational system: The whole system is released, and operational.

### Previous Milestones

https://github.com/InTaVia/milestone-3

https://github.com/InTaVia/milestone-4

# `Please Update Below`


## Knowledge Graph & Backend (WP2 & 3)
### Data model InTaVia IDM-RDF

The repository https://github.com/InTaVia/idm-rdf contains the [IDM-RDF](https://github.com/InTaVia/idm-rdf/blob/main/idm-OWL/intavia_idm1.1.owl) at its current state (including ongoing discussions in the issues).

### Ingestion workflows / source datasets

The repository https://github.com/InTaVia/source-dataset-conversion contains the conversion scripts and the datasets in the IDM data model at their current state for the following prosopographical source datasets:

- [Finland](https://github.com/InTaVia/source-dataset-conversion/blob/main/BS_dataset/bs2intavia.ttl) (Aalto / UH)
- [Austria](https://github.com/InTaVia/source-dataset-conversion/blob/main/APIS_dataset/apis_oebl_serialization_2-9-2022.ttl) (OeAW)
- Netherlands [Part1](https://github.com/InTaVia/source-dataset-conversion/blob/main/intavia_biographynet/data/rdf/xaa.zip), [Part2](https://github.com/InTaVia/source-dataset-conversion/blob/main/intavia_biographynet/data/rdf/xab.zip), [Part3](https://github.com/InTaVia/source-dataset-conversion/blob/main/intavia_biographynet/data/rdf/xac.zip) (zipped in three parts for size) (VU)
- Slovenia [example subset](https://github.com/InTaVia/source-dataset-conversion/blob/main/SBI_dataset/sbi.ttl) (ZRC SAZU)

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
* Reconciliation Service (implementing the [Reconciliation Service API
](https://reconciliation-api.github.io/specs/))

The original version of the API is available under https://intavia-backend.acdh-dev.oeaw.ac.at/v1/
A second and improved version of the API has been deployed under https://intavia-backend.acdh-dev.oeaw.ac.at/v2/

### ResearchSpace for internal usage

In addition to the resources mentioned above we set up a [ResearchSpace instance](https://mp-playground.acdh-dev.oeaw.ac.at/) that is meant for internal work on and exploration of the knowledge graph. This service is currently for internal use only.

### Prefect workflow component

We deployed [Prefect](https://www.prefect.io/) within the  kubernetes cluster to run conversion, enrichment and ingestion scripts on the cluster. Given that the open-source version of this software solution doesnt come with authentication built in, this component is currently only reachable from within ACDH-CH subnet. Given some delay in our original planning the scripts are currently still executed locally instead of running within prefect.

The repository https://github.com/InTaVia/prefect-flows contains implementations for the the following workflows:

* Ingest data
* Entity ID linker
* Reconcile person instances
* Inference
* Enrich CHO data
* Convert GeoSpatial coordinates

Prefect V2 has been deployed and flows are moved from v1 to v2 at the moment. The flows for pushing new data to the source-data repo (see above) are already in Prefect v2.

## NLP (WP4)

[...]

## Frontend (WP5 & WP6)

The Milestone 5 Prototype (v0.3.0) of the InTaVia web client (frontend) is available as a permanent release: https://github.com/InTaVia/web/releases/tag/v0.3.0.

The prototype is available online: https://intavia.acdh-dev.oeaw.ac.at/.

The prototype implements functionalities used across the three top-level components (Data Curation Lab (DCL), Visual Analytics Studio (VAS), and Storytelling Suite (STS) = Story Creator (SC) + Story Viewer (SV)) in a single application (except the SV, which is a seperate application). The functionalities implemented are:

### Search and find

### Data curation, editing, and local data

### Visual analysis

### Story creation

### Story viewing
Rlease: https://github.com/InTaVia/story-viewer/releases/tag/v1.0.0.
