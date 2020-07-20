# 3D Reconstruction - Improvements
In this blog post, different improvements will be implemented for 3D reconstruction.
* Improvement time of the calculation of the points to paint
* Centered epipolar stripe
* Search for matches in a section of the epipolar line
* Calculation of the generic epipolar line

## Improvement time of the calculation of the points to paint
In the previous implementation, search windows of a rather large size (36x36) were used, which penalized the execution time.
In this case, to calculate all the points of the image the
program took 39.58 seconds.

To improve these times, a smaller search window (6x6) has been used, thanks to which it has been obtained that the calculation of all the points is done in just 20.04 seconds.

## Centered epipolar stripe
In the previous implementation, the epipolar stripe was positioned in the upper left point, and from it, a stripe of the size indicated below was selected, leaving the reference point in the upper left.

In this new implementation, the way of going through the different rows and columns has been modified so that the center of the detection window and not the upper left corner is taken as a reference point.

## Search for matches in a section of the epipolar line
In the previous implementation, the epipolar stripe and edge detection were used as search restrictions to improve execution time.

In this implementation, a new restriction has been added whereby a search will not be made in the entire epipolar line, but a search will be made in a section of it.

Since the image on the left is being taken as a reference, the points of interest will be found to the left of the detection on the right image, that is, the search will be carried out in the area of ​​the epipolar stripe located to the left of the detection.

Along with this restriction, an offset has been added on which to search in the left area, so that if we are in the last positions, the search is not made from position 0.

## Calculation of the epipolar stripe
In the previous implementation it had been assumed that the cameras were in canonical position, which allowed calculating the epipolar stripe as the row in which the detection is located plus a small margin.

In this new implementation, an attempt has been made to generalize this calculation of the epipolar line, so that in the event that the cameras are not in a canonical position, the epipolar stripe can be obtained to search for.

For this, the following steps have been followed:
* Step to the coordinate system of the camera.
* Rear projection of the 2D point to the 3D space.
* Calculation of the rear projection ray.
* Obtaining two points of the rear projection ray in the right chamber.
* Obtaining the line connecting the two points.
* Calculation of the cut points with the axes.

Once the epipolar line was calculated using the equation of the line, an attempt was made to implement its own matchTemplate, but the results obtained were not good and the execution time was very high, which is why it was obtained by the following approximation.

The cut points of the epipolar line with the axes are calculated, respecting a certain margin to subsequently obtain the epipolar strip.

Once the cut points have been obtained, an ROI will be created using as the upper left point the intersection point between the epipolar and the left search margin and as the lower right point the intersection point between the epipolar and the detection column j (margin right).

Once the ROI is obtained, it will be used as a search region to be able to use the matchTemplate provided by OpenCV.

As explained above, the epipolar line remains centered in the search window.

## Results obtained
Once the different code improvements have been made
the following results.

[![](https://img.youtube.com/vi/9965npQqgIE/0.jpg)](https://www.youtube.com/watch?v=9965npQqgIE)
