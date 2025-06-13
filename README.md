# MLESmapService
This repository contains the MLESmap demonstrator developed for the ChEESE project (Deliverable 5.2) for Simulation Case 1.3.3.

MLES (ML based estimator for and from earthquakes' ground shaking) is a set of Machine Learning based estimators for the forward inference of ground shaking maps.
MLESmap aims at providing ground accelerations in a given region a few seconds after a large magnitude earthquake occurs. It relies on an ML engine trained on large catalogs of physics-based seismic simulations. The training data includes earthquake hypocenters, magnitude, seismological recording station locations and values of ground accelerations obtained from those seismological stations or via catalogs of physics-based seismic simulations. The trained ML model is a Multilayer Perceptron (MLP) based regression. It provides forward inference as PSA values at station locations.

##  Repository content
- `MLESmapDemostrator.ipynb` - Main notebook with inferences and visualisations.
- `Model_Iceland_3layers_8Feat_pSA_1_Batch100_Epoch15.h5` - ML model trained for 1s period used in the notebook
- `scaler_X_1s.save`, `scaler_y_1s.save` - Scalers used for the inference in the notebook.
- `LICENSE.md`- License of the repository
- `README.me`

## General structure of the notebook
The main cells of the `MLESmapDemostrator.ipynb` notebook are described below:

- **Seismic event definition:**
 The parameters of the event to be inferred (latitude, longitude, magnitude and depth) have to be specified.

- **Model and scaler loading:**
 The ML model (`.h5`) and the `scaler_X` and `scaler_y` scalers are loaded with `joblib`.

- **Station grid generation:**
 A regular grid of receiver sites within the study area (lat/lon min and max) is created.

- **Calculation of distances and features:**
 Euclidean distance and azimuth between the event and each station are calculated using `turfpy`, and the input dataset is formed.

- **Data scaling and inference:**
 Normalise the input variables with `scaler_X`. Predictions are made with the model loaded and results are de-scaled using `scaler_y`.

- **Post-processing and geospatial visualization:**
 Results are stored in the final DataFrame `df_event`, ready for analysis or visualisation. The intensity map is created using `xarray`, `griddata`, `cartopy` and `matplotlib`.


## License
This project is licensed under the terms specified in the LICENSE file.
