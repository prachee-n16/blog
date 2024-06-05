---
title: Ray Tracer
draft: "True"
---
**Reference**: [Ray Tracing in One Weekend](https://raytracing.github.io/books/RayTracingInOneWeekend.html)
- Review vector math with [Graphics Codex](https://graphicscodex.com/projects/projects/)

The goal here is fairly simple: Understand how ray tracers work, and the above link has been recommended a lot. The implementation is done using C++ because it's fast and used in production quite a bit. For my version, I want to try this in Python by first, writing a 1:1 implementation and then, using libraries/advanced features to optimize.

There are [[Image Formats|many image formats]], multiple ways to [[Image Feature Vector|see an image]]. For an easier time, let's start with a simple [[PPM]] file.

There is a provided `vec3` class (3 dimensional as we consider RGB without alpha transparency). I've re-written this in Python, with operator overloading, alias and utility functions.
- Note, in the original impl where types exist, `double` is used rather than `float` since there is greater precision and range. `float` is used more often in ray tracers due to limited memory conditions (`double` is twice the size)
There is also a `color` class, which uses `vec3` and can be used to improve our first generated image

All ray tracers have a ray class and a method to compute what color is seen at a point in a ray. Let's say ray is a linear function `P(t) = A + tb` where P represents a point along this line in 3D, A is the ray origin, and b is the ray direction. As we change t, we begin to move along the ray. 

>[!todo]
> - [ ]  [[VirtualEnv|Set up a virtual environment]]


