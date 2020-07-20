# 3D reconstruction
In the following entries, the process followed to reconstruct a 3D scene from two images will be explained.

The images from which we will obtain the 3D scene are taken as follows:

![](/data/camaras_canonicas.png)

In this way, by means of simplified epipolar geometry we can calculate the distance at which the different objects present in the image are found.

For the reconstruction the following steps will be followed:
* **Edge extraction** to simplify computation.
* **Match points of interest**
* **Triangulation of the point in 3D space**

## Triangulation
Epipolar geometry allows us to calculate the position of a point in 3D space from its projection on two calibrated cameras and the projection matrices of these cameras.

In addition, it allows us to limit the search for similarities to the epipolar stripe [1](https://es.qwe.wiki/wiki/Epipolar_geometry#Epipolar_line). In our case, since we have a pair of stereo cameras in canonical position, our epipolar stripe corresponds to the horizontal, that is, the point of the right image will be paired with a point of the left image of the same row.

## Approaches
* [First approach - cv2.triangulatePoints](https://github.com/SusanaPineda/reconstruccion_3D/blob/master/reconstruccion_v1.md)
* [Second approach - self.triangulate_points](https://github.com/SusanaPineda/reconstruccion_3D/blob/master/reconstruccion_v2.md)
* [Improvements](https://github.com/SusanaPineda/reconstruccion_3D/blob/master/reconstruccion_v3.md)