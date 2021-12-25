---
title: "Rendering"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Rendering
In this section, we will talk about lighting, materials and rendering the final
output mesh. There are many tools both open source and proprietary for rendering
a mesh. There are standalone renderers like POV-Ray, Mitsuba etc, as well as
fully integrated 3D software that everything from modeling, rigging, shading to
rendering, like Blender and Autodesk Maya. In this chapter, we will use Blender
since it is free and open source and available for almost all relevant operating
systems including BSD and Haiku.

## Materials
Blender has an extensive nodes system that helps to shade a 3D object with
materials, textures and various manipulations on them. However, in this section
we will only talk about how we can manipulate so that we can get the results we
like.

The texture map reconstructed from the photograph give information on how to
color a given polygonal face in the mesh based on the UV co-ordinates. This is
correct in most cases and if they are not correct, then the reconstruction
parameters maybe tweaked to make get a better texture map. Unfortunately, when
it is not accurate, for example, with a shiny surface, the material may have to
be added in manually.

For example, if a surface along with it's texture is shiny, then that has to
be tweaked so that light can reflect off of the object while path tracing
step in rendering.  Blender, like many other 3D software, used the PBR node
which looks like below.

![pbr](pbr.png)

There are a lot of parameters here, but the most important ones are explained
below,
- **Base color** controls the color of the 3D object. This paints an uniform
coat of the selected color over the mesh. The base color input can come from a
texture node with UV data.

- **Subsurface color** controls the color of the scattered light under the
surface. For example, the human skin scatters a reddish color because of the
flesh. In cultural heritage site, they may not have any use since sub surface
scattering generally do not happen in rocks and building materials. But,
sometimes thin amethyst like stones may scatter some light.

- **Metallic** controls the reflectivity of the surface.
- **Specular** controls how the reflectivity falls off from direct reflection.
- **Roughness** value controls the diffusion of light reflected off.
- **IOR** is the index of refraction of a transparent object.
- **Transmission** controls the transparency of the object.
- **Normal** like the _base color_ is a input normal map whose RGB component
corresponds to the three component of the area vector for the given polygon
face.

The image below demonstrates the material type for various values of the above
parameters.
![pbr parameters](pbrparam.png)
From left to right: (a) Transmission is 1.0 (b) Roughness is 1.0 (c) Metallic is
1.0 and (d) Roughness is 0.0 and Metallic is 0.0

## Lighting
In real world, there is always a diffused light in everywhere we look, both from
natural light sources like the sun or artificial lights like lamps. However,
in a atrificial setup like ours, there is no inherent lights and hence, the
render may also look very dark with one lamp in the scene. Too many lamps can
make the render washed out. Below is an example of both washed out and too dark
scenes rendered.

![dark and washed out renders](darkwashed.png)

The right side is too dark while the left is washed out.

One solution is use a  HDRI map, also known as environment map. The environment
is an image that is wrapped around the scene. In path tracing, when a light ray
reaches the far bound without hitting any object, the ray takes the color of the
environment map. There are many environment maps that are freely available
online. A 360 degree image can also act as environment map and Blender supports
that too.

Here is an example of the same scene with a environment map and no artificial
lamp.
![environment texture](env.png)

The darker areas areas even get light from the environment map like in real
life, where as in a setup with the environment map there is not a light source
at dark areas as there is nothing to reflect off of.

In case the environment light setup is not desired, a 3-point light setup can
be used. A 3-point light setup contains three lights, key, fill and rear lights.
Blender has a plugin that helps in getting a correct 3-point light setup. To
activate it, go to `Blender > Edit > Preferences > Addons > Lighting:
Tri-lighting`. Once the addon is activated, it can be added in the scene using
the `Add` menu.

In this system, there is
- The **key light** that is the strongest light and is the main light that
lights the scene.
- The **fill light** that not bright and it serves the purpose of filling the
dark areas or shadow areas of the **key light** with a subtle light to that
there is not a lot of contrasts.
- The **rear light** is a stronger light with that serves to light the back of
subject and sometimes put to bring a clearer silhoutte of the subject such that
it separates the subject from the background.

The three lights are generally put around the subject with the camera in the
vicinity of the subject. Not only the lights and material affect the quality of
the render, but also the camera. The camera setup is detailed in the section
on photographing techniques. The same principles applies here in rendering too.
Blender supports all the camera parameters discussed there.

