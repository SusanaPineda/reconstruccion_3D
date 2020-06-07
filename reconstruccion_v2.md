# 3D Reconstruction - Own TriangulatePoints
In the following approach, we will try to implement a triangulation algorithm using epipolar geometry.

To get the point in the 3D world from two images we are going to need the projection matrices of the two cameras used and the homogeneous coordinates in which the 3D point projects in the obtained images.

From this information, the following system of equations can be created.

![](/data/sistema_ecuaciones.png)

from the system of equations we can calculate the 3D point using the inverse of the svd of the matrix.

Before we can paint the calculated point, we must normalize it and eliminate the fourth component of the coordinates. It is also important to apply a scale in order to easily appreciate the reconstruction.

In this case, the reconstruction appeared rotated, making the objects stand upside down, so the value of Z was inverted at all points and a small displacement was applied so that they were placed on the ground plane.

If the same algorithm is maintained as in the previous version, modifying certain representations of the points (homogeneous coordinates) and changing the triangulation method to the new method, the following results are obtained:

[![](https://img.youtube.com/vi/kHl5mi_ep0Q/0.jpg)](https://www.youtube.com/watch?v=kHl5mi_ep0Q)

## Adding color
Finally, the points of the 3D reconstruction have been painted with the same color as in the images. In this way the results are more attractive and the form is easier to visualize.

To do this, a new list has been created in which the pixel color is stored when there is a point match. When painting, the 3D point and its corresponding color are passed to the plotPoint function provided.

NOTE: It is important to pass both the 3D points and the color as a list, as otherwise the 3D rendering is worse.

Adding color to the reconstruction gives the following results:

[![](https://img.youtube.com/vi/Vt-K87eSzCk/0.jpg)](https://www.youtube.com/watch?v=Vt-K87eSzCk)