### Notes for South Florida HAB Observatory
#### Will be used for FDEP HAB Tech RFP

#### Two options for processing (from ESA)
1. Start with L1 and run FLH and C2RCC operators
 - Slow, large file sizes
 - FLH is negative (using TOA radiances from L1 file)
 - Cannot run Idepix; needs tensorflow, which will only run on a windows machine

2. Start with L2 and run FLH operator
 - Use L2 cloud flag
 - Need to test 
