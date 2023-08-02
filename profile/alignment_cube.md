# Alignment Cube
Alignment Cube allows an interactive visual exploration and evaluation of alignments. It is possible to analyze alignments on the level of individual correspondences. Since it was initially designed for dense dynamic networks in the first place, an advantage consists of its scalability. Hence, it allows to visualize the performance history of an alignment system and therefore allows a comparison of the alignment results of a system when different parameters are tuned or core algorithms are changed.

## Basic Interpretation
As described in detail by [Ivanova et al.](https://link.springer.com/chapter/10.1007/978-3-319-68288-4_24) two ontologies and their alignment can be seen as a bipartite network of mappings between individual concepts in two different ontologies. Hence, a matrix represents a single alignment between two ontologies/schemas. We have modified this definition slightly and consider rows as relations from an underlying RDF database and columns as paths in the JSON or XML responses of an API in our implementation. This change makes it easy to apply the principle behind alignment cubes to alignments between RDF databases and RESTful Web APIs. Stacking several matrices, i.e., several alignments, creates an Alignment Cube.

| ![alignment_cube](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/8c45272e-e8ee-44b0-bddc-7064e99f9d6b) |
|:--:| 
| **Figure 1:** 3D View of the Alignment Cube |

TO BE DONE

| ![history_layer](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/0f23dce4-fcd6-4748-abd8-ab90701a4053) |
|:--:| 
| **Figure 2:** History Layer |

| ![api_view](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/1e0e169c-ff9d-47cd-9a79-6c4b11b433b1) |
|:--:| 
| **Figure 3:** API Path View |

| ![db_view](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/215792fd-498a-4e4c-933e-157a6e17e0a6) |
|:--:| 
| **Figure 4:** RDF Relation View |

## Example Evaluation
TO BE DONE

| ![evaluation_layers](https://github.com/ETARA-Benchmark-System/.github/assets/4719393/bb2cf079-dada-4dd7-9e1b-98cc9e089a46) |
|:--:| 
| **Figure 5:** Gold Standard Layer, FiLiPo Layer and DORIS Layer |
