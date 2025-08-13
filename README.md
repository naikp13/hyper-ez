### Hyper-EZ: Hyperspectral Easy Enhancement Package
Hyper-EZ is a python based package for enhancing hyperspectral imagery using an Imporoved Parallel Patch-wise Sparse Residual learning algorithm (ip2sr), an upgraded version of the p2sr algorithm published in https://www.mdpi.com/2072-4292/17/11/1878). It combines Sentinel-2 multispectral data and high-resolution imagery (ESRI World Imagery) through a fully automated architecture using a sophisticated reconstruction and enhancement process to increase the spatial resolution of hyperspectral imaging data while preserving spectral information.

### Key Components

#### 1. Data Acquisition (`data_acquisition.py`)
- **SatelliteDataAcquisition**: STAC API client for Sentinel-2 data search
- **DataDownloader**: Robust file downloading with retry logic

#### 2. Geospatial Processing (`geospatial_utils.py`)
- **GeospatialProcessor**: Handles reprojection, clipping, and resampling
- Automatic coordinate system transformations
- Multi-band GeoTIFF creation

#### 3. Image Processing (`image_processing.py`)
- **HyperspectralProcessor**: Core enhancement algorithms
- High-resolution imagery acquisition (ESRI World Imagery)
- HSI enhancement using guided filtering

#### 4. Visualization (`visualization.py`)
- **HyperspectralVisualizer**: False color composite generation
- Comparison tools for original vs enhanced imagery

## Configuration

Key parameters can be modified in `config.py`:

```python
# Processing Parameters
DEFAULT_CLOUD_COVER_THRESHOLD = 5  # Maximum cloud cover percentage
TARGET_RESOLUTION_METERS = 10.0     # Sentinel-2 target resolution
HIGH_RESOLUTION_METERS = 2.0        # ESRI imagery resolution

# Enhancement Parameters
DEFAULT_PATCH_SIZE = 12
DEFAULT_STRIDE = 1
DEFAULT_GUIDE_RADIUS = 10
DEFAULT_DETAIL_WEIGHT = 1
```

## Workflow

The enhancement process follows these steps:

1. **Download Benchmark Data**: Acquire reference hyperspectral imagery
2. **Extract Spatial Metadata**: Get bounds, CRS, and resolution information
3. **Search Sentinel-2 Data**: Find suitable multispectral imagery via STAC API
4. **Process Sentinel-2 Bands**: Download, clip, and resample all 12 bands
5. **Acquire High-Resolution Imagery**: Download ESRI World Imagery
6. **Initial Enhancement**: Fuse Sentinel-2 with hyperspectral data
7. **Super-Enhancement**: Further enhance using high-resolution imagery
8. **Visualization**: Generate false color composites

## Data Sources

- **Hyperspectral Data**: EnMAP validation clips
- **Multispectral Data**: Sentinel-2 Level-2A (via AWS Earth Search STAC API)
- **High-Resolution Imagery**: ESRI World Imagery Service


## Output Files

- `hyperspectral.tif`: Original hyperspectral reference data
- `processed_sentinel2.tif`: Processed 12-band Sentinel-2 imagery
- `high_resolution_imagery.tif`: Reprojected ESRI World Imagery
- Enhanced hyperspectral arrays (in-memory)

## Error Handling

The package includes comprehensive error handling for:
- Network timeouts and HTTP errors
- Invalid geospatial data
- Missing satellite imagery
- Coordinate system transformation issues
- File I/O operations

## Performance Considerations

- **Memory Management**: Automatic garbage collection and temporary file cleanup
- **Parallel Processing**: Band processing can be parallelized (future enhancement)
- **Caching**: Downloaded data is temporarily cached during processing

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Dependencies

- `matplotlib>=3.5.0`: Plotting and visualization
- `rasterio>=1.3.0`: Geospatial raster I/O
- `shapely>=1.8.0`: Geometric operations
- `requests>=2.28.0`: HTTP requests
- `numpy>=1.21.0`: Numerical computing
- `pytz>=2022.1`: Timezone handling
- `pystac-client>=0.5.0`: STAC API client
- `opencv-contrib-python==4.11.0.86`: Computer vision algorithms

## License

This project is licensed under the MIT License.

## Citation

This is a pre-release version. The hyper-ez github package is under-development and will be published soon. Please cite the following paper if this version of package was used, 
```bibtex
@article{naik2025scalable,
  author = {Parth Naik and Rupsa Chakraborty and Sam Thiele and Richard Gloaguen},
  title = {Scalable Hyperspectral Enhancement via Patch-Wise Sparse Residual Learning: Insights from Super-Resolved EnMAP Data},
  journal = {Remote Sensing},
  volume = {17},
  number = {11},
  article = {1878},
  year = {2025},
  doi = {10.3390/rs17111878},
  url = {https://doi.org/10.3390/rs17111878}
}
```

## Acknowledgments

- [HSI Enhancement Library](https://github.com/naikp13/hsi_enhancement) for core enhancement algorithms
- [AWS Earth Search](https://earth-search.aws.element84.com/v1) for Sentinel-2 data access
- [ESRI](https://services.arcgisonline.com/) for high-resolution imagery

## Support

For questions, issues, or contributions, please:
- Open an issue on GitHub
- Contact: parthnaik1993@gmail.com

---

**Note**: This package requires internet connectivity for downloading satellite imagery and may have usage limits based on data provider terms of service.
