#### Example URLs for searching copernicus dataspace catalog API

Documentation:
https://documentation.dataspace.copernicus.eu/APIs/OData.html

#### Search for S2 MSI L1C data w/lt 30% clouds and date range which intersects a point (will generate files from just one tileID)
https://catalogue.dataspace.copernicus.eu/odata/v1/Products?$filter=Collection/Name eq 'SENTINEL-2' and OData.CSC.Intersects(area=geography'SRID=4326;POINT(-81.159 24.647)') and Attributes/OData.CSC.DoubleAttribute/any(att:att/Name eq 'cloudCover' and att/OData.CSC.DoubleAttribute/Value lt 30.00) and Attributes/OData.CSC.StringAttribute/any(att:att/Name eq 'productType' and att/OData.CSC.StringAttribute/Value eq 'S2MSI1C') and ContentDate/Start gt 2022-05-01T00:00:00.000Z and ContentDate/Start lt 2022-05-15T04:00:00.000Z&$top=10  

