## What is Image Stitching?
Image Stitching is the process of combining multiple photographic images with overlapping fields of view to produce a segmented panorama or high-resolution image.

In this article, we will perform image stitching from scratch.

There are several steps that we need to complete to solve this problem. First is finding key points between the image, second is warping of the image and last is drawing on the images.

## Finding key points between two images
Inside this function, we must first find the key points from the 2 images. For that, I implemented the Oriented Brief class from the open cv. This function will return key-point and descriptor values. This function uses the FAST algorithm to find image orientation using first-order moments and computes the descriptors where the coordinates of random point pairs are rotated according to the measured orientation. After that, we must match the key points from both descriptors. This function will return the matches and key points of both images. Then, we separated key points which are lower than the previous one. So that we can separate the best match among them.

## Wrapping the images
We have to transform the field of view to establish a homograph to warp the perspective. After getting the homograph perspective values, we have to perform the geometrical transformation. It does not change the image content but deforms the pixel grid and maps this deformed grid to the destination image. WarpPerspective function from the open cv performs this pixel grid transformation of an image. This function is also rounded to the nearest integer coordinates and the corresponding pixel used and this is called nearest-neighbour interpolation. This method is achieved by using more sophisticated interpolation methods.

## Draw Images
Now, we have to perform good matching points, match counts, and key points of the two images and two different images; and in return, we will get the stitched image. The below function simply checks the length of the good matching point with the minimum matching point and uses the find homography function to establish an actual homography using the RANSAC algorithm. This RANdom SAmple Consensus uses the iterative method of parameters to observe the outliers of the values. Once we get the values from this outlier algorithm, we have to pass this value to the warping function to warp the images together. 
