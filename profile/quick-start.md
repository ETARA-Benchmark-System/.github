# Quick Start
In order to run ETARA several configurations must be done first. The cloned project has to be opened (currently) in an IDE of your choice. This step will be replaced soon by simply providing an executable jar file. Afterwards, two steps need to be performed: (1) Creating access to the used data sources and (2) providing initial configurations to simulate Web APIs, i.e., response templates, data sources and more.

## Creating Access to Data Sources
A Web API is esentially a wrapper around a database. The Web API is used as interface to make a database accessible to other users (in a controlled manner). The reason why Web APIs are so popular is because they seem to be a sweet-spot between making data openly accessible and protecting it. Thus, in order to use ETARA and simulate Web APIs, the databases to which the simulated APIs are to provide an interface must first be downloaded and registered in the system.

### Download of RDF Data Sources
The ETARA benchmark system provides nine different data sets of bibliographic and filmographic domains. The bibliographic set contains sample data sets (in RDF format) extracted from dblp, ArXiv, CrossRef, Semantic Scholar and Springer Nature, consisting of meta data of several important conferences and journals (e.g. SIGIR, SIGMOD, CIKM, etc.) from different years (2014 and 2015). We intentionally created small sets because this makes them easier to manually analyze and understand. The bibliographic data sets contain information about titles, publication years, author names, institutions, references and citations. For legal reasons information like abstracts is not provided in the data sets. 

The filmographic set contains meta data of movies created between 2000 and 2020 and covers samples from Linked Movie Database, Open Movie Database and The Movie Database. The data sets cover titles, release dates, actor names, director names and others. For legal reasons information about the movie plot are not provided in the data sets.

