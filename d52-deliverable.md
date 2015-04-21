# Data retrieval for semantic enrichment/processing and semantic indexes for domain specific data retrieval

Deliverable D5.2

## Documentation Information


* *Deliverable Nr Title*: D5.2 Data retrieval for semantic enrichment/processing and semantic indexes for domain specific data retrieval
* *Lead*: Reto Gmür (BUAS)
* *Authors*: Reto Gmür (BUAS)
* *Publication Level*: Public

### Document Context Information

* *Project (Title/Number)*: Fusepool P3 (609696)
* *Work Package / Task*: WP5 / T5.3 & T5.4
* *Responsible person and project partner*: Reto Gmür (BUAS)

### Quality Assurance / Review

[TBD]


### Official Citation

Fusepool-P3-D5.2

### Copyright

This document contains material, which is the copyright of certain
Fusepool P3 consortium parties.

This work is licensed under the Creative Commons Attribution 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/.

## Executive Summary

This deliverable covers the interaction of Fusepool P3 with external non-human resources and actors. It 
is thematically and technologically adjacent on one side to D4.1 which covers the interaction with human users and which uses the services provided by this deliverable and on the other side with D5.3 which provides the generic data storage/access RDF API and is a constituent part of the P3 Platform Architecture (D5.1).

The data retrieval for semantic enrichment supports both components delivering the data to the platform, notably GUI components allowing to upload files as well as components harvesting data from external sites. The data retrieval is tightly integrated with the data transformation components provided by Work Package 2 which uses the same RESTfull RDF API as the components performing the semantic enrichment provided by Work Package 3.

The components involved are tightly integrated in that they provide a single entry points hiding away all the complexity of the various processing steps. On the other hand the components are loosely coupled which does not just improve stability and flexibility but also greatly enhance debugging possibilities by having a very small set of well defined and monitorable points of interactions. Throughout the refinement, enrichment and processing lifecycle the data passes interfaces defined by the P3 Transformer API that allow to monitor the state of the processing so that corrective measures can be taken if needed.

With T5.4 this deliverable comprises the provision of application level retrieval and query services. As specified by the Platform Architecture wherever possible the interaction between data consuming and the data-storing components shall follow standard protocols and interaction patterns, most notably the ones defined by the Linked Data Platform Specification [LDP]. The architecture foresees T5.4 components to allow some application specific access interfaces provided by services interacting directly with the underlying triple store as opposed to using the standard interactions APIs. As shown by D4.1 the generic API did not needed to be extended with non-standard custom interfaces to accommodate the requirements of the client components. In one case however it was necessary to switch from the originally envisaged LDP interaction model to the SPARQL query language and protocol as this offered a far better performance. The fact that no specific interfaces needed to be introduced proves the versatility of the chosen standard protocols and greatly increases flexibility as well as protection of the investments of the organizations deploying the P3 platform as it allows them to freely choose between standard compliant backends.

## Abbreviations

| Acronym/Abbreviation | Description |
|----------------------|-------------|
| API     | Application Programming Interface            |
| LDP                 | Linked data platform |
| LDPC                | Linked data platform Container |
| RDF     | Resource Description Framework               |
| REST    | Representational State Transfer              |
| SPARQL        | SPARQL Protocol And RDF Query Language |                                                                                                                                                                                                              


## Introduction

The purpose of this deliverable it to provide both for the data retrieval, i.e. allow to retrieve the data that shall be semantically enriched, as well as for the services providing domain/application level views on datasets. 

The data retrieval for semantic enrichment supports both components delivering the data to the platform, notably GUI components allowing to upload files as well as components harvesting data from external sites. The components delivering content to the platform use standard interaction mechanisms to add contents to a Transforming LDPC as this has been defined in the Platform Architecture D5.1. While D5.1 describes the functional role as well as the protocols supported by the P3 Proxy this report shall focus on the implementation of this crucial mediator between data retrieval and the data processing leading to queryable semantic content. The Transforming LDPC architecture presupposes an agent adding data to the container. Such an agent can be a GUI component allowing the user to add files to an LDPC of the workspace or the crawler that retrieves remote resources at regular intervals. 

On the side of the application level retrieval and query service the architecture of the platform foresees the possibilities of services providing a custom HTTP API that interact directly with the triple store. As written in the D5.1 report, such services are only implemented if the development of the UI shows that an interaction via the standard mechanism SPARQL and LDP is not feasible or not providing an adequate level of performance. We will see that a change of the standard protocol could avoid the introduction of such service, increasing the portability of the platform across storage backends. 


## Data retrieval

### Proxy

### Crawler

### Monitoring data

Originally we planned to implement a logging no-operation transformer for debugging as part of T5.3. This no-op transformer could have been added at any position of a transforming pipeline to log the data passed from one transformer to the next. The no-op transformer was thought to be useful to monitor the data at each of its transformation steps. Experience has shown however that standard TCP/IP network monitoring tools where sufficient in most cases. The only case we encountered where standard TCP/IP monitoring tool were not powerful enough was when debugging a scenario where different pipelines that are run concurrently access the same transformer, but even in this case we did not need the planned logging no-operation transformer but could use a standard logging HTTP Proxy such as The Grinder [Grinder], given that the transformer API is based on HTTP and the RDF data exchange bases on standard serialization formats no further tool was needed. This finding clearly exemplifies the benefits of the chose standards based architecture with loosely coupled components communicating vie HTTP and standard format. 

## Application level retrieval

### Findings from T4.1

### LDP vs. SPARQL

### CORS
 
-> D4.1
-> Issue against marmotta
-> Added support in transformers by support in the library


| Ref.             | Description |                                                                                                                                                                                                              
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| LDP | [http://www.w3.org/TR/ldp/](http://www.w3.org/TR/ldp/) |
| Grinder | [http://grinder.sourceforge.net/g3/tcpproxy.html](http://grinder.sourceforge.net/g3/tcpproxy.html) |



T5.3 – Data retrieval for semantic enrichment: The Fusepool P3 platform will provide workspaces for the
semantic enrichment process. This ensures that the original state of the data is kept throughout the enrichment
process and enables storage and retrieval of meta-information from the semantic enrichment process (e.g.
to backtrace processing steps leading to (un)wanted linking results). [SRFG, BUAS & OGL support, BUAS
coordinates integration]
T5.4 – Application level retrieval and query services: provide domain/application level views on datasets
including specialised query services. This includes spatial/temporal queries as applied by YAGO2 as well
as text/label based retrieval methods. For the later open-source search technologies like Apache Solr and
elasticsearch customize for RDF dataset will be exploited. [SRFG, OGL support, BUAS coordinates integration]