# Markers Lithuania 2022

## URL

The markers' results are served on the following URL:
https://am-pilot.sinergise.com/dione/LT22/markers?foiRefId={foiRefId}

## Example request

There is only one available API call. We can get all the computed markers for a parcel by passing in a foiRefId. Example request for FOI with foiRefId=20993162:

https://am-pilot.sinergise.com/dione/LT22/markers?foiRefId=20993162

## Markers served

| markerTypeId                             | Marker                                              |
| ---------------------------------------- | --------------------------------------------------- |
| LT22.CL_MT.S2L2A_CROP_GROUP_PREDICTION   | Crop group prediction                               |
| LT22.CL_MT.S2L2A_CROP_GROUP_PREDICTION_2 | Crop group prediction (using an alternate grouping) |
| LT22.CL_MT.S2L2A_MOWING                  | Mowing detection                                    |

Crop list and mappings found in [the code-lists folder of this repository.](code-lists/Lithuania/)

## Description of the served attributes for each Marker

### Mowing

- `id`: marker id (internal)
- `markerTypeId`: "LT22.CL_MT.S2L2A_MOWING" (internal)
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

### Crop group classifications

- `id`: marker id (internal)
- `markerTypeId`: "LT22.CL_MT.S2L2A_CROP_GROUP_PREDICTION" (internal)
- `inferenceId`: inference id (internal)
- `foiId`: FOI (feature of interest) id (internal)
- `classificationCode`: assumed crop group with the highest confidence
- `declaredAsCode`: declared crop group (mapped from the declared crop type)
- `classificationScore`: `score` of the likeliest assumed crop group
- `markerScores`:
  - `hypothesisCode`: Assumed crop group
  - `score`: confidence in the assumed crop group (value between 0 and 100)
- `impl`: "CLASSIFICATION" (internal)

#### Alternate grouping

We tried to mitigate the problem of mixing groups by training another model using a training dataset where certain individual crops were grouped together into groups.

| Crops                                                        | Group                    |
| ------------------------------------------------------------ | ------------------------ |
| `Perennial pastures or meadows 5 years and more`, `Pasture or meadow, perennial grass up to 5 years` | **Pastures and Meadows** |
| `Winter triticale`, `Winter barley`, `Winter wheat`, `Winter rye` | **Winter cereals**       |
| `Spring wheat`, `Spring barley`                              | **Spring cereals**       |