#### Example URLs for searching copernicus dataspace catalog API

Documentation:
https://documentation.dataspace.copernicus.eu/APIs/OData.html

#### Search for S2 MSI L1C data w/lt 30% clouds and date range which intersects a point (will generate files from just one tileID)
https://catalogue.dataspace.copernicus.eu/odata/v1/Products?$filter=Collection/Name eq 'SENTINEL-2' and OData.CSC.Intersects(area=geography'SRID=4326;POINT(-81.159 24.647)') and Attributes/OData.CSC.DoubleAttribute/any(att:att/Name eq 'cloudCover' and att/OData.CSC.DoubleAttribute/Value lt 30.00) and Attributes/OData.CSC.StringAttribute/any(att:att/Name eq 'productType' and att/OData.CSC.StringAttribute/Value eq 'S2MSI1C') and ContentDate/Start gt 2022-05-01T00:00:00.000Z and ContentDate/Start lt 2022-05-15T04:00:00.000Z&$top=10  

#### Download URL:
https://catalogue.dataspace.copernicus.eu/odata/v1/Products({"22c2637b-b2af-58db-998e-5de7e362f44b"})/$value"
Authentication is failing (need token)

Tasks:
The query above will give both S2A and S2B files for one tile during the time period.  

1. Encode URL for use on UNIX system (see below)
2. Extract Id fields from the json (example: "22c2637b-b2af-58db-998e-5de7e362f44b") and download (wget? curl?)
3. Generate access token
4. Download L1C files 
5. Process to L2 (C2RCC) and then reproject to L3 (no mosaicing)
6. Output as netcdf
7. Analyze: validate against SFER cruise data, Cheeca Rocks (and other) buoys, generate time series, etc.
8. Add to ERDDAP (optional)

#### Access token (works in terminal on imars_mbp2 - try on terminal on Jupyter Lab)
curl --location --request POST 'https://identity.dataspace.copernicus.eu/auth/realms/CDSE/protocol/openid-connect/token' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data-urlencode 'grant_type=password' \
  --data-urlencode 'username=<user>' \
  --data-urlencode 'password=<pass>' \
  --data-urlencode 'client_id=cdse-public'


Encoded URL from above:
https%3A%2F%2Fcatalogue.dataspace.copernicus.eu%2Fodata%2Fv1%2FProducts%3F%24filter%3DCollection%2FName%20eq%20%27SENTINEL-2%27%20and%20OData.CSC.Intersects%28area%3Dgeography%27SRID%3D4326%3BPOINT%28-81.159%2024.647%29%27%29%20and%20Attributes%2FOData.CSC.DoubleAttribute%2Fany%28att%3Aatt%2FName%20eq%20%27cloudCover%27%20and%20att%2FOData.CSC.DoubleAttribute%2FValue%20lt%2030.00%29%20and%20Attributes%2FOData.CSC.StringAttribute%2Fany%28att%3Aatt%2FName%20eq%20%27productType%27%20and%20att%2FOData.CSC.StringAttribute%2FValue%20eq%20%27S2MSI1C%27%29%20and%20ContentDate%2FStart%20gt%202022-05-01T00%3A00%3A00.000Z%20and%20ContentDate%2FStart%20lt%202022-05-15T04%3A00%3A00.000Z%26%24top%3D10
