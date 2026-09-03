> [!note]
> Frustum Culling occurs in the CPU to save the GPU from having to render objects outside the frustum.

Usually occurring in NDC frame and sometimes in World/View or Model Frame

[ Concept ]
Object in World Space ───────── (Transform Model) ─────────► Test inside NDC Frame?

[ Practical Implementation ] 
NDC Frame Planes ───────────── (Transform Planes) ─────────► Test against Object in World Space!

> [!info]
> A bounding-sphere or AABB box or any volume around the model is made for the CPU to check if the model is within the frustum to be consider for rendering by the GPU. 

![[Pasted image 20260729145702.png]]

# Frustum Culling in different Frames

## View Frustum Culling in Model Space
[[View Frustum Culling in Model Space]]

## View Frustum Culling in World Frame/View Frame 
[[View Frustum Culling in World or View Frame]]

## View Frustum Culling in NDC Frame 


## Ritter's Method for creating Bounding-Sphere Volumes
[[Ritter's Method]]