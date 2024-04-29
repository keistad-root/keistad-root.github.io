---
title: Clustering method developed by Y. Choi
tag:
  - PID
  - Hot pixel
---

The pixel information stored as a form of array which length is 2.
`std::array<int,2>` is used for this array.
For reduce search time, the cluster information is stored into two different variable-length arraies, `std::vector<std::array<int,2>>`.
These arraies are named as `clusteredEvent` and `suspiciousCluster`.
First an cluster candidate is generated, it is appended to `suspiciousCluster`.

For any pixel to be correlated to any cluster, the difference between the mininum or maximum y-coordinate of the cluster and y-coordinate of the pixel should be less than 2.
It means that if the pixels are tested as ascending or descending order of y coordinate, 
then the cluster which y-coordinate difference with a pixel is more than 2 even once is irrelevant with following pixels.
Those clusters is passed to `clusteredEvent` and don't effect to sequencial pixels.
It is helpful to reduce significant time to search whether a pixel is related to stored cluster or not.

The next problem is to merge cluster candidates which are recorded seperately because the first pixel of later-added cluster doesn't have relationship with earlier-added cluster.
Any pixel can be linked with only two pixel which one of x- or y- coordinate is 1 less than the pixel, only which can belong to generated cluster candidates, so the maximum number of cluster with which the pixel could have correlation in the process of checking is 2.
Thus there are 3 cases to classify pixels, in the terms of uncorrelated, single-correlated and double-correlated.
If a pixel is uncorrelated, then it is stored as a new cluster candidate.
If a pixel looks like having correlation, the pixel is added to the cluster and tested one more time with other clusters.
If there are no more relation, the pixel is single-correlated, but otherwise the pixel is double-correlated, thus the later-correlated cluster is absorbed to earlier-correlated cluster.
This process is repeated to all of pixels stored in an event.
After testing, all clusters in `suspiciousCluster` is passed to `clusteredEvent` and clustering process is move on to the next event.
