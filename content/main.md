---
weight: 10
title: API Reference
---

# Mangal

[The Mangal project](http://www.mangal.io) aims at archiving published ecological networks and at
easing their retrieval. The database includes 172 datasets representing over [1300 ecological
networks](http://poisotlab.biol.umontreal.ca/#/). This documentation is meant to describe all the
the endpoints and parameters to developers who would like to use the Mangal RESTFul API. 

# Authentication

Authentification is mandatory only for `POST`, `PUT` & `DELETE` operations. We used an OAuth 2.0 strategy to secure the Mangal API services exploiting [ORCID](https://orcid.org/) as a third party authentification service. The authentification procedure will be described soon (in the meantime, if you have question feel free to send email at steve.vissault[at]usherbrooke.ca). We are currently developing templates to facilitate the conversion and publication of new ecological networks into mangal.

**All `GET` methods don't require any authentification**.

# Endpoints

Below, we briefly describe the content of each endpoint.


| Endpoint       | Content description                                                         |
|----------------|-----------------------------------------------------------------------------|
| `\reference`   | Reference to the original publications (e.g. doi, bibtex, authors etc.)     |
| `\dataset`     | Metadata on the networks collection (e.g. generic description)              |
| `\network`     | Metadata on the network collected (e.g. data and sampling location).        |
| `\node`        | Informations on the individu, taxa or population involved in the network    |
| `\interaction` | Direction, type, strength of the interaction among two nodes                |
| `\taxonomy`    | Homogeneized and cleanup taxonomy with gbif, eol, col, itis, bold, ncbi IDs |
| `\trait`       | Trait variables available for a node or taxon (generic traits)              |
| `\environment` | Environment variables collected at the sampling data and location           |
| `\attribute`   | Variables used to describe interaction, trait, environment                  |



**Full database diagram:** [Download](https://raw.githubusercontent.com/mangal-wg/mangal-api/master/mangal_dev.png)

# Generic parameters

Generic parameters applicable for `GET` method

| Parameter | Description                                                       | Exemple                                                        |
|-----------|-------------------------------------------------------------------|----------------------------------------------------------------|
| `q`       | Full search within the table, **only working on string columns**. | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?q=%insect%` |
| `sort`    | Sort specific column                                              | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?sort=-id`   |
| `page`    | Request specific page                                             | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?page=0`     |
| `count`   | Number of entries returned (max. 1000)                            | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?count=50`   |

# References

## GET Method

```javascript
import axios

axio.get('http://poisotlab.biol.umontreal.ca/api/v2/reference')
  .then((res) => {
    console.log(res.data)
  })

```
```shell
curl "http://poisotlab.biol.umontreal.ca/api/v2/reference"
```

> Output exemple

```json
[
  {
    "id": 1,
    "doi": "10.5962/bhl.title.11538",
    "author": "roberson",
    "year": "1929",
    "jstor": null,
    "pmid": null,
    "bibtex": "@book{bhl43820, title = {Flowers and insects; lists of visitors of four hundred and fifty-three flowers,  }, copyright = {Public domain.  Published 1923-1963 with notice but no evidence of copyright renewal found in Stanford Copyright Renewal Database.  Contact dcc@library.uiuc.edu for information.}, url = {https://www.biodiversitylibrary.org/item/43820}, publisher = {Carlinville, Ill.,n.p.}, author = {Robertson, Charles,}, year = {}, pages = {234}, keywords = {Bees|Fertilization of plants|Flowers|Illinois|Insects|Macoupin County|}}",
    "paper_url": "https://www.biodiversitylibrary.org/bibliography/11538#/summary",
    "data_url": "https://www.nceas.ucsb.edu/interactionweb/html/robertson_1929.html",
    "created_at": "2019-02-21T21:17:04.520Z",
    "updated_at": "2019-02-21T21:17:04.520Z"
  },
  {
    "id": 9,
    "doi": "10.2307/3683041",
    "author": "elberling",
    "year": "1999",
    "jstor": "3683041",
    "pmid": null,
    "bibtex": "@article{10.2307/3683041, ISSN = {09067590, 16000587}, URL = {http://www.jstor.org/stable/3683041}, author = {Heidi Elberling and Jens M. Olesen}, journal = {Ecography}, number = {3}, pages = {314-323}, publisher = {[Nordic Society Oikos, Wiley]}, title = {The Structure of a High Latitude Plant-Flower Visitor System: The Dominance of Flies}, volume = {22}, year = {1999}}",
    "paper_url": "https://www.jstor.org/stable/3683041?seq=1#page_scan_tab_contents",
    "data_url": "https://www.nceas.ucsb.edu/interactionweb/data/plant_pollinator/excel/elberling&olesen_1999.xls",
    "created_at": "2019-02-22T20:09:13.872Z",
    "updated_at": "2019-02-22T20:09:13.872Z"
  }
]
```

### HTTP Request

List all references available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/reference`

Request specific reference `id`

`GET http://poisotlab.biol.umontreal.ca/api/v2/reference/:id`

### Specific parameters

| Parameter | Description                         | Exemple                                                                   |
|-----------|-------------------------------------|---------------------------------------------------------------------------|
| `doi`     | Search by Digital Object Identifier | `http://poisotlab.biol.umontreal.ca/api/v2/reference?doi=10.2307/3683041` |
| `author`  | Search by first author              | `http://poisotlab.biol.umontreal.ca/api/v2/reference?author=kolpelke`     |
| `year`    | Search by year of publication       | `http://poisotlab.biol.umontreal.ca/api/v2/reference?year=2007`           |
| `jstor`   | Search by JSTOR ID                  | `http://poisotlab.biol.umontreal.ca/api/v2/reference?jstor=3683041`       |

# Datasets

## GET Method

```javascript
import axios

axio.get('http://poisotlab.biol.umontreal.ca/api/v2/dataset')
  .then((res) => {
    console.log(res.data)
  })

```
```shell
curl "http://poisotlab.biol.umontreal.ca/api/v2/dataset"
```

> Output exemple

```json
[{
  "id": 2,
  "name": "howking_1968",
  "date": "1963-06-01T04:00:00.000Z",
  "description": "Insect activity recorded 
    on flower at Lake Hazen, Ellesmere Island, 
    N.W.T., Canada",
  "public": true,
  "created_at": "2019-02-22T15:39:00.427Z",
  "updated_at": "2019-02-22T15:39:00.427Z",
  "ref_id": 2,
  "user_id": 2
}, {
  "id": 7,
  "name": "lundgren_olesen_2005",
  "date": "2002-08-04T04:00:00.000Z",
  "description": "Pollnator activity 
    recorded on flowers, Uummannaq Island, Greenland, Danmark",
  "public": true,
  "created_at": "2019-02-22T20:04:25.322Z",
  "updated_at": "2019-02-22T20:04:25.322Z",
  "ref_id": 7,
  "user_id": 2
}]
```

### HTTP Request

List all datasets available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset`

Request specific dataset `id`

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset/:id`

### Specific parameters

| Parameter     | Description                                            | Exemple                                                                     |
|---------------|--------------------------------------------------------|-----------------------------------------------------------------------------|
| `name`        | Search by unique name (`firstAuthor_pubYear`)          | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?name=howking_1968`       |
| `date`        | Search by creation date -- format `YYYY-mm-dd`         | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?date=1963-06-01`         |
| `description` | Full text search in description                        | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?description=%Ellesmere%` |
| `ref_id`      | Retrieve all datasets attached to a specific reference | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?ref_id=7`                |


# Networks

## GET Method

```javascript
import axios

axio.get('http://poisotlab.biol.umontreal.ca/api/v2/network')
  .then((res) => {
    console.log(res.data)
  })

```
```shell
curl "http://poisotlab.biol.umontreal.ca/api/v2/network"
```

> Output exemple

```json
[
  {
    "id": 1246,
    "name": "havens_1992_19840601_1246",
    "date": "1984-06-01T04:00:00.000Z",
    "geom": {
      "type": "Point",
      "coordinates": [
        -74.1672222222222,
        44.4875
      ]
    },
    "description": "Food web of pelagic communities of small lakes and ponds of the Lost Lake.",
    "public": true,
    "all_interactions": true,
    "created_at": "2019-02-27T02:23:11.329Z",
    "updated_at": "2019-03-03T18:54:57.168Z",
    "dataset_id": 15,
    "user_id": 3
  },
  {
    "id": 1247,
    "name": "havens_1992_19840601_1247",
    "date": "1984-06-01T04:00:00.000Z",
    "geom": {
      "type": "Point",
      "coordinates": [
        -74.2838888888889,
        44.4619444444444
      ]
    },
    "description": "Food web of pelagic communities of small lakes and ponds of the .",
    "public": true,
    "all_interactions": true,
    "created_at": "2019-02-27T02:23:11.573Z",
    "updated_at": "2019-03-03T18:54:57.302Z",
    "dataset_id": 15,
    "user_id": 3
  },
  {
    "id": 1227,
    "name": "havens_1992_19840601_1227",
    "date": "1984-06-01T04:00:00.000Z",
    "geom": {
      "type": "Point",
      "coordinates": [
        -75.0555555555556,
        43.5277777777778
      ]
    },
    "description": "Food web of pelagic communities of small lakes and ponds of the Chub Pond.",
    "public": true,
    "all_interactions": true,
    "created_at": "2019-02-27T02:23:05.598Z",
    "updated_at": "2019-03-03T20:54:21.148Z",
    "dataset_id": 15,
    "user_id": 3
  }
]
```

### HTTP Request

List all networks available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/network`

Request specific network `id`

`GET http://poisotlab.biol.umontreal.ca/api/v2/network/:id`

### Specific parameters

| Parameter          | Description                                                                | Exemple                                                                   |
|--------------------|----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| `public`           | The network is publicly available                                          | `http://poisotlab.biol.umontreal.ca/api/v2/network?public=false`          |
| `all_interactions` | If `true`, absence of interactions can be considered as real/true absences | `http://poisotlab.biol.umontreal.ca/api/v2/network?all_interactions=true` |
| `dataset_id`       | Retrieve all networks attached to a specific dataset                       | `http://poisotlab.biol.umontreal.ca/api/v2/network?dataset_id=12`         |


# Nodes

## GET Method

```javascript
import axios

axio.get('http://poisotlab.biol.umontreal.ca/api/v2/node')
  .then((res) => {
    console.log(res.data)
  })

```
```shell
curl "http://poisotlab.biol.umontreal.ca/api/v2/node"
```

> Output exemple

```json
[
  {
    "id": 6447,
    "original_name": "insects",
    "node_level": "taxon",
    "network_id": 926,
    "taxonomy_id": 4650,
    "created_at": "2019-02-25T15:09:24.658Z",
    "updated_at": "2019-02-25T15:09:24.658Z",
    "taxonomy": {
      "id": 4650,
      "name": "Insecta",
      "ncbi": 50557,
      "tsn": 4703,
      "eol": 344,
      "bold": 82,
      "gbif": null,
      "col": "ae304a1e0beadcfec04932589049bb5a",
      "rank": "class",
      "created_at": "2019-02-24T18:56:42.545Z",
      "updated_at": "2019-06-14T15:25:59.300Z"
    }
  },
  {
    "id": 6448,
    "node_level": "taxon",
    "original_name": "Callinectes",
    "network_id": 926,
    "taxonomy_id": 3823,
    "created_at": "2019-02-25T15:09:24.701Z",
    "updated_at": "2019-02-25T15:09:24.701Z",
    "taxonomy": {
      "id": 3823,
      "name": "Callinectes",
      "ncbi": 6762,
      "tsn": 13951,
      "eol": 46508442,
      "bold": 4985,
      "gbif": null,
      "col": "8c9d5b7b0ef67ba0ca49a80b06665541",
      "rank": "genus",
      "created_at": "2019-02-22T14:55:39.819Z",
      "updated_at": "2019-06-14T15:25:29.810Z"
    }
  }
]
```

### HTTP Request

List all nodes available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/node`

Request specific node `id`

`GET http://poisotlab.biol.umontreal.ca/api/v2/node/:id`

<aside class="success">
<code>/node</code> will always return also <code>/taxonomy</code>. The nested <code>taxonomy</code> JSON referred to the taxonomic informations of the node.
</aside>

### Specific parameters

| Parameter          | Description                                                                | Exemple                                                                   |
|--------------------|----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| `original_name`           | Search by taxon or IDs defined by the original author of the publication (exact match)                                     | `http://poisotlab.biol.umontreal.ca/api/v2/node?original_name=insects`          |
| `node_level` | Search by sampling unit with 3 options: population, taxon, individu | `http://poisotlab.biol.umontreal.ca/api/v2/node?node_level=population` |
| `network_id`       | Retrieve all nodes attached to a specific network                       | `http://poisotlab.biol.umontreal.ca/api/v2/node?network_id=926`         |


# Interactions

## GET Method

```javascript
import axios

axio.get('http://poisotlab.biol.umontreal.ca/api/v2/interaction')
  .then((res) => {
    console.log(res.data)
  })

```
```shell
curl "http://poisotlab.biol.umontreal.ca/api/v2/interaction"
```

> Output exemple

```json
[
  {
    "id": 98124,
    "node_from": 24589,
    "node_to": 24554,
    "date": "1983-01-01T00:00:00.000Z",
    "direction": "directed",
    "type": "herbivory",
    "method": "gut content",
    "attr_id": 33,
    "value": 8,
    "geom": null,
    "public": true,
    "network_id": 1474,
    "created_at": "2019-03-05T20:56:11.109Z",
    "updated_at": "2019-03-05T20:56:11.109Z",
    "attribute": {
      "id": 33,
      "name": "number of individuals in gut",
      "description": "Number of individuals in the gut content during analysis",
      "unit": "NA",
      "created_at": "2019-03-04T17:11:22.765Z",
      "updated_at": "2019-03-04T17:11:22.765Z"
    }
  },
  {
    "id": 98427,
    "node_from": 24628,
    "node_to": 24633,
    "date": "2004-04-01T00:00:00.000Z",
    "direction": "directed",
    "type": "predation",
    "method": "stable isotopes and gut content",
    "attr_id": 25,
    "value": 1,
    "geom": null,
    "public": true,
    "network_id": 1488,
    "created_at": "2019-03-06T14:52:01.494Z",
    "updated_at": "2019-03-06T14:52:01.494Z",
    "attribute": {
      "id": 25,
      "name": "presence/absence",
      "description": "Presence or absence of interaction",
      "unit": "NA",
      "created_at": "2019-03-01T16:03:38.993Z",
      "updated_at": "2019-03-01T16:03:38.993Z"
    }
  }
]
```

### HTTP Request

List all interactions available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/interaction`

Request specific interaction `id`

`GET http://poisotlab.biol.umontreal.ca/api/v2/interaction/:id`

<aside class="success">
<code>/interaction</code> will always return also <code>/attribute</code> used to quantify the strength of the interaction. <code>attribute.name</code> is the variable associated with <code>value</code> in the interaction table.
</aside>

### Specific parameters

| Parameter          | Description     | Exemple                                                                   |
|--------------------|----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| `node_from` | Search by node id which the interaction originate from (e.g. predator) | `http://poisotlab.biol.umontreal.ca/api/v2/interaction?node_from=24628` |
| `node_to` | Search by node id which the interaction end to (e.g. prey) | `http://poisotlab.biol.umontreal.ca/api/v2/interaction?node_to=24633` |
| `direction`           | Search by edge direction. 3 options: directed, undirected or unknown                                     | `http://poisotlab.biol.umontreal.ca/api/v2/interaction?direction=unknown`          |
| `type` | Search by ecological interaction types from the following options: competition, amensalism, neutralism, commensalism, mutualism, parasitism, predation, herbivory, symbiosis, scavenger, detritivore, unspecified, consumption  | `http://poisotlab.biol.umontreal.ca/api/v2/interaction?type=predation` |
| `attr_id`       | Retrieve all interactions described by a specific attribute                 | `http://poisotlab.biol.umontreal.ca/api/v2/interaction?attr_id=25`         |
| `network_id`       | Retrieve all interactions attached to a specific network                       | `http://poisotlab.biol.umontreal.ca/api/v2/interaction?network_id=926`         |


# Taxonomy

## GET Method

```javascript
import axios

axio.get('http://poisotlab.biol.umontreal.ca/api/v2/taxonomy')
  .then((res) => {
    console.log(res.data)
  })

```
```shell
curl "http://poisotlab.biol.umontreal.ca/api/v2/taxonomy"
```

> Output exemple

```json
[
  {
    "id": 2,
    "name": "Acer negundo",
    "ncbi": 4023,
    "tsn": 28749,
    "eol": 583069,
    "bold": 100987,
    "gbif": 3189866,
    "col": "90203e29e2f59e5754167f89b9eba3cc",
    "rank": "species",
    "created_at": "2019-02-21T21:17:12.585Z",
    "updated_at": "2019-06-14T15:20:36.273Z"
  }, {
    "id": 3,
    "name": "Acer saccharinum",
    "ncbi": 75745,
    "tsn": 28757,
    "eol": 583072,
    "bold": 101028,
    "gbif": 3189837,
    "col": "1582ed5db846e241f3e18da418a2a477",
    "rank": "species",
    "created_at": "2019-02-21T21:17:12.637Z",
    "updated_at": "2019-06-14T15:20:36.328Z"
  }, {
    "id": 5317,
    "name": "Uria aalge",
    "ncbi": 13746,
    "tsn": 176974,
    "eol": 45509343,
    "bold": 10149,
    "gbif": 2481342,
    "col": "1f21d6d69cb8c09be9a27485d68bc4d1",
    "rank": "species",
    "created_at": "2019-02-27T04:10:09.559Z",
    "updated_at": "2019-06-14T15:26:37.498Z"
  }
]
```

### HTTP Request

List all taxonomy items available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/taxonomy`

Request specific taxonomic `id`

`GET http://poisotlab.biol.umontreal.ca/api/v2/taxonomy/:id`


### Specific parameters

| Parameter          | Description     | Exemple                                                                   |
|--------------------|----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| `name` | Search by taxonomic name (exact match) | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?name=Uria aalge` |
| `ncbi` | Search by unique taxonomic identifier from [National Center for Biotechnology Information](https://www.ncbi.nlm.nih.gov/) | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?ncbi=13746` |
| `tsn`           | Search by unique taxonomic identifier from [Integrated Taxonomic Information Sytem](https://www.itis.gov/) | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?tsn=176974`          |
| `eol` | Search by unique taxonomic identifier from [Encyclopedia of Life](https://eol.org/) | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?eol=583072` |
| `bold`       | Search by unique taxonomic identifier from [Barcode of Life](http://www.boldsystems.org/)               | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?bold=10149`         |
| `gbif`       | Search by unique taxonomic identifier from [Global Biodiversity Information Facility](https://www.gbif.org/)                      | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?gbif=2481342`         |
| `col`       | Search by unique taxonomic identifier from [Catalogue of Life](https://www.catalogueoflife.org/)                       | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?col=1f21d6d69cb8c09be9a27485d68bc4d1`         |
| `rank`       | Retrieve all nodes with a specific taxonomic resolution from the list: kingdom, subkingdom, infrakingdom, superdivision, division, subdivision, phylum, class, superorder, order, superfamily, family, genus, subgenus, species, infraspecies                  | `http://poisotlab.biol.umontreal.ca/api/v2/taxonomy?rank=class`         |

# Attributes

## GET Method

```javascript
import axios

axio.get('http://poisotlab.biol.umontreal.ca/api/v2/attribute')
  .then((res) => {
    console.log(res.data)
  })

```
```shell
curl "http://poisotlab.biol.umontreal.ca/api/v2/attribute"
```

> Output exemple

```json
[
    {
        "id": 40,
        "name": "dietary matrix",
        "description": "Proportions of the consumer diets made up by the prey.",
        "unit": "NA",
        "created_at": "2019-03-27T09:20:44.990Z",
        "updated_at": "2019-03-27T09:20:44.990Z"
    },
    {
        "id": 41,
        "name": "body size",
        "description": "Average body length",
        "unit": "mm",
        "created_at": "2019-03-28T20:27:51.716Z",
        "updated_at": "2019-03-28T20:27:51.716Z"
    },
    {
        "id": 42,
        "name": "habitat use",
        "description": "Which type of habitat is used by the species (aquatic/terrestrial/both)",
        "unit": "NA",
        "created_at": "2019-04-10T15:01:59.318Z",
        "updated_at": "2019-04-10T15:01:59.318Z"
    }
]
```

### HTTP Request

List all attributes items available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/attribute`

Request specific attribute `id`

`GET http://poisotlab.biol.umontreal.ca/api/v2/attribute/:id`
