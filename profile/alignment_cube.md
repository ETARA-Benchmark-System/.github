# Alignment Cube
Alignment Cube allows an interactive visual exploration and evaluation of alignments. It is possible to analyze alignments on the level of individual correspondences. Since it was initially designed for dense dynamic networks in the first place, an advantage consists of its scalability. Hence, it allows to visualize the performance history of an alignment system and therefore allows a comparison of the alignment results of a system when different parameters are tuned or core algorithms are changed.

## Loading Alignments
In order to fill the Alignment Cube with data, the data to be visualized must first be selected, as shown in Figure 1. With the button "Add Gold Standard" a Gold Stand Alignment, created with ETARA's Gold Standard Builder, can be added as a data set. With the button "Upload Alignment" alignments from other systems can be loaded.

| ![alignment_selection](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/a5c61d01-3858-47b2-ba2d-dbef50757d67) |
|:--:| 
| **Figure 1:** Selection of Gold Standard Alignments |

Figure 2 shows an overview of the loaded alignments. It shows with which system the alignments have been created and how many mappings are contained in the alignments. With the button "Generate Alignment Cube" the loaded alignments can be visualized.

| ![alignment_selection_3](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/f2c0d78b-bb84-4e0e-ac41-c6c1b6d4a486) |
|:--:| 
| **Figure 2:** Uploading External Alignments |

## ETARAs Alignment Format
In the following, the ETARA alignment format is represented as a JSON schema.This is a declarative language that allows you to annotate and validate JSON documents. The advantage of a JSON schema is the clear structure and a possibility to clearly describe the ETARA alignment format. Furthermore, it provides a clear human- and machine-readable documentation. This allows us to validate the loaded alignments in an automated way.

