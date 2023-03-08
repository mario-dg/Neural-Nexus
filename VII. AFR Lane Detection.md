State-of-the-Art Commercial Systems (Safety Driving Assistant):
- Lane Departure Warning System (LDWS) (SAE Level 1)
	- Warning, when leaving lane
- Lane Keeping Support (LKS) (SAE Level 2)
	- Assistance with minimal steering intervention
- Lane Keeping/Lane Departure Protection (LKDP) (SAE Level 3)
	- Autonomous lane keeping

- Navigation without a detailed global map, by analysing "drivable areas" in car's surroundings
- Multiple cues available (geometric, semantic, man-made)
- Image, LiDAR, Radar → multiple output results

#### Road Segmentation
- Pixel-wise classification of what is road (road/no-road)
- Semantic cue
- No information, if place is reachable, no geometry, and no lane information

#### Driving Corridor Prediction
- Estimation of driving corridor (i.e. lane)
- Might consider obstacles
- Multiple lanes possible, dependent on higher level plan

#### Lane Marking Detection
- Roads subdivided into lanes by lane markings
- Detect lanes/curbs, and fit parametric model
- Good working on highways, where lanes are clear

#### Lane Detection
- Grouping of 2 lane markings to one lane
- Information about lane width
- Relevant lane dependent on higher level plan

#### Free Space Estimation
- Estimate reachable space
- Geometric cue
- Lane markings independent