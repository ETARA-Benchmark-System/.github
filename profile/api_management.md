# Web API Simulation Management
This section will present the individual tools needed to simulate a Web API with all its characteristics. First, an overview of all possible functionalities related to Simulated Web APIs is given. Then we will explain in detail how to create a simulated Web API and which settings can be made. Finally, we will discuss the possibility of creating your own response templates using [Apache FreeMaker](https://freemarker.apache.org/index.html).  

## Overview
After users have registered their databases and have imported some predefined Web API configurations, they can be used to simulate APIs. Figure 4 shows a short overview of all simulated Web APIs, i.e., their labels, the web path under which they can be accessed, their status and an overview of all possible actions.

| ![api_overview](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/42aec325-1d93-4516-8192-309c867becfb) |
|:--:| 
| **Figure 1:** Overview of Simulated API Configurations |

The first button opens a menu for editing all options (see Figure 5) and the following two buttons are used for duplicating and deleting the settings. Especially the option to duplicate an API configuration is very useful in the beginning and to make small changes in the API without having to change all settings again.

## Simulation Configurations
Figure 2 shows an example of all configuration options that ETARA provides. After specifying a label for the simulated API (see Figure 2, marker 1), users must specify the path (URL) which is used to request the API (see marker 2). Next, they select the database to use (see marker 3) and the average response time (see marker 4). Moreover, users can configure the rate limit (see marker 5) which defines the number of requests per minute and day. Since the APIs being simulated are RESTful Web APIs, data is requested via HTTP Get requests. When a client requests a specific resource on a Web server using the HTTP protocol, the client submits certain GET parameters to the server with the requested URL. These parameters are pairs of names and corresponding values. They are appended to the URL with the $?$ character followed by a parameter name and tell the server which resources are meant. The parameter name to which the simulated API responds can be configured through the interface (see marker 6).

| ![detailed_api](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/561bfc66-c744-407b-828e-1c9974f311b0) |
|:--:| 
| **Figure 2:** General API Configuration Options |

The most complex configuration is to make valid (SPARQL) queries to the database, extract desired information and insert it into the given response template. For this purpose, users can specify one or more triple patterns that are used to identify a subject in the database (see marker 7). In the example shown in Figure 2, the database *sample_crossref* is searched for a subject that has a relation named *doi* and refers to the value of the parameter named *doi*. The found subject (an entity) is then used to fill the response template, using Apache FreeMarker, with information about the entity (e.g. the title of a publication). A detailed explanation of FreeMarker is explained in the later sections.

## Advanced Configurations
In addition to the classic configuration options such as rate limit or latency, users are able to control more complex behaviors of APIs. The "Search Type" option in Figure 3 specifies the search method to be used. There are two search options to choose from: *precise* and *fuzzy*.

| ![advanced_api](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/3cdb9202-dd25-4fbb-bf12-e2840b09301b) |
|:--:| 
| **Figure 3:** Advanced Configuration Options |

The *precise* parameter sets APIs to only return data that was requested. For example, if an API receives a request containing an arxiv ID, the corresponding publication is searched. If it exists, the found publication entity is forwarded to the response template as described before. However, if no publication with the searched ID exists, no result can be returned. 

The *fuzzy* parameter enables an approximate search. This allows to return search results that have a certain degree of semantic overlap with the query. This option was implemented because some APIs behave like a classic Web search and return the best results for the query. For example, when passing a title instead of an ID, such behavior may be desirable. 

Furthermore, users can configure the type of error handling. For this, the "Error Type" option provides three possible parameters: (1) *HTTP Status Code*, (2) *JSON With Status Code* and (3) *JSON Without Status Code*. By selecting *HTTP Status Code*, the simulated API responds with an HTTP status code including an error description, which provides information about the nature of the error. If the *JSON With Status Code* parameter is used, the API sends a JSON object with attribute-value pairs describing the error code. Additionally, an HTTP status code is appended to the response. By *JSON Without Status Code*, only a JSON object containing a description of the error code is sent. These three options cover all the usual ways a server handles errors or unsuccessful requests.

## Response Templates
TO BE DONE