```
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://example.com/alignment.schema.json",
  "type": "object",
  "properties": {
    "name": {
      "type": "string"
    },
    "system":{
      "type": "string"
    },
    "description": {
      "type": "string"
    },
    "alignments": {
      "type": "array",
      "items": {
        "$ref": "#/definitions/mapping"
      }
    }
  },
  "required": [
    "name",
    "alignments"
  ],

  "definitions": {
    "mapping": {
      "type": "object",
      "properties": {
        "api_path": {
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "relation_path": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/relationPath"
          }
        },
        "metrics": {
          "type": "object",
          "patternProperties": {
            "": {
              "type": "number"
            }
          }
        }
      },
      "required": [
        "api_path",
        "relation_path",
        "metrics"
      ]
    },
    "relationPath": {
      "type": "object",
      "properties": {
        "path": {
          "type": "array",
          "items": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

An example of a valid alignment is given in the following example. It consists of two mappings between the relation `title` and `title` and `publishedAsPartOf -> title` and `container-title`.

```
{
    "system": "System A",
    "alignments": [
        {
            "metrics": {
              "confidence": 1,
              "data_availability": 1
            },
            "relation_path": [{"path": ["https://www.example.com/publication#title"]}],
            "api_path": ["title"]
        },
        {
            "metrics": {
              "confidence": 1,
              "data_availability": 0.5
            },
            "relation_path": [{"path": [
                "https://www.example.com/publication#publishedAsPartOf",
                "https://www.example.com/publication#title"
            ]}],
            "api_path": ["container-title"]
        }
    ],
    "name": "System A: movieDb - movieApi"
}
```

The ETARA Alignemnt scheme allows many different metrics.In the example above, two metrics are captured. On the one hand the metric `confidence`, which indicates how secure system A is with this mapping and on the other hand `data_availability`, which describes how often this field occurs in a JSON response. This flexible design makes it possible to visualize and use different metrics in the alignment cube.

It is similar with the mappings themselves.It is possible to create simple 1:1 mappings, such as `title` and `title`, or more complex 1:1 mappings that require traversing the knowledge base first.An example of this is the mapping `title` and `publishedAsPartOf -> title`.

## Basic Interpretation
As described in detail by [Ivanova et al.](https://link.springer.com/chapter/10.1007/978-3-319-68288-4_24) two ontologies and their alignment can be seen as a bipartite network of mappings between individual concepts in two different ontologies. Hence, a matrix represents a single alignment between two ontologies/schemas. We have modified this definition slightly and consider rows as relations from an underlying RDF database and columns as paths in the JSON or XML responses of an API in our implementation. This change makes it easy to apply the principle behind alignment cubes to alignments between RDF databases and RESTful Web APIs. Stacking several matrices, i.e., several alignments, creates an Alignment Cube.

TO BE DONE

| ![alignment_cube](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/8c45272e-e8ee-44b0-bddc-7064e99f9d6b) |
|:--:| 
| **Figure 3:** 3D View of the Alignment Cube |

| ![history_layer](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/0f23dce4-fcd6-4748-abd8-ab90701a4053) |
|:--:| 
| **Figure 4:** History Layer |

| ![api_view](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/1e0e169c-ff9d-47cd-9a79-6c4b11b433b1) |
|:--:| 
| **Figure 5:** API Path View |

| ![db_view](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/215792fd-498a-4e4c-933e-157a6e17e0a6) |
|:--:| 
| **Figure 6:** RDF Relation View |

## Example Evaluation
In order to show how ETARAs Alignment Cube component can be used to evaluate two alignment systems this section will present an demonstrative evaluation of to alignment systems. The current state-of-the-art API alignment systems are [FiLiPo](#) and [DORIS](#). FiLiPo is a system which automatically finds an alignment between data provided by APIs and RDF databases. It is a sample-driven approach that models API services as parameterized queries. Furthermore, it is able to find valid input values for APIs automatically (e.g. IDs) and can determine valid alignments between RDF databases and APIs.

DORIS builds upon the schema of an RDF database and during the alignment process, it sends several requests to an API. Users only have to specify the input class for the API and a request limit. The input class specifies which form of entities the API responds to (e.g. publications).  Moreover, a key assumption of DORIS is that it is more likely to find information about popular entities (e.g. famous actors) via API calls. From this follows the assumption that KBs contain more facts of well-known entities and hence it ranks entities by descending number of facts. These entities will then be used for the alignment.

First, a gold standard alignment including the alignments determined by FiLiPo and DORIS must be loaded into the alignment cube component. The result is displayed in Figure 7 in the form of three layers of the alignment cube. Each layer represents one alignment, i.e., golst standard alignment, FiLiPos alignment and DORIS alignment.

| ![evaluation_layers](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/bb2cf079-dada-4dd7-9e1b-98cc9e089a46) |
|:--:| 
| **Figure 7:** Gold Standard Layer, FiLiPo Layer and DORIS Layer |

The next step is to interpret the results displayed in the alignment cube. The first noticeable aspect is that the goldstandard alignment, consisting of seven mappings, contains significantly more mappings than the alignment output of DORIS. DORIS was only able to find a mapping for the title and the publication year, which are easy to find, since the title and year values between the API and the dblp are almost identical. 

DORIS determines a mapping by comparing the values of the dblp and the API. To compare data values DORIS uses an equality method (ignoring punctuation and case). The drawback of this approach becomes clear when examining the other mappings of the GS alignment. Relations like *publishedIn*, *publishedInJournal* and *publishedAsPartOf -> title* store the conference or journal name, in which a publication was published. Through the manual creation of a gold standard alignment by using ETARA's gold standard builder, a deeper insight into the data can be gained. For example, during the mapping process we noticed that conference or journal titles of dblp and the created test API are very different. For example, an example conference title in dblp looks like this:

> Proceedings of the 23rd ACM International Conference on Conference on Information and Knowledge Management, CIKM 2014, Shanghai, China, November 3-7, 2014

In comparison, the created test API stores conference titles in the following form: 

> Proceedings of the 23rd ACM International on Conference on Information and Knowledge Management

Therefore DORIS is not able to identify these mappings. 

Compared to DORIS, Figure 7 shows that FiLiPo was able to determine a mapping between *publishedIn* and *container-title*. The reason is that FiLiPo uses a set of different similarity metrics and does not check for equality. However, a closer analysis shows that FiLiPo creates these mappings with low confidence values (size of the individual cubes). This indicates that either this mapping is very rare and therefore should be handled with care or (as in this case) that the mapping is not an exact mapping.

In addition to detailed analyses of the alignments and systems, ETARA also enables quick evaluations in the form of precision, recall, and f1-score. DORIS could only find two out of nine mappings and thus has a very low recall of 2/9 = 0.22. FiLiPo, in comparison, was able to achieve a recall of 9/9 = 1.0. Both systems had a precision of 1.0.
