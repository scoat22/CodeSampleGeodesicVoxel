# CodeSampleGeodesicVoxel
Geodesic voxel code example
![alt text](https://i.imgur.com/32Gq7xI.png)

For my 3D modeling project, I was faced with the task of "skinning" the mesh. This is a common problem in 3D modeling/animation software. I sought out to create a solution that was fast and accurate.

## Code overview:
This code skins a mesh by assigning bone indices and weights to each vertex.
It takes an array of triangles as input, and creates an intermediate voxel 3D grid. This is done by rasterizing each triangle in 3D, which is much faster than the conventional triangle-intersection method. Then it rasterizes each bone to the grid.
Second, it loops over each bone voxel, and assigns a distance for each bone. Effectively this constructs a "heat map", which can be referenced in the final step.
Finally, each voxel looks into each bone's heat map, and chooses the closest bone(s).

## My process:
Each step has both single and multi-thread versions. First I implemented single-thread versions of each step, just to make it easier to get things working. Then I re-wrote everything in a multi-threaded version, making sure to scale as much as possible so that someone with potentially thousands of threads on their machine could make full use of them. I think its important to not be afraid to rewrite code, because the first draft will never be perfect.

## Languages used:
The code is written in C# for Unity (game engine). It also uses the Burst extension, which optimizes code for Assembly. 
