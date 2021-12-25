---
title: "Photographing techniques"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---
# Photographing techniques
In this chapter, we will take a look at how we can produce 3d polygon meshes from
photographs. The quality of the model is dependent on many factors and understanding
how each of the factors affect the the final model can help in producing
better quality models.

The very first step in the photogrammetric pipeline is to detect the features and
build a point cloud of the model. So, the detection of features in the model should
be the first rule of thumb to distinguish between a bad and good input photograph.
And hence all the tweaking of the factors listed below is to optimize in gathering
many detectable feature on the subject while not detecting the features in the background.

Although the _automatic_ settings on the digital cameras is good enough for taking
photographs for everyday situations, they are not good enough for photogrammetric
reconstructions. This section describes what settings to keep in mind while photographing
the target. The three most important camera settings shutter speed, aperture and
the ISO. In photography, this is known as the **exposure triangle**.

## Camera shutter speed 
The **shutter speed** is the time the camera lens is exposed to the scene. The lower
the shutter speed, the longer the lens is exposed to the scene and vice-versa. Allowing
the lens to get exposed for a longer time, produces brighter images since more light
can enter the sensor. However, if the target or the camera is moving and the shutter
speed is low, then target or any other object in the field of view can expose more
than one part in the sensor and hence the images may come out blurry.

It is hard to detected features in a blurry images, and since the quality of the
model is dependent on the number of detected features, the final output may suffer.
Therefore, **avoid taking blurry images** and try to keep the images as sharp as
possible. Increasing the shutter speed can help.

With a higher shutter speed, the exposure time is less and the object in the field
of view get less time to expose more area in the sensor and hence, the images are
less blurry. However, the images are darker as a result. If **the subject is in bright
light, then higher shutter speed is recommended.** However, it is not always possible
to have bright lights everywhere.

Sometimes it is not easy to keep a steady
hand while taking photographs, especially when the shutter speed is too low to compensate
for ill lit scenes. Since we are taking photographs of temples and heritage sites,
the photographer has no control over the position of the sun and area that is not
directly lit like interiors and shadows. In such cases, a tripod may be used and
the control the camera using a remote than physically pressing the shutter release
button that may disturb the camera. In case of drone photography, it is advisable
to make sure that the drone's motion is stabilized and completely still when the
photograph was taken.

## Camera aperture
The aperture is the size of the _hole_ that exposes the sensor. It is donut-shaped
ring that can expand and contract. The **f-number** or **f-stop** controls how big
of a _hole_ you want on your aperture. The f-number is generally represented as
F/#. A higher aperture like F/4 or F/2 open the aperture more widely and hence more
light can enter the sensor, while a lower aperture like F/32 or F/64 allows less
light. However, the most important property that the f-number changes is the **depth
of field**.

The depth of field, controls the focus and blurriness of the background. A higher
depth of field brings out more details in the background and a lower depth of field
blurriest the background and makes the subject of the photographs to stand out more.
For our case of  photographing cultural heritage sites, we are more interested in
the subject rather than the objects in the background. And the photogrammetric
techniques that we employ uses feature detection to track the various parts of the
model.

A photograph with details in the background can be picked up as a feature and tracked.
While they do not provide any useful information to the algorithm, they take up
space and computing resources. So, **use a low depth of field** or higher f-number
for taking the photographs.

## Camera ISO
The ISO controls the sensitivity of the sensor. It is always recommended **to keep
the ISO as low as possible**. A lower ISO is always better for increasing the dynamic
range, and color accuracy while decreasing the chromatic aberrations. A lower ISO
also makes sensor less sensitive and hence reduces
the noise and graininess. This is important since a less grainy image makes it less
likely for the feature detection algorithm to pick up noise. However, a less sensitive
sensor needs more exposure to detect less bright areas. So, it all comes down to
the balance between the ISO, shutter speed and the aperture.

## Subject zoom and overlap
The photogrammetric algorithm does not care if the entire subject is not visible
in every single shot. Therefore, **close up pictures that can cover many detectable
features** are desirable. However, for the algorithm to know the entire model, it
is also advisable to take some pictures with the entire subject in frame as well
as making sure that for two images, there is at least a 70% overlap of the detectable
features.

## Subject material
A shiny, specular surface that reflects the surrounding is difficult for the algorithm
to work with since the reflections of the surrounding objects may be detected as
a feature of the subject. Many lose parts like hairs and grids are difficult to
capture and vary wildly from scene to scene. Even with high overlaps, the features
are not easy to detect and only confuse the algorithm to try select and track non-existent
features. For cultural heritage sites, it is much more practical to hand model such
parts.

## Subject masking
Isolating a cultural heritage site from it's background is not possible and if the
subject is big enough, then the depth of field may not help in isolation and blurring
the background. So, the image has to be masked to only keep the subject and remove
any background. While the background many not be very useful, features detected in
the background will only consume computing power and space.

## Number of views
For a cultural heritage model, it is important to take pictures of all possible
angles and elevations as well as occluded regions so that they can be modeled. If
a part of the structure is not present in at least 3 images and then the triangulation
fails and the final output model may not contain the part. While this can be filled
automatically in post-processing, the result may not be accurate.

## Summary
In summary, the following things needs to be considered. 
- Set the camera to use higher shutter speed, lower depth of field and lower ISO.
- Close up pictures with more detectable features.
- A 60-70% overlap of the detectable feature in at least two images.
- Avoid shiny, specular and transparent subjects.
- Avoid blurry images.
- Avoid subjects with fine and many lose parts like hair, grids and nets.
- Mask the subject from the background
- Rotate and zoom the camera such that the subject covers at least 70% of the image.
- Use different elevations for covering occluded and shadow areas like rooftops.
- A larger number of photographs never hurts, except for the requirement of computing
power.

With that in mind, the data collection part of the project may be carried out
and the with enough data in the hands, we can move the next section of actual
photogrammetric reconstructions.
