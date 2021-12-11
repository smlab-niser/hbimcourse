---
title: "Photogrammetry"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

Photogrammetry is the process of obtaining *reliable information about physical
objects and the environment through processes of recording, measuring and interpreting
photographic images and patterns of recorded radiant electromagnetic energy and
other phenomena.*

Though photogrammetry has been as old as photographs itself, the techniques have
gone from mostly analog and optical techniques to computer-aided simulations. For
heritage sites, the photogrammetry is a very helpful technique to estimate the geometry.
In general, the photogrammetry can be divided into two types, (a) aerial and (b)
terrestarial based on the position of the camera and also based on the position of
the target, it can be divided into long and short range photogrammetry.

For applications that require high image/geometry details in conjunction with occuluded
regions like the rooftops, terrestarial photogrammetry is not enough and hence the
close range aerial photogrammetry is preferred. For such applications, we need to
operate a unmanned aerial vehicle (UAV) such as a drone. In the course further, UAV
and photogrammetry will be used interchangeably.

The basic principle behind photogrammetry is the geomtrical reconstruction of the
path of rays from the target to the camera sensor at the moment of exposure. The
reconstruction is based on the 

## Types of photogrammetric photographs
In this section, we will discuss the types of images captured, the challenges facing
the capturing and how it can affect the reconstructed models. 
### Vertical photographs
The images that are taken are categorized as vertical photography if the rays hitting
the sensor is perpendicular to the optical plane of the image, i.e, perpendicular
to the ground. For digital images, the ground
sample distance (GSD) determines the spatial resolution, i.e, the smallest visible
detail in the photograph. As the height of the UAV increases, the scale of the image
is halved and for digital images, the GSD also decreases.

The vertical photographs capture the parallel geometry of the target. In practice,
most aerial photograph deviate from verical photographs because of the following
reasons. (a) the ground may not be flat i.e, the elevation of the ground changes,
(b) the photograph may not be completely vertical and (c) the projection is imperfect.

For higher elevations, the target becomes nearer to the sensor and hence the scale
of the image changes and the relif displacement increases with distance to the center 
of the image. It is also inversely proportional to the height, focal length and
the aperature of the sensor. The reason being that the rays are comparatively less
inclined.

Therefore, images for monoscoping mapping should be taken such that it reduces the
distortion due to relif displacement, i.e, the images is best taken using a telephoto
lens from a greater height. However, for reconstruction purposes and stereoscopic
viewing, and most BIM applications, the image should have higher focal length, wider
aperature, taken from a lower height.
### Tilted photographs


### Interior photographs
### Exterior photographs

## Stereomodels

## Libraries

#### Citation
[1] *James S. Aber, Irene Marzolff, Johannes B. Ries,* __Chapter 3 - Photogrammetry, Small-Format Aerial Photography__ Elsevier, 2010, Pages 23-39, ISBN 9780444532602.
