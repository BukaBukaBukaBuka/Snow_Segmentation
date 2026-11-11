# Satellite Snow-Cover Segmentation

This notebook demonstrates unsupervised segmentation of satellite imagery to estimate snow-covered area, with a physically motivated interpretation of the resulting clusters.

**Data:** 
Three single-band raster files ("kanal_1.dat", "kanal_2.dat", "kanal_3.dat", ASCII grids, 731 × 618 pixels), one per channel, stacked into a composite multispectral image. Provided as course material; the originating platform is not documented. Parcel vector data: geoportal.gov.pl (EPSG:2180).

**What it does:**
1. Loads the three channel rasters, treats 0 as no-data (concentrated along borders), and stacks them into a composite image.
2. Determines the cluster count with the elbow method on KMeans inertia.
3. Segments the image (K = 5), clustering on per-pixel spectral values. Snow is identified via physical reasoning: snow has the highest reflectance, hence the brightest pixels; cluster compactness and RGB whiteness (balanced channel means) serve as sanity checks. Clusters are interpreted as snow regimes (fresh / settled / melt-affected).
4. Computes snow-covered area per cluster and integrates the result with cadastral parcel boundaries (raster mirrored about OX to align with EPSG:2180 vectors), yielding snow coverage inside the parcel.

**Results (this example):** 
~33.5% snow coverage over the full image (~15 km²), ~22.6% within the parcel (~2.6 km²).

**Contents:** 
"snow_segmentation.ipynb", "kanal_1..3.dat" (sample)

**Stack:**
Python (numpy, pandas, scikit-learn, matplotlib).
