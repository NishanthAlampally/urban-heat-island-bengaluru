# Urban Heat Island Predictor — Bengaluru

A geospatial machine learning project investigating urban heat islands in Bengaluru, India, using Landsat satellite imagery and environmental indices. The project combines remote sensing, feature engineering, gradient-boosted regression, and spatial analysis to predict land surface temperature and explore potential urban cooling interventions.

The current implementation analyses a single Landsat scene from April 2025. **Time-series modelling is a planned extension** to investigate how urban heat patterns evolve over time.

## Objectives

- Estimate land surface temperature (LST) across Bengaluru using satellite-derived environmental features.
- Investigate the relationship between vegetation, built-up areas, surface characteristics, and temperature.
- Train a machine learning model to predict land surface temperature.
- Identify high-temperature hotspots and explore potential cooling interventions.
- Extend the analysis to multiple satellite acquisitions to study temporal trends in urban heat.

## Methodology

### 1. Satellite Data Processing

Processes Landsat 8 Level-2 imagery, including surface reflectance and surface temperature bands. Quality masks are applied to exclude unsuitable pixels, and the imagery is clipped to Bengaluru's geographical boundary.

### 2. Feature Engineering

Derives environmental and spectral features, including:

- **NDVI:** Normalized Difference Vegetation Index
- **NDBI:** Normalized Difference Built-up Index
- **MNDWI:** Modified Normalized Difference Water Index
- **ALBEDO:** Estimated surface reflectance
- **BSI:** Bare Soil Index
- **EMIS:** Surface emissivity
- **Spatial coordinates:** Normalised pixel row and column coordinates

Land surface temperature is derived from the Landsat thermal data and used as the prediction target.

### 3. Machine Learning

An XGBoost regression model predicts land surface temperature from the engineered features.

The dataset is split by spatial tiles rather than individual pixels to reduce leakage from neighbouring pixels between training and test sets. Model performance is evaluated using:

- \(R^2\)
- Root Mean Squared Error (RMSE)

### 4. Feature Importance

SHAP-based analysis is included to investigate the contribution of different environmental and spatial features to model predictions.

### 5. Cooling Intervention Analysis

Explores hypothetical cooling scenarios involving tree planting and green roofs in high-temperature areas. The trained model estimates changes in predicted surface temperature under modified feature assumptions.

These results are exploratory model-based estimates, not measurements of actual intervention outcomes.

### 6. Ward-Level Analysis

Aggregates temperature and predicted cooling statistics across Bengaluru's administrative wards to investigate spatial differences in heat exposure.

An interactive map visualises ward-level temperature patterns and selected cooling metrics.

## Time-Series Extension — Planned

The next stage of the project will extend the single-scene analysis to multiple satellite acquisitions across time.

Potential directions include:

- Building a consistent time series of land surface temperature across Bengaluru.
- Analysing seasonal and longer-term changes in urban heat patterns.
- Tracking the evolution of hotspots across administrative wards.
- Investigating temporal relationships between vegetation, urbanisation, and surface temperature.
- Developing time-series forecasting models where the available data supports reliable validation.

This extension will require consistent preprocessing across dates, cloud and quality masking, and careful handling of seasonal variation and missing observations.

## Technology Stack

- Python
- NumPy and Pandas
- Rasterio
- GeoPandas
- OSMnx
- Matplotlib
- Scikit-learn
- XGBoost
- SHAP
- Folium

## Project Status

- [x] Landsat scene preprocessing
- [x] Environmental feature engineering
- [x] XGBoost regression
- [x] Spatially separated train/test split
- [x] Predicted temperature visualisation
- [x] Exploratory cooling intervention scenarios
- [x] Ward-level spatial analysis
- [x] Interactive mapping
- [ ] Multi-date satellite data integration
- [ ] Time-series analysis and forecasting
- [ ] Temporal model evaluation

## Limitations

The current model uses a single Landsat acquisition and therefore does not establish seasonal or long-term temperature trends. Predictions and cooling scenarios depend on the selected features, training data, and modelling assumptions. Further validation across dates and locations is necessary before interpreting predictions as generalisable temperature estimates or intervention effects.

## License

This project is licensed under the MIT License. See `LICENSE` for details.
