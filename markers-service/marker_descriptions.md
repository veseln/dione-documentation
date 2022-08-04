# Marker descriptions 

## Baresoil marker

The bare-soil marker identifies all observations with exposed bare soil due to field being recently plowed, or due to non-photosynthetic vegetation cover. The latter can be a consequence of a harvest or vegetation drying up on the field. The event itself, being plowing or harvest, cannot be detected in satellite imagery, but its consequences are observable. The bare-soil marker thus identifies plowing events by detecting exposed bare soil.

Bare-soil marker assigns bare-soil probability to each valid Sentinel-2 observation. All observations with bare-soil probability above user-defined threshold are declared as bare-soil observations.

More details about the marker in the [blogpost](https://medium.com/sentinel-hub/area-monitoring-bare-soil-marker-608bc95712ae).



## Homogeneity marker

Homogeneity marker identifies FOIs with inhomogeneous land use, like for example a FOI that covers a meadow and arable land growing corn, or a FOI that covers arable land only, but with two or more different crop types growing.

Signal of FOIs that are not homogeneous are by definition mixed, which can lead to wrong interpretation of other markers' results. For example FOI that covers meadow and arable land is at some point in season partly vegetated and in part of it bare soil can be exposed. Vegetation being present on a such FOI spoils the detection of bare soil and at the same time bare soil lowers the NDVI index that can be wrongly interpreted as a mowing event. FOIs that are not homogeneous in land use and don't grow a single crop type thus need to be flagged and reviewed by an expert.

More details about the marker in the [blogpost](https://medium.com/sentinel-hub/area-monitoring-homogeneity-marker-742047b834dc).

## Similarity and Euclidean distance markers



Similarity and Euclidean distance markers are from the group of crop classification markers. Output of both markers can be used to check validity of a FOI's claim. Both markers have in common that a FOI is compared to nearby FOIs. The way how the comparison is made is different between the two markers and briefly described below. Similarity and Euclidean distance markers  don't require any model training, which is their biggest advantage.

### Similarity marker

Similarity marker evaluates how *similar* a FOI is to other FOIs from its neighborhood having the same (or different) claim based on time series of Normalized Difference Vegetation Index (NDVI). For example, how similar is a cornfield to other cornfields in its vicinity? Similarity is calculated by comparing a FOI's NDVI time-series with average NDVI time-series of FOIs from its vicinity having the same (or different) claim. Comparison is therefore between a FOI and average of many other FOIs that are located near this FOI. Similarity marker assigns a score (a number) between 0 and 100 to each FOI and for each crop type hypothesis. Closer this score is to 100 for a crop type less similar FOI is to other FOIs with this crop type.

### Distance marker

Euclidean distance marker evaluates how *near* in Euclidean distance metric space a FOI is to other nearby FOIs. The distance is evaluated in the feature space defined by a FOIs' NDVI time-series. Unlike similarity marker the distance marker makes pair-wise FOI comparisons and provides summary metrics like mean distance to FOIs with same or any other crop-type claim. Euclidean  marker assigns a score (a number) between 0 and 100 to each FOI and for each crop type hypothesis. Closer this score is to 100 for a crop type larger the differences in NDVI time-series between a FOI and other FOIs with this crop type are. 

See more details about the similarity and distance markers in the [blogpost](https://medium.com/sentinel-hub/area-monitoring-similarity-score-72e5cbfb33b6).

## Mowing marker

The mowing marker identifies all observations where mowing events lead to a drop in the vegetation index values (NDVI). The mowing event itself cannot be detected via satellite imagery, but its consequences are observable. The marker identifies mowing events by identifying drops in the NDVI profile of features-of-interest (FOIs) claiming to be permanent meadows or growing grass, clover or grass/clover mixtures.

More details about the marker in the [blogpost](https://medium.com/sentinel-hub/area-monitoring-mowing-marker-e99cff0c2d08).

## Mean NDVI marker 

Mean NDVI marker is a simple marker, which can be used to identify outlier FOI candidates. For some crop types, mean NDVI can be low due to farming practices and crop properties, e.g. FOIs with green houses growing vegetables or other crops, while for others it is not. FOI claimed to be a meadow that has consistently low NDVI is most probably not a meadow and deserves an expert review.

## Crop and land  type markers

The consistency of FOI with its claimed crop type or land use can be tested with the crop or land classification markers. An LSTM neural network is trained to classify FOIs into  different crop or land types. 

The models are trained on a dataset consisting of farmer's declarations. The dataset was divided into 5 independent folds. 5 different models are trained. Each model is trained on 4 folds and used to make predictions for FOIs from the left-out independent fold. 

More details about the marker in the [blogpost](https://medium.com/sentinel-hub/area-monitoring-crop-type-marker-1e70f672bf44]).