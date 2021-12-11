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
### History and archaeology
- When the temple was discovered from foilage around, there was no deity found in the temple.
- The name was _Indreswara_, _swara_ is generally used as a name of Shiva, which makes it a Saiva temple.
- There is not a lot of literature and histry found about the temple.
- The temple was covered in foilage when it was discovered.
- It deity may not be missing, it may not have been installed.
- There was no background discoloration at the location of deity in the _garva gruha_.
- Brahmeswar temple nearby has a deity. It is a Saivite temple.
- Magheswar has a Ashokan pillar. It has a two storey Linga. It's architecture doesn't match other Orissan temple.
- It is just one pidha temple. It has stone railing similar to buddha temples. Maybe it was a Buddhist temple that had the Ashokan pillar and the temple was created around it. Buddhism is from around 6th century BC.
- Orissa has a lot of Buddhist activities from 2nd century BC.
- The diamond triangle: Udaygiri, Lalitagiri and Ratnagiri are some very rich buddhist sites. Other sites Langudi, for instance. Lot sites in Cuttack and Jajpur district. Many excavation.
- Buddhism started as a rebellion against a caste system of Brahminism (which is not called Hinduism). And there was revival of Hinduism, from Brahminism.
- It was called Brahminism before Buddhism came to the picture. Before that it was called Sanatanism. It was not a religion. It was just a set of guidelines for life style.
- There is not a lot of Sanatanism evidence in Orissa.
- Historians know about Orissa from 6th century AD, but before that it was a dark period.
- There is not a lot of information about Orissan history before it. Some information is present during Ashoka. But nothing before and after him. The Kalinga war happened during 3rd century BC when Ashoka attacked.
- People say Orissa was a very closed state. It had no interaction around the neighboring kingdoms. The people had trade through sea. Orissa people were extremely skilled navigators for their time. They made a lot of overseas business.
- Orissa was a federation republic. It was not unified under a single king. Orissa was a self-sufficient.
- Orissan people don't keep records and were very bad record keeping. The history only passed as a word of mouth.

### Photogrammetry
- Rough photogrammetry drone trajectory I have drawn from memory.
- The drone was flying at about 80 m above the ground.
![drone trajectory](/img/week32/drone-trajectory.png)
- Photogrammetry is based on the overlap of the images. The same features atleast has to be detected on 3 images. That is how you decide which images to take.
- The images are then stitched. First step is **densification** and **key-point detection**.
- Once we have enough images of the overlapping images, the images are then calibrated and the camera position is estimated. (This is very similar to what I did in LLFF.)
- The next step is to manually provide control points.
- The base-station is a RTK-based GNSS system (realtime kinematic correction, if I remember is correctly).
![drone base station](/img/week32/base-station.jpg)
- The drone is the rover and the station is the base. The remote, the rover and the base are in communication all the time.
- This helps in the realtime calculation of the geolocation and correction of the co-ordinates.
- The geolocation device is on the craft/rover as well as on the base station.
- For civilian usage, there is an error of 5 to 8 meters in the geo co-ordinates.
- It should connected to a CORS network (coninuously operating reference station). But here in India we do not have CORS, so we do it on VRS (virtual reference station), based on the region. Government restrictions.
- The shooting was done in raw with a 20 megapixel sensor.
- It was shot in raw to remove all the shadows. But it will be bigger file size. Every image will be around 60 MiBs. And after the post processing it becomes about 8 MiB.
- The control points are added to the images manually and better control points give better measurements.
- There will be occuluded region when there was a overall coarse scan. But then a flat vertical scan profile photograph was taken with close by camera.
- The drone makes sure that is no motion blur while taking the photograph, by making sure the shutter speed, drone movement is condemn with each other.
- Since the photographs are taken in raw image format, all the parameters like gamma, ISO, color can all be corrected except the shutter speed.
- All this correction is all manual. There are some batch process, though, like tone, temperature and color balance so that there is no artefacts.
- Most of the batch processing is for tonal balancing. Tone balance can be done in batch process. But not gamma.
- The metadata also contains a camera position and orientation. The craft has a very high precision IMU (wut?) unit with a tolerance of .25 arcsec.

### Laser Scan

- The scanner was a FARO Focus.
![scanner](/img/week32/scanner.png)
- (I don't understand what the guy meant.) The resolution of the scanner was 1/4x. The color resolution was 3x. It takes HD photos. 4x is a point cloud resolution and 3x is the color resolution.
- The total time is 13 minutes for a given vantage point.
- Scanner was placed to minimize the coverage error.
- The scanner doesn't have geo co-ordinates. The base station is required to tag geo co-ordinates.
- The of the geo co-ordinates in the point cloud merging happens in software.
- Some points that the scanner cannot reach will have to filled in manually from the photogrammetry data.
- The blind spots are hard to reach corners and top of the temple.
- When the data as been collected, the overlapping points are calibrated together in a process called **registering**.
- For point cloud registration is done manually by looking at the common overlapping points and triangulation of the points to get the absolute co-ordinates.
- The interior of the temple has no lights so therefore a torch was used at the _garva gruha_ and the corridor connecting the _garva gruha_ and the _jagamohana_.
![torch](/img/week32/torch.png)
- There was a metallic grill that was installed by ASI at the ceiling of the _jagamohana_ and _garva gruha_.
- The grill was causing errors in registering the points. The laser scanner was placed at the top of the grill to take the scan of the ceiling of the _jagamohana_.
- There was a lot of bats between the grill and the ceiling of the _garva gruha_. The technician was scared to go in there. Some workers (gardeners I guess) had to shoo away the bats to let the technician to be able to put the scanner on the grill.
![scanning over the grill](/img/week32/grill.png)
- Above the ceiling of the _garva gruha_ there is an entrance to the hollow interior of the _deula._
- The hollow interior of the temple was now nested by bats. A worker in the temple tried to take some photos of the interior. These are the photos he managed to take.
![hollow interior of the deula](/img/week32/hollow.png)
