---
title: "Rajarani: Data collection"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
## Photogrammetry
- The flight plan for unmanned aerial vehicle is given below.
- The drone was flying at about 80 m above the ground.
![drone trajectory](drone-trajectory.png)
- Photogrammetry is based on the overlap of the images. The same features at least has to be detected on 3 images.
- The images are then stitched. First step is **densification** and **key-point detection**.
- Once we have enough images of the overlapping images, the images are then calibrated and the camera position is estimated.
- The next step is to manually provide control points.
- The base-station was a RTK-based GNSS system (real time kinematic correction).
![drone base station](base-station.jpg)
- The drone is the rover and the station is the base. The remote, the rover and the base are in communication all the time.
- This helps in the real time calculation of the geolocation and correction of the co-ordinates.
- The geolocation device is on the craft/rover as well as on the base station.
- For civilian usage, there is an error of 5 to 8 meters in the geo co-ordinates.
- It was connected to a CORS network (continuously operating reference station) and
to a VRS (virtual reference station).
- The sensor was 1” CMOS 20 mega-pixel camera with 24mm lens and 84 deg field of view.
- The unmanned aerial vehicle had a automatic pitch-roll-yaw stabilization.
- The UAV flight had a flight altitude of 80m, flying at 7 m/hr, with 75% overlap
and 80% side-lap.
- A total of 2,334 photographs were taken.
- The control points are added to the images manually and better control points
give better measurements.
- The were occluded region during overall coarse scan. To fix that flat vertical
scan profile photograph was taken with close by camera.
- The drone makes sure that is no motion blur while taking the photograph, by making sure the shutter speed, drone movement is condemn with each other.
- Since the photographs are taken in raw image format, all the parameters like gamma, color can all be corrected except the shutter speed.
- All this correction is all manual. There are some batch process, though, like tone, temperature and color balance so that there is no artifacts.
- Most of the batch processing is for tonal balancing. Tone balance can be done in batch process, but not gamma.

### Rajarani camera details

| Camera parameters     | Value                       |
| --------------------- | --------------------------- |
| Number of photographs | 2334                        |
| Shutter speed         | 120                         |
| ISO                   | 100                         |
| Aperture              | f/5.0                       |
| Focal length          | 24.0 (35mm film) 8.8 (lens) |
| Metering method       | Average                     |



## Terrestrial Laser Scan

- The scanner was a FARO Focus M70 scanner.
![scanner](scanner.png)
- The scanner was operating based on time of flight laser pulse operating at 97 Hz
scan speed at at about half a million points per second at a range of 1m to 30m
with an accuracy of 3mm.
- A total of 62 scan position was fixed based on intricacy of the carvings on
the temple and also to minimize the scan error.
- A built-in 360 deg 165 mega-pixel HDR camera with 2x exposure bracketing was used
to capture color/texture information of the point cloud.
- The total time is 13 minutes for a given vantage point.
- Scanner was placed to minimize the coverage error.
- The scanner doesn't have geo co-ordinates. The base station is required to tag geo co-ordinates.
- The of the geo co-ordinates in the point cloud merging happens in software.
- Some points that the scanner cannot reach will have to filled in manually from the photogrammetry data.
- The blind spots are hard to reach corners and top of the temple.
- When the data as been collected, the overlapping points are calibrated together in a process called **registering**.
- For point cloud registration is done manually by looking at the common overlapping points and triangulation of the points to get the absolute co-ordinates.
- The interior of the temple has no lights so therefore a torch was used at the _garva gruha_ and the corridor connecting the _garva gruha_ and the _jagamohana_.
![torch](torch.png)
- There was a metallic grill that was installed by ASI at the ceiling of the _jagamohana_ and _garva gruha_.
- The grill was causing errors in registering the points. The laser scanner was placed at the top of the grill to take the scan of the ceiling of the _jagamohana_.
- There was a lot of bats between the grill and the ceiling of the _garva gruha_. The technician was scared to go in there. Some workers (gardeners I guess) had to shoo away the bats to let the technician to be able to put the scanner on the grill.
![scanning over the grill](grill.png)
- Above the ceiling of the _garva gruha_ there is an entrance to the hollow interior of the _deula._
- The hollow interior of the temple was now nested by bats. A worker in the temple tried to take some photos of the interior. These are the photos he managed to take.
![hollow interior of the deula](hollow.png)
