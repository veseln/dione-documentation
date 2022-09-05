# Markers Cyprus 2022

## URL

The markers' results are served on the following URL:
https://am-pilot.sinergise.com/dione/CY22/markers?foiRefId={foiRefId}

## Request

There is only one available API call. We can get all the computed markers for a parcel by passing in a foiRefId. Example request for FOI with foiRefId=6363-26/37--109/1~40:
https://am-pilot.sinergise.com/dione/CY22/markers?foiRefId=6363-26%2F37--109%2F1~40

Note that parcel reference id (refId) in Cyprus is alphanumeric and can include some special characters, e.g. # or /. The refId needs to be encoded before querying the service.

## Markers served

| markerTypeId                             | Marker                         |
| ---------------------------------------- | ------------------------------ |
| CY22.CL_MT.S2L2A_MOWING                  | Mowing                         |
| CY22.CL_MT.S2L2A_AGGREGATION_MEAN_NDVI   | Mean NDVI from Apr - June 2022 |
| CY22.CL_MT.S2L2A_AGGREGATION_MEAN_NDVI_2 | Mean NDVI from Feb - Mar 2022  |
| CY22.CL_MT.S2L2A_AGGREGATION_MEAN_NDVI_3 | Mean NDVI from Jan - Apr 2022  |
| CY22.CL_MT.S2L2A_HOMOGENEITY             | Homogeneity                    |
| CY22.CL_MT.S2L2A_SIMILARITY              | Similarity                     |
| CY22.CL_MT.S2L2A_DISTANCE                | Distance                       |
| CY22.CL_MT.S2L2A_CROP_GROUP_PREDICTION   | Crop group prediction          |
| CY22.CL_MT.S2L2A_LAND_COVER              | land use group classification  |
| CY22.CL_MT.S2L2A_BARE_SOIL               | Baresoil                       |

Crop list and mappings found in [the code-lists folder of this repository.](code-lists/Cyprus/)

## Description of the served attributes for each Marker

### Mowing

- `id`: marker id (internal)
- `markerTypeId`: `CY22.CL_MT.S2L2A_MOWING`
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

### Mean NDVI from Apr - June 2022

- `id`: marker id (internal)
- `markerTypeId`: `CY22.CL_MT.S2L2A_AGGREGATION_MEAN_NDVI` 
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `value`: Mean NDVI value of all valid observations per FOI
- `impl`: "AGGREGATION" (internal)

### Mean NDVI from Feb - Mar 2022

- `id`: marker id (internal)
- `markerTypeId`: `CY22.CL_MT.S2L2A_AGGREGATION_MEAN_NDVI_2` 
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `value`: Mean NDVI value of all valid observations per FOI
- `impl`: "AGGREGATION" (internal)

### Mean NDVI from Jan - Apr 2022

- `id`: marker id (internal)
- `markerTypeId`: `CY22.CL_MT.S2L2A_AGGREGATION_MEAN_NDVI_3` 
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `value`: Mean NDVI value of all valid observations per FOI
- `impl`: "AGGREGATION" (internal)

### Homogeneity

- `id`: marker id (internal)
- markerTypeId: `CY22.CL_MT.S2L2A_HOMOGENEITY` 
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
- `markerTypeId`: `CY22.CL_MT.S2L2A_SIMILARITY`
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
- `markerTypeId`: `CY22.CL_MT.S2L2A_DISTANCE`
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
- `markerTypeId`: `CY22.CL_MT.S2L2A_CROP_GROUP_PREDICTION`
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: assumed crop group with the highest confidence
- `declaredAsCode`: declared crop group (mapped from the declared crop type)
- `classificationScore`: `score` of the likeliest assumed crop group
- `markerScores`:
  - `hypothesisCode`: Assumed crop group
  - `score`: confidence in the assumed crop group (value between 0 and 100)

- `impl`: "CLASSIFICATION" (internal)

### Land use group classification

- `id`: marker id (internal)
- `markerTypeId`: `CY22.CL_MT.S2L2A_LAND_COVER`
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
- `markerTypeId`: `CY22.CL_MT.S2L2A_BARE_SOIL` 
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `observationCount`: count of all FOI's bare-soil observations
- `markerObservations`:
  -  `date`: signal acquisition date
  -  `confidence`: confidence in the observation being bare-soil

- `impl`: "OBSERVATION"

