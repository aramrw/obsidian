#shaders #math
# Domain Warping

Domain Warping (or space distortion) is a technique where, rather than drawing a complex shape, the coordinate space itself is distorted before a simple shape is drawn. 

For instance, applying a formula that tears the grid outward from the center can create complex shapes from simple circles or lines.

**Note:** 
> Relying on a tangent curve for warping introduces [[Asymptotes]]. This causes infinite stretching at regular intervals. While stylistically distinct, using a continuous function like sine waves or [[Simplex Noise]] provides a more stable, artifact-free distortion.

--- 