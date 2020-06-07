# 3D reconstruction - First approach
In this first approach, the steps explained in the first blog post will be followed using functions from the openCV library.

The steps followed are the following:
* **Obtaining images** from both cameras in hsv using cv2.cvtColor(). Images in the hsv color space are used to achieve the best possible match.
* Obtaining the KRT matrices using the available attributes of the cameras.
* Obtaining the **border images** using cv2.Canny(). The border image is used to compare only the border areas, thus eliminate unnecessary computation.
* The two images are scanned looking for **block matches** taking into account the restriction of the epipolar and comparing only blocks where there are edges. In this way, the pairs of points to be used in the 3D reconstruction are obtained.
* Once we have gone through the image we will have two arrays of points (points of the right image and points of the left image) that will be the ones that we will use to pass to the cv2.triangulatePoints function.
* The opencv **triangulatePoints** function returns the 3D points referenced by each of the point pairs.
* In order to **paint the points** obtained, they must be passed to normalized coordinates dividing by the third component of the array that defines the point. For some reason when calculating the points in 3D, the last component had a value of 0 in all points, so it has been ignored and the values ​​have not been normalized.
* Once the points have been obtained, the function provided by Jderobot is used to paint them on the 3D stage. In this case a solid color has been used.

With this implementation the following results are obtained:
[![](https://img.youtube.com/vi/XoNR8E73cZ8/0.jpg)](https://www.youtube.com/watch?v=XoNR8E73cZ8)

As you can see, the reconstruction of the image is done in an acceptable way, which means that the relationship between points is being good, but the 3D reconstruction does not show depth, the image seems to be projected on a curved surface.

As the result obtained with cv2.triangulatePoints is not good, in the following approach we will try to implement our own triangulation algorithm.