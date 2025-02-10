### South Florida Connectivity Dash

#### What is it? Why do we need it?

Science Questions:
1. How does water from the Everglades connect to Florida's Coral Reef?
2. What are the time scales (5-days from Heidi H.?)?
3. Can we trace the path of water reaching the FCR?
4. Can we assess WQ in the channels between FL Bay/backcountry and the reefs?
5. How are HABs affecting FCR/FKNMS? - Can we track/monitor HAB conditions and show status?


#### Tools:
1. Sentinel-2 WQ (test C2RCC w/SFER cruise data and IRL sensor data)
2. Sentinel-3 WQ (FLH mainly to look at blooms)
3. USGS and USACE gauge data (on Quarto dash)
4. Physical model for flow? (FVCOM?)


#### Dashboard (simple - Quarto/Shiny/FlexDB):
1. Flow from Everglades (current and recent conditions - short time series w/Clim and red/green status guage)
2. Sentinel-2 images (most recent ~two weeks)
3. Sentinel-3 FLH (recent) - Calculate area exceeding a threshold in recent weeks)
4. Flow conditions - Need to use a model


#### FLH satellite products:
1. Can use MODIS for now, but will go away soon
2. Can use PACE (very little history)
3. Can use S3 OLCI (need to set up ingest - can we get through CMR?)
