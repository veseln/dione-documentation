# Markers Lithuania 2021

## URL

The markers' results are served on the following URL:
 https://am-pilot.sinergise.com/dione/LT21/markers?foiRefId={foiRefId}

## Example request

There is only one available API call. We can get all the computed markers for a parcel by passing in a foiRefId. Example request for FOI with foiRefId=19052076:

https://am-pilot.sinergise.com/dione/LT21/markers?foiRefId=19052076

## Markers served

| markerTypeId   | Marker                |
| -------------- | --------------------- |
| LT21.CL_MT.117 | Mean NDVI             |
| LT21.CL_MT.120 | Baresoil              |
| LT21.CL_MT.121 | Mowing                |
| LT21.CL_MT.123 | Homogeneity           |
| LT21.CL_MT.124 | Distance              |
| LT21.CL_MT.125 | Similarity            |
| LT21.CL_MT.126 | Crop group prediction |
| LT21.CL_MT.127 | Land group prediction |

Crop list and mappings found in [the code-lists folder of this repository.](code-lists/Lithuania/)

## Description of the served attributes for each Marker

### Mowing

- `id`: marker id (internal)
- `markerTypeId`: "LT21.CL_MT.121" (internal)
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

### Mean NDVI

- `id`: marker id (internal)
- `markerTypeId`: "LT21.CL_MT.117" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `value`: Mean NDVI value of all valid observations per FOI
- `impl`: "AGGREGATION" (internal)

### Homogeneity

- `id`: marker id (internal)
- `markerTypeId`: "LT21.CL_MT.123" (internal)
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
- `markerTypeId`: "LT21.CL_MT.125" (internal)
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
- `markerTypeId`: "LT21.CL_MT.124" (internal)
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
- `markerTypeId`: "LT21.CL_MT.126" (internal)
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
- `markerTypeId`: "LT21.CL_MT.127" (internal)
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

- `markerTypeId`: "LT21.CL_MT.120" (internal)

- `inferenceId`: inference id (internal)

- `foiId`: FOI (feature of interest) id (internal)

- `observationCount`: count of all FOI's bare-soil observations
  - `markerObservations`:
    -  `date`: signal acquisition date
    - `confidence`: confidence in the observation being bare-soil

- `impl`: "OBSERVATION"