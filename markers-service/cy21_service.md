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