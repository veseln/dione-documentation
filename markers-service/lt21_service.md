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

