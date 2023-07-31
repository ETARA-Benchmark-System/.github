# Database Management
To simulate APIs, several requirements needs to be met. First, ETARA needs access to databases that represent the pool of available data for the simulated APIs. Currently, ETARA is only able to process RDF databases, but this aspect will be extended in the future. By registering a database, ETARA can access it and allow the simulated APIs to access the data and respond to requests with actual data. 

| ![db_overview](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/000fbb52-d1e8-47eb-a305-7b765ebaac51) | 
|:--:| 
| **Figure 1:** Overview of Databases |

Figure 1 presents an exemplary overview of all databases registered in the ETARA system. In the overview some (but not all) information of each database is displayed. First, the name or label of the database is displayed. This represents the unique name of the database in the system and is used to reference it, e.g., if a simulated API will use it as a data source. Moreover, it displays the location of the stored index and the identifier map, which will be explained in detail in the next section. If users click the edit button, the detail view is displayed, which is shown in Figure 2.

## Detailed Configurations
| ![db_details](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/ac979a63-c011-4be4-9f12-ee03100573b5) |
|:--:| 
| **Figure 2:** Detailed View of a Registered Database |

The detail view (of the dblp knowledge base) gives access to a few configuration options of a database, e.g. source files, index path and the location of the indentifier map. The path field describes the path to the database index (e.g., a TDB Index or SPARQL endpoint). The source field points to the raw text file of the dblp knowledge base (dblp.nt). The access to the raw data is needed because of two reasons:

TO BE DONE
