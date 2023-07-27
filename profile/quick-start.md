# Quick Start
In order to run ETARA several configurations must be done first. The cloned project has to be opened (currently) in an IDE of your choice. This step will be replaced soon by simply providing an executable jar file. Afterwards, two steps need to be performed: (1) Creating access to the used data sources and (2) providing initial configurations to simulate Web APIs, i.e., response templates, data sources and more.

## Creating Access to Data Sources
A Web API is esentially a wrapper around a database. The Web API is used as interface to make a database accessible to other users (in a controlled manner). The reason why Web APIs are so popular is because they seem to be a sweet-spot between making data openly accessible and protecting it. Thus, in order to use ETARA and simulate Web APIs, the databases to which the simulated APIs are to provide an interface must first be downloaded and registered in the system.

### Download of RDF Data Sources
The ETARA benchmark system provides nine different data sets of bibliographic and filmographic domains. The bibliographic set contains sample data sets (in RDF format) extracted from dblp, ArXiv, CrossRef, Semantic Scholar and Springer Nature, consisting of meta data of several important conferences and journals (e.g. SIGIR, SIGMOD, CIKM, etc.) from different years (2014 and 2015). We intentionally created small sets because this makes them easier to manually analyze and understand. The bibliographic data sets contain information about titles, publication years, author names, institutions, references and citations. For legal reasons information like abstracts is not provided in the data sets. 

The filmographic set contains meta data of movies created between 2000 and 2020 and covers samples from Linked Movie Database, Open Movie Database and The Movie Database. The data sets cover titles, release dates, actor names, director names and others. For legal reasons information about the movie plot are not provided in the data sets.

**Downloads**
* Bibliographic Data Sets: [[cloud](https://www.startpage.com)] [[zenodo](https://www.startpage.com)]
* Filmographic Data Sets: [[cloud](https://www.startpage.com)] [[zenodo](https://www.startpage.com)]

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
* Api Configurations: [[hub](https://www.startpage.com)] [[zenodo](https://www.startpage.com)]

### Import of Configurations

### Short Explanation of a Web API Configuration 
| ![api_overview](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/42aec325-1d93-4516-8192-309c867becfb) |
|:--:| 
| **Figure 3:** Overview of Simulated API Configurations |

| ![detailed_api](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/0d386b6f-ec02-4fba-aa67-0be4313a6766) |
|:--:| 
| **Figure 4:** General API Configuration Options |

| ![advanced_api](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/3cdb9202-dd25-4fbb-bf12-e2840b09301b) |
|:--:| 
| **Figure 5:** Advanced Configuration Options |

## Start ETARA
After all configurations have been imported, ETARA can be executed using an IDE (for example IntelliJ or Eclipse) or the executable JAR file. After running ETARA, all imported API configurations are then started and simulated. An example of such a simulation can be seen in the following screenshot.

|  ![etara_start](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/7f7b43cc-9f5e-4516-8196-cb5186f3cd6f) |
|:--:| 
| **Figure 6:** Start via Console |

The simulated APIs are located under the base domain `http://localhost:8080` and can be requested via the respective paths, for example `http://localhost:8080/webservices/crossref/work`. Executing a GET request (for example `http://localhost:8080/webservices/crossref/work?q=10.1007/s11192-013-0954-3`) causes the simulated version of the crossref API to issue a query to the database used, parse the query result and respond according to the template specifications. An example of such a response looks like the following:

| ![response_example](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/e1df3159-8b92-4e62-8dcb-e062bf097e6e) |
|:--:| 
| **Figure 7:** Web API Response Example |
