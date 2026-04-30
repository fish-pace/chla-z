# CHLA-Z: Global Chlorophyll-a Vertical Distribution (0–200 m)

**CHLA-Z** is a global gridded dataset providing estimates of chlorophyll-a concentration as a function of depth (0–200 m) on a latitude/longitude grid, along with derived vertical-structure metrics such as integrated chlorophyll, peak chlorophyll, peak depth, and center-of-mass depth.

The product is derived from a boosted regression tree (BRT) model trained on in-situ chlorophyll profile observations from Bio-Argo and OOI using PACE OCI Level-3 mapped remote-sensing reflectances (Rrs) as predictors.

CHLA-Z is intended for use in ocean productivity, ecosystem, and fisheries applications where the vertical structure of phytoplankton matters.

---

## Dataset Summary

| Field | Value |
|------|------|
Product name | CHLA-Z
Version | v1
Format | Zarr v3 (cloud-optimized)
Processing level | L4 derived product
Temporal coverage | 2024-03-01 to 2025-09-30
Temporal resolution | Daily
Spatial coverage | Global
Spatial resolution | ~4 km (0.0416667°)
Vertical range | 0–200 m
Vertical resolution | 10 m bins
Coordinate system | Latitude / Longitude (Equidistant Cylindrical)

---

## Data Access

### HTTPS

```
https://storage.googleapis.com/nmfs_odp_nwfsc/CB/fish-pace-datasets/chla-z/zarr
```

### Google Cloud Storage

```
gs://nmfs_odp_nwfsc/CB/fish-pace-datasets/chla-z/zarr
```

---

## Open the Dataset in Python

Use the `gcs://` URL with anonymous access.

```python
import xarray as xr

zarr_url = "gcs://nmfs_odp_nwfsc/CB/fish-pace-datasets/chla-z/zarr"
ds = xr.open_zarr(zarr_url, consolidated=False, 
          storage_options={"token": "anon"})
```

Make a plot

```python
# Example: time series at a point (nearest grid cell)
pt = ds["CHLA"].sel(lon=-155, lat=20, method="nearest")
pt = pt.isel(z=0) # surface
pt.sel(time=slice("2024-03-01", "2024-04-01")).plot()
```

---

## Variables

Primary variables include:

- **CHLA** — Chlorophyll-a concentration on depth bins (mg m⁻³)
- **CHLA_int_0_200** — Integrated chlorophyll-a (0–200 m) (mg m⁻²)
- **CHLA_peak** — Peak chlorophyll-a value (mg m⁻³)
- **CHLA_peak_depth** — Depth of peak chlorophyll-a (m)
- **CHLA_depth_center_of_mass** — Center-of-mass depth of chlorophyll-a (m)
- **z_thickness** — Thickness of vertical bins (m)

---

## Intended Use

This dataset supports applications including:

- Ocean productivity analysis
- Fisheries ecosystem studies
- Phytoplankton vertical structure
- Subsurface chlorophyll maximum detection
- Marine habitat modeling
- Ocean biogeochemistry research

---

## Data Processing Overview

CHLA-Z is generated using a machine learning workflow:

1. Bio-Argo and OOI provide in-situ chlorophyll profiles
2. PACE OCI Level-3 reflectance data provide satellite predictors
3. A boosted regression tree (BRT) model estimates chlorophyll at depth
4. Derived vertical metrics are computed from predicted profiles
5. Outputs are stored as a cloud-optimized Zarr v3 dataset

---

## Citation

If you use this dataset, please cite:


Holmes, E. E. (2026). CHLA-Z: Global chlorophyll-a vertical distribution (0–200 m) derived from PACE OCI and Bio-Argo (draft) (0.1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.18204005


---

## Acknowledgment

Please acknowledge:

- NASA PACE / OBPG for PACE OCI satellite inputs
- The Bio-Argo program for in-situ profile observations
- NOAA Fisheries (NMFS) and the Fish-PACE project

---

## License

This dataset is released under:

**Creative Commons Attribution 4.0 (CC-BY-4.0)**

https://creativecommons.org/licenses/by/4.0/

---

## Documentation

Full documentation and project details:

https://fish-pace.github.io/chla-z/

---

## Contact

Eli Holmes  
NOAA Fisheries  
eli.holmes@noaa.gov

---

## Notes

This dataset is a research product intended for evaluation and exploration.  
Users should consult the documentation for known limitations and validation status.
