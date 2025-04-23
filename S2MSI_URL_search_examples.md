#### Example URLs for searching copernicus dataspace catalog API

Documentation:
https://documentation.dataspace.copernicus.eu/APIs/OData.html

#### Search for S2 MSI L1C data w/lt 30% clouds and date range which intersects a point (will generate files from just one tileID)
https://catalogue.dataspace.copernicus.eu/odata/v1/Products?$filter=Collection/Name eq 'SENTINEL-2' and OData.CSC.Intersects(area=geography'SRID=4326;POINT(-81.159 24.647)') and Attributes/OData.CSC.DoubleAttribute/any(att:att/Name eq 'cloudCover' and att/OData.CSC.DoubleAttribute/Value lt 30.00) and Attributes/OData.CSC.StringAttribute/any(att:att/Name eq 'productType' and att/OData.CSC.StringAttribute/Value eq 'S2MSI1C') and ContentDate/Start gt 2022-05-01T00:00:00.000Z and ContentDate/Start lt 2022-05-15T04:00:00.000Z&$top=10  

Tasks:
The query above will give both S2A and S2B files for one tile during the time period.  

1. Need to convert URL for use on UNIX system
2. Need to extract Id fields from the json (example: "22c2637b-b2af-58db-998e-5de7e362f44b") and download (wget? curl?)
3. Process to L2 (C2RCC) and then reproject to L3 (no mosaicing)
4. Output as netcdf
5. Analyze: validate against SFER cruise data, Cheeca Rocks (and other) buoys, generate time series, etc.
6. Add to ERDDAP (optional)
