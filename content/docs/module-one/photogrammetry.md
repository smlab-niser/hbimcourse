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

# Photogrammetry

Photogrammetry is the process of obtaining *reliable information about physical
objects and the environment through processes of recording, measuring and interpreting
photographic images and patterns of recorded radiant electromagnetic energy and
other phenomena.*

Though photogrammetry has been as old as photographs itself, the techniques have
gone from mostly analog and optical techniques to computer-aided simulations. For
heritage sites, the photogrammetry is a very helpful technique to estimate the geometry.
In general, the photogrammetry can be divided into two types, (a) aerial and (b)
terrestrial based on the position of the camera and also based on the position of
the target, it can be divided into long and short range photogrammetry.

For applications that require high image/geometry details in conjunction with occluded
regions like the rooftops, terrestrial photogrammetry is not enough and hence the
close range aerial photogrammetry is preferred. For such applications, we need to
operate a unmanned aerial vehicle (UAV) such as a drone. In the course further, UAV
and photogrammetry will be used interchangeably.

The basic principle behind photogrammetry is the geometrical reconstruction of the
path of rays from the target to the camera sensor at the moment of exposure.

## Photogrammetry pipeline
In this section, we will describe how a set of images are converted to a 3D model
and go through the various steps involved, such that we can have a clear idea on
how we can tweak the parameters and other factors so that the process of data collection
and processing can be optimized for better final model. The goal is not to go into
the detail mathematics behind the process, nor the details of the algorithm or
it's implementation.


![pipline image](./fc1.png)
### Natural feature extraction
The natural feature extraction is to find a group of pixels that are not changing
too much for different viewpoints. One of the well known method for doing so is called,
**Scale-invariant feature transform** or the SIFT algorithm.

For a given image, a set of progressively down-scaled images are first created
and then points with locally maximum Laplacian are identified. These maxima are
the points of interest or features. The Laplacian is a measure of how the color
value of the current position is different than the values at its neighboring
points. The square patch of pixels with the center at the maxima, called
key-points.

The number of
patches are sometimes reduced to a reasonable number if they are too high. 
Each extracted discriminative patch is then stored along with it's descriptor
based on the gradients around the maxima.

SIFT extracts discriminative patches from first image and compares them to the
discriminative patches in the second image, irrespective of the rotation,
translation or scaling. These patches and their transformation gives clues for
the changing of camera viewpoints during photographing.

![pipline image](./fc2.png)
### Matching
In this part of the pipeline, the aim to find the areas in the scene that are
similar in different images. That can be done with the help of descriptors of
key-points. By converting the entire image into a compact image descriptors, we
can compare two images or parts of it by simply computing the norm between them
instead of comparing every feature individually that may take a lot of
computation power.

The features are then all matched image between candidate image pairs, based on
their image descriptors.

![pipline image](./fc3.png)
### Structure from motion and depth map
The Structure from Motion algorithm calculates the camera positions of all the
images. This is a very popular algorithm and is extensively documented and we
won't go into details of the it.
Once the camera positions are computed, the depth value of each pixel can be
calculated using many approach such as, Block Matching, Semi-Global Matching,
ADCensus, etc. 
For the depth map of independent images (which can be computed in parallel), a
filtering step is applied to ensure consistency between multiple cameras.
### Meshing
The structure from motion and depth maps computed is used to create a dense
geometrical representation from the scene. The depth map is used to create a
trochee of the depth values and then the process of tetrahedralization is
performed to get a interconnected mesh. The mesh is the separated using a
min-cut max-flow algorithm.

A Laplacian is applied to remove rogue points in the mesh and unnecessary
vertices.

![pipline image](./fc4.png)
### Texturing
The generated mesh generally doesn't have a UV associated with it. The UV are
computed automatically into regions of triangles based on the original
triangulation of the mesh.

For every triangle, many candidate images are considered that are visible from
the given camera angle such that they are looking at the surface perpendicularly,
The color is then averaged over each triangle and stored in the texture map.

We have glossed along the pipeline for the entire photogrammetry process. A
basic overview of the process can be helpful in case we want to fine tune our
photography to produce better models.