**Downloads**
* Bibliographic Data Sets: [[cloud](https://basilika.uni-trier.de/nextcloud/s/jwzxYgJ6Bp8K8Rz)] [[zenodo](https://www.startpage.com)]
* Filmographic Data Sets: [[cloud](https://basilika.uni-trier.de/nextcloud/s/sGS86e2WGANayzz)] [[zenodo](https://www.startpage.com)]

### Registering Data Sources
To simulate APIs, several requirements needs to be met. First, ETARA needs access to databases that represent the pool of available data for the simulated APIs. Currently, ETARA is only able to process RDF databases, but this aspect will be extended in the future. By registering a database, ETARA can access it and allow the simulated APIs to access the data and respond to requests with actual data. 

| ![db_overview](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/000fbb52-d1e8-47eb-a305-7b765ebaac51) | 
|:--:| 
| **Figure 1:** Overview of Databases |

Figure 1 presents an exemplary overview of all databases registered in the ETARA system. In the overview some (but not all) information of each database is displayed. First, the name or label of the database is displayed. This represents the unique name of the database in the system and is used to reference it, e.g., if a simulated API will use it as a data source. Moreover, it displays the location of the stored index and the identifier map, which will be explained in detail in the next section. If users click the edit button, the detail view is displayed, which is shown in Figure 2.

| ![db_details](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/ac979a63-c011-4be4-9f12-ee03100573b5) |
|:--:| 
| **Figure 2:** Detailed View of a Registered Database |

The view gives access to a few configuration options a database, e.g. source files, index path and the location of the indentifier map. In this example, we opened the detailed view of dblp. The path field describes the path to the database index, in this case a TDB index. The source field points to the raw text file of dblp (dblp.nt). The access to the raw data is needed because ETARA initially generates a so-called identifier map. This is a mapping between the URI formatted relations (predicates) of an RDF file and a short keyword. Typically, the suffix specifies the keyword, but this can be renamed by the user. The identifier map is initially created when ETARA is run for the first time, if it does not already exist. A more detailed explanation of the purpose of the Indentifier Map is not necessary for this section. If you want to learn more about it, read [here](documentation.md).

## Download and Use Initial Configurations
After users have registered their databases, they can be used to simulate Web APIs. In order to use ETARA as quickly as possible, only a short overview is given in the following. The ETARA benchmark system provides 42 API configurations, including response templates with different structures and granularity. Moreover, many of the provided templates are based on real world APIs, like ArXiv, CrossRef, Semantic Scholar, Springer Nature, Open Movie Database and The Movie Database. More information about the provided data and response templates can be found [here](/profile/documentation.md).

### Download Configurations (ETARA Hub)
The ETARA Hub is a repository that provides several different categories of Web API configurations, e.g. for bibliographic APIs like CrossRef, for filmographic APIs like the Open Movie Database, more complex JSON response structures, API configurations that respond to request errors with an HTTP status code, and much more. More information about the ETARA Hub can be found [here](etara-hub.md).

We would like to encourage all users of the ETARA Benchmark System to add the API configurations developed for their own tests to the repository and make them available for other developers and researchers. 

**Downloads**
* Api Configurations: [[hub](https://github.com/ETARA-Benchmark-System/ETARA-Hub)]

### Import of Configurations
At the current time, it is unfortunately not possible to import predefined Web API configurations via ETARA's web interface. Instead, the configurations have to be copied into the correct folders of the ETARA project. The following image shows an overview of all ETARA project files.

| ![etara_files](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/81116086-2a4f-49ad-a24a-89ee61b78b18) |
|:--:| 
| **Figure 3:** Overview of ETARA Project Files |

The ETARA project files consist of three folders (`client`, `configs` and `res`), a file to customize various startup configurations and an executable JAR file. For this part, we will only discuss the `client` folder in more detail. More information about ETARAs project files can be found [here](documentation.md). All Web API configurations downloaded from ETARA Hub must be moved to the `configs\webservices\` folder to be recognized by ETARA as Web APIs to be simulated. Afterwards, all further configurations can be done via ETARA's web interface again. 

### Short Explanation of a Web API Configuration 
After users have registered their databases and have imported some predefined Web API configurations, they can be used to simulate APIs. Figure 4 shows a short overview of all simulated Web APIs, i.e., their labels, the web path under which they can be accessed, their status and an overview of all possible actions.

| ![api_overview](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/42aec325-1d93-4516-8192-309c867becfb) |
|:--:| 
| **Figure 4:** Overview of Simulated API Configurations |

The first button opens a menu for editing all options (see Figure 5) and the following two buttons are used for duplicating and deleting the settings. Especially the option to duplicate an API configuration is very useful in the beginning and to make small changes in the API without having to change all settings again.

| ![detailed_api](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/561bfc66-c744-407b-828e-1c9974f311b0) |
|:--:| 
| **Figure 5:** General API Configuration Options |

Figure 5 shows an example of all configuration options. After specifying a label for the simulated API (see Figure 5, marker 1), users must specify the path (URL) which is used to request the API (see marker 2). Next, they select the database to use (see marker 3) and the average response time (see marker 4). Moreover, users can configure the rate limit (see marker 5) which defines the number of requests per minute and day. Since the APIs being simulated are RESTful Web APIs, data is requested via HTTP Get requests. When a client requests a specific resource on a Web server using the HTTP protocol, the client submits certain GET parameters to the server with the requested URL. These parameters are pairs of names and corresponding values. They are appended to the URL with the $?$ character followed by a parameter name and tell the server which resources are meant. The parameter name to which the simulated API responds can be configured through the interface (see marker 6).

The most complex configuration is to make valid (SPARQL) queries to the database, extract desired information and insert it into the given response template. For this purpose, users can specify one or more triple patterns that are used to identify a subject in the database (see marker 7). In the example shown in Figure 5, the database *sample_crossref* is searched for a subject that has a relation named *doi* and refers to the value of the parameter named *doi*. The found subject (an entity) is then used to fill the response template, using Apache FreeMarker, with information about the entity (e.g. the title of a publication). A detailed explanation of FreeMarker can be found [here](documentation.md).

| ![advanced_api](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/3cdb9202-dd25-4fbb-bf12-e2840b09301b) |
|:--:| 
| **Figure 6:** Advanced Configuration Options |

In addition to the classic configuration options such as rate limit or latency, users are able to control more complex behaviors of APIs. The "Search Type" option in Figure 6 specifies the search method to be used. There are two search options to choose from: *precise* and *fuzzy*.

The *precise* parameter sets APIs to only return data that was requested. For example, if an API receives a request containing an arxiv ID, the corresponding publication is searched. If it exists, the found publication entity is forwarded to the response template as described before. However, if no publication with the searched ID exists, no result can be returned. 

The *fuzzy* parameter enables an approximate search. This allows to return search results that have a certain degree of semantic overlap with the query. This option was implemented because some APIs behave like a classic Web search and return the best results for the query. For example, when passing a title instead of an ID, such behavior may be desirable. 

Furthermore, users can configure the type of error handling. For this, the "Error Type" option provides three possible parameters: *HTTP Status Code*, *JSON With Status Code* and *JSON Without Status Code*. By selecting *HTTP Status Code*, the simulated API responds with an HTTP status code including an error description, which provides information about the nature of the error. If the *JSON With Status Code* parameter is used, the API sends a JSON object with attribute-value pairs describing the error code. Additionally, an HTTP status code is appended to the response. By *JSON Without Status Code*, only a JSON object containing a description of the error code is sent. These three options cover all the usual ways a server handles errors or unsuccessful requests.

## Start ETARA
After all configurations have been imported, ETARA can be executed using an IDE (for example IntelliJ or Eclipse) or the executable JAR file. After running ETARA, all imported API configurations are then started and simulated. An example of such a simulation can be seen in the following screenshot.

|  ![etara_start](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/7f7b43cc-9f5e-4516-8196-cb5186f3cd6f) |
|:--:| 
| **Figure 7:** Start via Console |

The simulated APIs are located under the base domain `http://localhost:8080` and can be requested via the respective paths, for example `http://localhost:8080/webservices/testapi1/work`. Executing a GET request (for example `http://localhost:8080/webservices/testapi1/work?doi=10.1007/s11192-013-0954-3`) causes the simulated API a0 to issue a query to the database used, parse the query result and respond according to the template specifications. An example of such a response looks like the following:

| ![response_example](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/73e7240c-5438-43f5-8bfc-21566b94ccbb) |
|:--:| 
| **Figure 8:** Web API Response Example |
