# Markers Cyprus 2021 

## URL

The markers' results are served on the following URL:
 https://am-pilot.sinergise.com/dione/CY21/markers?foiRefId={foiRefId}

## Request

There is only one available API call. We can get all the computed markers for a parcel by passing in a foiRefId. Example request for FOI with foiRefId=6343-26/52--34~3:
 https://am-pilot.sinergise.com/dione/CY21/markers?foiRefId=6343-26%2F52--34~3

```
Note that parcel reference id (refId) in Cyprus is alphanumeric and can include some special characters, e.g. # or /. The refId needs to be encoded before querying the service.
```

## Markers served

| markerTypeId   | Marker                                       |
| -------------- | -------------------------------------------- |
| CY21.CL_MT.106 | Mowing                                       |
| CY21.CL_MT.102 | Mean NDVI from Feb - March 2021              |
| CY21.CL_MT.108 | Homogeneity                                  |
| CY21.CL_MT.110 | Similarity                                   |
| CY21.CL_MT.109 | Distance                                     |
| CY21.CL_MT.111 | Crop group classification (Original groups): |
| CY21.CL_MT.113 | Crop group classification (41 groups)        |
| CY21.CL_MT.114 | crop group classification (39 groups)        |
| CY21.CL_MT.112 | Land use group classification                |
| CY21.CL_MT.105 | Baresoil                                     |

Crop list and mappings found in [the code-lists folder of this repository.](code-lists/Cyprus/)

## Description of the served attributes for each Marker

### Mowing

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.106" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `eventStart`: start date of mowing event
- `eventEnd`: end date of mowing event
- `impl`: "EVENT" (internal)
- `duration`: duration of the mowing event in days
- `ndviBottom`: lowest NDVI value within the event_start - event_end interval
- `ndviEnd`: NDVI value at the end of the mowing event
- `numObservations`: number of valid observations within event_start - event_end interval
- `ndviStart`: NDVI value at the start of the mowing event
- `bottomTimestamp`: timestamp of the lowest NDVI value within event_start - event_end interval
- `ndviDrop`: difference between ndvi_start and ndvi_bottom

### Mean NDVI from Feb - March 2021

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.102" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `value`: Mean NDVI value of all valid observations per FOI
- `impl`: "AGGREGATION" (internal)

### Homogeneity

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.108" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: `hypothesisCode` with the highest `score`
- `classificationScore`: score of the most probable assumed `hypothesisCode`
- `markerScores`: 
  - `hypothesisCode`: assumed homogeneity/non-homogeneity of FOI ("homogeneous", "heterogeneous")
  - `score`: the normalised ([0, 100]) representation of probability of the hypothesis being true

- `impl`: "CLASSIFICATION" (internal)

### Similarity

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.110" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: most similar crop type (crop id)
- `classificationId`: most similar crop type (internal crop id)
- `declaredAsCode`: declared crop type (crop id)
- `declaredAsId`: declared crop type (internal crop id)
- `classificationScore`: `score` of the most similar crop type
- `markerScores`: 
  - `hypothesisCode`: assumed crop type of target FOI (based on neighboring FOIs)
  - `hypothesisId`: assumed crop type of target FOI (internal crop id)
  - `score`: the normalised ([0, 100]) representation of the chi2 value of the NDVI time-series difference between the target FOI and the neighboring FOIs

- `impl`: "CLASSIFICATION" (internal)

### Distance

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.109" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: most similar crop type (crop id)
- `classificationId`: most similar crop type (internal crop id)
- `declaredAsCode`: declared crop type (crop id)
- `declaredAsId`: declared crop type (internal crop id)
- `classificationScore`: `score` of the most similar crop type
- `markerScores`: 
  - `hypothesisCode`: assumed crop type of target FOI (based on neighboring FOIs)
  - `hypothesisId`: assumed crop type of target FOI (internal crop id)
  - `score`: the normalised ([0, 100]) representation of the Median Euclidean distance between the NDVI time-series of the target FOI and the neighboring FOIs having assumed crop type declared

- `impl`: "CLASSIFICATION" (internal)
- `sameCropCount`: number of all neighbouring FOIs with the same declared crop type as the target FOI

### Crop group classification

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.111" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: assumed crop group with the highest confidence
- `declaredAsCode`: declared crop group (mapped from the declared crop type)
- `classificationScore`: `score` of the likeliest assumed crop group
- `markerScores`:
  - `hypothesisCode`: Assumed crop group
  - `score`: confidence in the assumed crop group (value between 0 and 100)

- `impl`: "CLASSIFICATION" (internal)

### Crop group classification (test, with 41 groups)

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.113" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: assumed crop group with the highest confidence
- `declaredAsCode`: declared crop group (mapped from the declared crop type)
- `classificationScore`: `score` of the likeliest assumed crop group
- `markerScores`:
  - `hypothesisCode`: Assumed crop group
  - `score`: confidence in the assumed crop group (value between 0 and 100)
- `impl`: "CLASSIFICATION" (internal)

### Crop group classification (test, with 39 groups)

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.114" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: assumed crop group with the highest confidence
- `declaredAsCode`: declared crop group (mapped from the declared crop type)
- `classificationScore`: `score` of the likeliest assumed crop group
- `markerScores`:
  - `hypothesisCode`: assumed crop group
  - `score`: confidence in the assumed crop group (value between 0 and 100)
- `impl`: "CLASSIFICATION" (internal)

### Land use group classification

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.112" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: assumed land use group with the highest confidence
- `declaredAsCode`: declared land use group
- `classificationScore`: `score` of the likeliest assumed land use group
- `markerScores`:
  - `hypothesisCode`: assumed land use group
  - `score`: confidence in the assumed land use group (value between 0 and 100)
- `impl`: "CLASSIFICATION" (internal)

### Baresoil

- `id`: marker id (internal)
- `markerTypeId`: "CY21.CL_MT.105" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `observationCount`: count of all FOI's bare-soil observations
- `markerObservations`:
  -  `date`: signal acquisition date
  - `confidence`: confidence in the observation being bare-soil

- `impl`: "OBSERVATION"

