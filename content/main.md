---
weight: 10
title: API Reference
base: test
---

# API Documentation

Application Programming Interface (API) to support [Mangal.io](http://poisotlab.biol.umontreal.ca/#/), an ecological interactions database. 

# Authentication

Authentification is mandatory only for `POST`, `PUT` & `DELETE` operations. We use the ORCID authentification service. Registration is open and accessible at [http://poisotlab.biol.umontreal.ca/auth](http://poisotlab.biol.umontreal.ca/auth). We are currently developing templates to facilitate the conversion and publication of new ecological networks into mangal.

`GET` doesn't require authentification. If you have any question, please email me steve.vissault[at]usherbrooke.ca


# Endpoints

| Endpoint | Content description                                                     |
|----------|-------------------------------------------------------------------|
| `\reference`   | Original publications (doi, bibtex, authors etc.)                                              |
| `\dataset`      | Collection of networks |
| `\network`   | Network collected at specific location and date.                                              |
| `\node`  | Individu, taxa or population involved in the network                |
| `\interaction`  | Directed or undirected interaction among two nodes                |
| `\taxonomy`  | Homogeneized taxonomy / unique identifier from gbif, eol, col, itis, bold, ncbi            |
| `\trait`  |     Trait variables from a node or taxon (generic traits)           |
| `\environment`  | Environment variables attached to a network             |
| `\attribute`  | Variables use to describe interaction, trait, environment            |

[Download DB diagram](https://raw.githubusercontent.com/mangal-wg/mangal-api/master/mangal_dev.png)

# Generic parameters

Generic parameters applicable for `GET` method

| Parameter    | Description | Exemple                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| `q` | Full search within the table, **only working on string columns**.     | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?q=%insect%`                              |
| `sort`    | Sort specific column    | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?sort=-id` |
| `page`    | Request specific page    | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?page=0` |
| `count`    | Number of entries returned (max. 1000)    | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?count=50` |

# Datasets

## Get all datasets

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

### Parameters

| Parameter    | Description | Exemple                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| `name` | Search by unique name (`firstAuthor_pubYear`) | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?name=howking_1968`                             |
| `date` | Search by creation date -- format `YYYY-mm-dd` | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?date=1963-06-01`                             |
| `description`    | Full text search in description    | `http://poisotlab.biol.umontreal.ca/api/v2/dataset?description=%Ellesmere%`      |
# References

## Get all datasets

### HTTP REQUEST

List all datasets available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset`

Request specific entry based on the id

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset/:id`


### Parameters

| Parameter    | Description | Exemple                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| q | false   | If set to true, the result will also include cats.                               |
| sort    | true    | If set to false, the result will include kittens that have already been adopted. |
| page    | true    | If set to false, the result will include kittens that have already been adopted. |

# Networks

## Get all datasets

### HTTP REQUEST

List all datasets available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset`

Request specific entry based on the id

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset/:id`


### Parameters

| Parameter    | Description | Exemple                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| q | false   | If set to true, the result will also include cats.                               |
| sort    | true    | If set to false, the result will include kittens that have already been adopted. |
| page    | true    | If set to false, the result will include kittens that have already been adopted. |

# Nodes

## Get all datasets

### HTTP REQUEST

List all datasets available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset`

Request specific entry based on the id

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset/:id`


### Parameters

| Parameter    | Description | Exemple                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| q | false   | If set to true, the result will also include cats.                               |
| sort    | true    | If set to false, the result will include kittens that have already been adopted. |
| page    | true    | If set to false, the result will include kittens that have already been adopted. |

# Interactions

## Get all datasets

### HTTP REQUEST

List all datasets available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset`

Request specific entry based on the id

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset/:id`


### Parameters

| Parameter    | Description | Exemple                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| q | false   | If set to true, the result will also include cats.                               |
| sort    | true    | If set to false, the result will include kittens that have already been adopted. |
| page    | true    | If set to false, the result will include kittens that have already been adopted. |

# Taxonomy

## Get all datasets

### HTTP REQUEST

List all datasets available in mangal

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset`

Request specific entry based on the id

`GET http://poisotlab.biol.umontreal.ca/api/v2/dataset/:id`


### Parameters

| Parameter    | Description | Exemple                                                                      |
|--------------|---------|----------------------------------------------------------------------------------|
| q | false   | If set to true, the result will also include cats.                               |
| sort    | true    | If set to false, the result will include kittens that have already been adopted. |
| page    | true    | If set to false, the result will include kittens that have already been adopted. |
