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
Apache FreeMarker is a Java library and template engine. It is used to generate dynamic text output, e.g., JSON, XML, etc., based on a generalized template file. Java is used to query, clean and provide data to the template engine, which uses the given templates to dynamically create a text output, e.g. a JSON file that contains the response to an HTTP request. This approach follows a model view controller pattern (MVC) and is particularly popular in Web frameworks like Angular, React or Vue. The FreeMarker template language provides conditional blocks, iterations, assignments, string and arithmetic operations and formatting, macros, functions and many more. The engine enables that Java objects are exposed to the template as a tree of variables, so that it can use the variables to insert them at the appropriate place in the template and thus create a text file containing data.

| ![response_template](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/21c955dd-d055-49da-a6c9-20eadde41e62) |
|:--:| 
| **Figure 4:** Example of a Response Template |

Figure 4 shows an example of the integration of the Apache FreeMarker template engine into the ETARA interface. While in Figure 2 the configuration of an API was shown (accessible via the form in Figure 4, marker 1), this section deals with the configuration and creation of a return template (accessible via the form in Figure 4, marker 2). The template is in JSON format, which means that the API to be simulated will respond using JSON objects. 

The (SPARQL) query explained in the previous section requests an entity (subject) in the database of the API. Then all information about this entity is collected and passed to FreeMarker in the form of a tree structured Java object. Afterwards, the pre-built functionalities of FreeMarker can be used to parse the Java object, filter needed information and insert it into the template. 

An example is given in Figure 4. In this template, the Java object passed contains all information that is stored in the database about a publication. Line 2 of Figure 4 shows an easy example of how a value can be passed to the template. In this case the publication year of the requested publication is inserted as value for the `published-print` entry in the JSON template. The same approach is followed in the line 3 to 5 for titles, publication types and others. Line 6 is the first line that contains a more complex statement, i.e., an if condition. Most publications have only one title, however, it can happen that the title of a publication is simply to long and therefore authors can specify a shorter version of the title. To avoid generating an empty entry for `short-title` with every request, a simple if-query can be used to check whether a short title exists for the publication or not. In case of existence the short title can be inserted afterwards. Line 10 provides a similar approach but this case we will insert the every time an `URL` entry into the JSON response. The only thing that is conditional is the value of the response. Here, the templating engine will insert the URL that leads to the requested publication if this information is available. Otherwise the templating engine will just enter the value `n/a`. 

Besides if conditions, there are of course other control structures like loops. In line 11 you can see how a list of subject keywords is iterated over and each one is inserted into a `subject` array. For example, author names, actor names and others can be inserted into a given template. However, the most powerful features of FreeMarker are the so-called [Built-Ins](https://freemarker.apache.org/docs/ref_builtins_alphaidx.html). These are predefined functions that can be used to change or check the data that is inserted. 

| ![example_builtins](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/5a31ab78-b6f1-4207-a981-0af16c221dc5) |
|:--:| 
| **Figure 5:** Example of a Built Ins (split()) |

For example there are Built-Ins to check if strings start with a certain prefix, if substrings are contained and more. Furthermore it is possible to manipulate the data itself, for example by using a split, trim or remove method as shown in Figure 5. Here, the name of an author (e.g., "Bob Miller") is split into parts (e.g., "Bob" and "Miller"). With the use of `keep_before` and `keep_after_last` we kan create a response template that distinguishes between first and last names. This gives the possibility to create various individual response structures with only one database.

---
[Next: External Web API Management](https://github.com/ETARA-Benchmark-System/.github/blob/main/profile/external_management.md)
