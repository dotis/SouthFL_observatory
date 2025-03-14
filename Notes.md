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
2. PACE or other OC (S3?) anomalies to look at high Chla, turb, blooms (can we use MODA climatology?)
3. USGS and USACE gauge data (on Quarto dash)
4. Physical model for flow? (FVCOM?)
5. IMERG daily precip
6. 


#### Dashboard (simple - Quarto/Shiny/FlexDB/grafana):
1. Flow from Everglades (current and recent conditions - short time series w/Clim and red/green status guage)
2. Sentinel-2 images (most recent ~two weeks)
3. Sentinel-3 FLH (recent) - Calculate area exceeding a threshold in recent weeks)
4. Flow conditions - Need to use a model
5. Could use a simple version of the FKNMS grafana dash:
 - Show daily images (recent only)
 - Show time series (recent only w/climatology for reference)
   - Discharge, temp, salinity, rainfall (which areas to extract for sat or other gridded data?)
 - Show guages to indicate current conditions: presence of blooms, high temps, low salinity
 - 24N to 26N (or 26.5N) only (restrict to near the FKNMS)
 - Other?


#### FLH satellite products:
1. Can use MODIS for now, but will go away soon
2. Can use PACE (very little history) - This may be the best option (easiest)
3. Could serve S3 OLCI on ERDDAP (w/o FLH); get L2 from OBPG - Do we really need this?
4. Can use S3 OLCI (L2_OC from OBPG ingest through CMR)
 - Run FlhMci (SNAP) operator to derive FLH (from Rrs) - HASSLE!!
 - Use one filestream (complicated)
 - Graph:
    1. Mosaic op. to ingest bands and merge/grid
    2. Bandmaths op.(1) to create nLw (spectral) bands
    3. FLH op. to calculcate FLH
    4. Bandmaths op.(2) to create output bands
 - We could try to calculate FLH using bandmaths as part of the mosaic operator - easiest (needs work)
 - From ESA Forum, could use with nLw
 - ![image](https://github.com/user-attachments/assets/aa6ca9e5-eafa-4e7c-a53e-a2f1c892db7d)
 - Easiest way(?!?):
    - Mosaic and bandmaths graph on OBPG OLCI L2 data
    - Code in FLH manually in band maths node
    - Do we even need this? Advantages? (300m resolution); Disadvantages? (hassle)
 


### Tasks/Issues
 - Sample S2 WQ images to use for FDEP proposal for Y6
 - Validate S2 WQ
 - Set up ingest for IMERG (need Tylar's help)
 - Set up ingest for S3 (needed?)
 - Refine Quarto dash
 - Extract IMERG precip in ROI polygons (SWFL, SEFL, others?)
 - How to quantify bloom and other current conditions? Count pixels and calculate area over a threshold?
 - Weird issue w/mosaic operator for PACE AOP (hangs on Rrs_689). Hangs on any var after Rrs_688. Issue w/length of file? Too many vars?
 - Could try to set up L3BIN/L3MAPGEN


#### S2 Test images:
1. S2_SR_HARMONIZED/20200609T160521_20200609T160518_T17RNH (Low)
2. S2_SR_HARMONIZED/20220930T160051_20220930T161339_T17RMH (High)


### S3 OLCI Details/Issues:
1. Run /srv/pgs/rois2/gom/L1_OLCI_EFR/OLCI_L1_EFR_CMR.sh - Need to set date range to today-3 for last 3 days of data
   - Specify dates by generating a date 2-3 days ago and match data since then - use ISO8601
   - Unzip issue: Can unzip single full filename, but "unzip *.zip" fails - issue w/filename
   - OR, try not unzipping - just use zipped directory as the input product to the graph
3. Then, need run graph (similar to S2-MSI graph):
 - Subset?
 - FLH
 - OC? - Could run through C2RCC or could run l2gen or could ingest S3 OLCI L2 from OBPG and grid/mosaic
 - Easiest and most consistent to ingest S3 OLCI L2 from OBPG

