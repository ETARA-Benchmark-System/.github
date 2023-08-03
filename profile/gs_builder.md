# Gold Standard Builder
To evaluate automatically created alignments a GS alignment is required. Hence, ETARA provides a set of GS alignments for the given data sets and APIs. Moreover, it provides a component to support the creation of GS alignments. The GS builder consists of four delineated phases: (1) data selection, (2) response preparation, (3) data mapping and (4) final alignment adjustments.

## Data Selection
The first step is data selection, shown in Figure 1, is the selection of the RDF database that users want to align with a Web API. In the example shown in Figure 1, the dblp was chosen as RDF database. However, this option alone is not enough, because the choice of the Web API with which the dblp is aligned has some side effects. 

| ![selection](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/17795ac7-262e-410a-b354-0f919a6da47a) |
|:--:| 
| **Figure 1:** Data and Web API Selection |

For example, you can see that in Figure 1 an API named "Simulated API for OM2023" has been selected as the Web API. This Web API expects DOIs from publications as a request and can then respond with various metadata in the form of a JSON response. In order for the "correct" data to be sent from the dblp as a request to the Web API, users must specify this information. In the example shown, it was selected that only entities with the type or class `Publication` should be used as requests. However, this specification alone is not selective enough, since other IDs such as ISBNs, arvix IDs and others can also be used for queries. Therefore, users must also specify an input relation that will be used to form the queries. In the example in Figure 1, the relation `P356`, which points to a DOI, is selected.

## Response Preparation
The next phase is response preparation, shown in Figure 2, where the response schema of a Web API is to be cleaned of irrelevant components, such as metadata about the request itself. The deleted components of the response are then removed from all requests to avoid burdening the gold standard designer with unnecessary information.

| ![response_preparation](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/795f0cbc-1c5b-46df-91d8-2d54864d9b45) |
|:--:| 
| **Figure 2:** Response Preparation |


## Data Mapping
The third and most significant phase (data mapping) provides a variety of functions (e.g., search/sort relation names, search/sort values, etc.) to find mappings between the data of a single entity from an RDF database and the response of an API. The selected entity is always chosen randomly from the RDF database to cover a wide variety of entities which leads to a wide range of possible mappings.

| ![mapping_phase_components](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/1431c38b-ba4d-4230-b222-86ca5a8b3fc8) |
|:--:| 
| **Figure 3:** Mapping Phase |

As shown in Figure 3, the mapping component consists of three main sections: (1) the data that the RDF database stores for an entity, (2) the data that is sent as a response from the Web API, and (3) a section for creating mappings. In the upper section of the areas (1) and (2) options are given to sort the data (both the relation names and the values themselves) and to search for keywords. After two mappings are identified by the users, for example the relation `yearOfPublication` and `print-date`, they can specify the form of the mapping. 

In principle, two types of mappings are distinguished: (1) equivalent mappings and (2) subsumption mappings. Equivalent mappings are easy to understand because, as the name suggests, they are mappings that store the same data. An example of this are the mappings `yearOfPublication` and `print-date` as well as `title` and `title` in Figure 3. To create such a mapping you only have to click on the two fields `yearOfPublication` and `print-date` and connect them via the middle arrow button in area (3). 

Subsumption mappings are simply mappings between two relations that are not equivalent and contain only a subset of the information. For example, the RDF relation `label` in Figure 3 consists of author information, the title of the publication, and the year. There is no way to create an equivalent mapping on the JSON response side, but the value of `title` is part of `label` and therefore `label` can be said to subsume `title`. To create a subsumption mapping, users have the two arrow buttons on the left and right in area (3). This allows them to specify the "direction" of the mapping, for example whether `label` subsumed `title` (i.e., `<-`) or `title` subsumed `label` (i.e., `->`).

| ![highlights](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/7a222ee4-858c-4d96-814a-021a53243c6a) |
|:--:| 
| **Figure 4:** Highlighting New Relations |

After all mappings for a single entity between the RDF database and the Web API response have been determined, users can call the next entity and determine further mappings. The more mappings a user specifies, the more accurate the final alignment, as it ensures that the data does not contain any outliers, but also that rarer relations, data errors, or any edge cases in general are discovered. To highlight users new relations, which were not present in the previous mapping attempts, are marked in green as shown in Figure 4. This way, relations that appear for the first time are not simply "lost" and can even be searched for specifically.

## Final Alignment Adjustments

TO BE DONE

| ![preliminary_alignment](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/f6222d99-6831-441a-a043-1fdc59c83ab5) |
|:--:| 
| **Figure 5:** Preliminary Alignment |

|  | 
|:--:| 
| **Figure 6:** Alignment Adjustments |
