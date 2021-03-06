# imgaug

This python library helps you with augmenting images for your machine learning projects.
It converts a set of input images into a new, much larger set of slightly altered images.

[![Build Status](https://travis-ci.org/aleju/imgaug.svg?branch=master)](https://travis-ci.org/aleju/imgaug)
[![codecov](https://codecov.io/gh/aleju/imgaug/branch/master/graph/badge.svg)](https://codecov.io/gh/aleju/imgaug)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/1370ce38e99e40af842d47a8dd721444)](https://www.codacy.com/app/aleju/imgaug?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=aleju/imgaug&amp;utm_campaign=Badge_Grade)

|     | Image | Heatmaps | Seg. Maps | Keypoints | Bounding Boxes |
| --- | ----- | -------- | --------- | --------- | -------------- |
| *Original Input* | ![input image](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/noop_image.jpg?raw=true "input image") | ![input heatmap](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/noop_heatmap.jpg?raw=true "input heatmap") | ![input segmentation map](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/noop_segmap.jpg?raw=true "input segmentation map") | ![input keypoints](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/noop_kps.jpg?raw=true "input keypoints") | ![input bounding boxes](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/noop_bbs.jpg?raw=true "input bounding boxes") |
| Gauss. Noise<br>+&nbsp;Contrast<br>+&nbsp;Sharpen | ![non geometric image](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/non_geometric_image.jpg?raw=true "non geometric image") | ![non geometric heatmap](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/non_geometric_heatmap.jpg?raw=true "non geometric heatmap") | ![non geometric segmentation map](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/non_geometric_segmap.jpg?raw=true "non geometric segmentation map") | ![non geometric keypoints](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/non_geometric_kps.jpg?raw=true "non geometric keypoints") | ![non geometric bounding boxes](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/non_geometric_bbs.jpg?raw=true "non geometric bounding boxes") |
| Affine | ![affine image](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/affine_image.jpg?raw=true "affine image") | ![affine heatmap](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/affine_heatmap.jpg?raw=true "affine heatmap") | ![affine segmentation map](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/affine_segmap.jpg?raw=true "affine segmentation map") | ![affine keypoints](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/affine_kps.jpg?raw=true "affine keypoints") | ![affine bounding boxes](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/affine_bbs.jpg?raw=true "affine bounding boxes") |
| Crop<br>+&nbsp;Pad | ![cropandpad image](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/cropandpad_image.jpg?raw=true "cropandpad image") | ![cropandpad heatmap](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/cropandpad_heatmap.jpg?raw=true "cropandpad heatmap") | ![cropandpad segmentation map](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/cropandpad_segmap.jpg?raw=true "cropandpad segmentation map") | ![cropandpad keypoints](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/cropandpad_kps.jpg?raw=true "cropandpad keypoints") | ![cropandpad bounding boxes](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/cropandpad_bbs.jpg?raw=true "cropandpad bounding boxes") |
| Fliplr<br>+&nbsp;Perspective | ![fliplr perspective image](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/fliplr_perspective_image.jpg "fliplr perspective image") | ![fliplr perspective heatmap](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/fliplr_perspective_heatmap.jpg?raw=true "fliplr perspective heatmap") | ![fliplr perspective segmentation map](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/fliplr_perspective_segmap.jpg?raw=true "fliplr perspective segmentation map") | ![fliplr perspective keypoints](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/fliplr_perspective_kps.jpg?raw=true "fliplr perspective keypoints") | ![fliplr perspective bounding boxes](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/small_overview/fliplr_perspective_bbs.jpg?raw=true "fliplr perspective bounding boxes")


**More (strong) example augmentations of one input image:**

![64 quokkas](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/examples_grid.jpg?raw=true "64 quokkas")

## Features of the library

* Supports many augmentation techniques.
  * E.g. affine transformations, perspective transformations, contrast changes, gaussian noise, dropout of regions, hue/saturation changes, cropping/padding, blurring, ...
* Supports augmentation of:
  * Images (uint8)
  * Heatmaps (float32) *(Beta)*
  * Segmentation maps (integer-based, bool, float-based) *(Beta)*
  * Keypoints/Landmarks (int32 or float32 coordinates)
  * Bounding Boxes (int32 or float32 coordinates)
  * Can augment all of the above automatically with the same sampled values. E.g. rotate both images and the segmentation maps on them by the same random value sampled from `uniform(0°, 30°)`.
* Define flexible stochastic ranges for each augmentation parameter.
  * E.g. "rotate each image by a value between -45 and 45 degrees".
  * E.g. "rotate each image by `ABS(N(0, 20.0))*(1+B(1.0, 1.0))`", where `ABS(.)` is the absolute function, `N(.)` the gaussian distribution and `B(.)` the beta distribution.
* Offers many helper functions.
  * E.g. for drawing heatmaps, segmentation maps, keypoints and bounding boxes.
  * E.g. for scaling segmentation maps, average/max pooling of images/maps or for padding images to desired aspect ratios (e.g. to square them).
* Define your augmentation sequence once at the start of the experiment, then apply it many times.
* Supports augmentation on multiple CPU cores.

## Documentation
* [http://imgaug.readthedocs.io/en/latest/source/examples_basics.html](http://imgaug.readthedocs.io/en/latest/source/examples_basics.html) - Quick example code to use the library.
* [http://imgaug.readthedocs.io/en/latest/source/augmenters.html](http://imgaug.readthedocs.io/en/latest/source/augmenters.html) - Example code for each augmentation technique.
* [http://imgaug.readthedocs.io/en/latest/source/api.html](http://imgaug.readthedocs.io/en/latest/source/api.html) - API.
* This README contains more examples. See further below.

## Installation

The library supports python 2.7 and 3.4+.

To install the library, first install all requirements:
```bash
pip install six numpy scipy Pillow matplotlib scikit-image opencv-python imageio Shapely
```

Then install imgaug either via pypi (can lag behind the github version):
```bash
pip install imgaug
```

or install the latest version directly from github:
```bash
pip install git+https://github.com/aleju/imgaug
```

Alternatively, you can download the repository via `git clone https://github.com/aleju/imgaug` and install manually
via `cd imgaug && python setup.py install`.

To deinstall the library, just execute `pip uninstall imgaug`.

## Overview of most augmenters

The images below show examples for most augmentation techniques (values written in the form `(a, b)` mean that a value was randomly picked from the range `a <= x <= b`):

<table>

<tr>
<td colspan="3">

**meta**

</td>
</tr>
<tr>
<td colspan="1">
<small>
Noop
</small>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td colspan="1">

![Noop](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/noop.gif?raw=true "Noop")

</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**arithmetic**

</td>
</tr>
<tr>
<td colspan="1">
<small>
Add
</small>
</td>
<td colspan="1">
<small>
Add<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
AdditiveGaussianNoise
</small>
</td>
</tr>
<tr>
<td colspan="1">

![Add](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/add.gif?raw=true "Add")

</td>
<td colspan="1">

![Add per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/add_per_channel_true.gif?raw=true "Add per_channel=True")

</td>
<td colspan="1">

![AdditiveGaussianNoise](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/additivegaussiannoise.gif?raw=true "AdditiveGaussianNoise")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
AdditiveGaussianNoise<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
AdditiveLaplaceNoise
</small>
</td>
<td colspan="1">
<small>
AdditiveLaplaceNoise<br/>(per_channel=True)
</small>
</td>
</tr>
<tr>
<td colspan="1">

![AdditiveGaussianNoise per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/additivegaussiannoise_per_channel_true.gif?raw=true "AdditiveGaussianNoise per_channel=True")

</td>
<td colspan="1">

![AdditiveLaplaceNoise](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/additivelaplacenoise.gif?raw=true "AdditiveLaplaceNoise")

</td>
<td colspan="1">

![AdditiveLaplaceNoise per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/additivelaplacenoise_per_channel_true.gif?raw=true "AdditiveLaplaceNoise per_channel=True")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
AdditivePoissonNoise
</small>
</td>
<td colspan="1">
<small>
AdditivePoissonNoise<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
Multiply
</small>
</td>
</tr>
<tr>
<td colspan="1">

![AdditivePoissonNoise](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/additivepoissonnoise.gif?raw=true "AdditivePoissonNoise")

</td>
<td colspan="1">

![AdditivePoissonNoise per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/additivepoissonnoise_per_channel_true.gif?raw=true "AdditivePoissonNoise per_channel=True")

</td>
<td colspan="1">

![Multiply](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/multiply.gif?raw=true "Multiply")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
Multiply<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
Dropout
</small>
</td>
<td colspan="1">
<small>
Dropout<br/>(per_channel=True)
</small>
</td>
</tr>
<tr>
<td colspan="1">

![Multiply per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/multiply_per_channel_true.gif?raw=true "Multiply per_channel=True")

</td>
<td colspan="1">

![Dropout](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/dropout.gif?raw=true "Dropout")

</td>
<td colspan="1">

![Dropout per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/dropout_per_channel_true.gif?raw=true "Dropout per_channel=True")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
CoarseDropout<br/>(p=0.2)
</small>
</td>
<td colspan="1">
<small>
CoarseDropout<br/>(p=0.2, per_channel=True)
</small>
</td>
<td colspan="1">
<small>
ImpulseNoise
</small>
</td>
</tr>
<tr>
<td colspan="1">

![CoarseDropout p=0.2](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/coarsedropout_p_0_2.gif?raw=true "CoarseDropout p=0.2")

</td>
<td colspan="1">

![CoarseDropout p=0.2, per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/coarsedropout_p_0_2_per_channel_true.gif?raw=true "CoarseDropout p=0.2, per_channel=True")

</td>
<td colspan="1">

![ImpulseNoise](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/impulsenoise.gif?raw=true "ImpulseNoise")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
SaltAndPepper
</small>
</td>
<td colspan="1">
<small>
Salt
</small>
</td>
<td colspan="1">
<small>
Pepper
</small>
</td>
</tr>
<tr>
<td colspan="1">

![SaltAndPepper](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/saltandpepper.gif?raw=true "SaltAndPepper")

</td>
<td colspan="1">

![Salt](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/salt.gif?raw=true "Salt")

</td>
<td colspan="1">

![Pepper](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/pepper.gif?raw=true "Pepper")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
CoarseSaltAndPepper<br/>(p=0.2)
</small>
</td>
<td colspan="1">
<small>
CoarseSalt<br/>(p=0.2)
</small>
</td>
<td colspan="1">
<small>
CoarsePepper<br/>(p=0.2)
</small>
</td>
</tr>
<tr>
<td colspan="1">

![CoarseSaltAndPepper p=0.2](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/coarsesaltandpepper_p_0_2.gif?raw=true "CoarseSaltAndPepper p=0.2")

</td>
<td colspan="1">

![CoarseSalt p=0.2](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/coarsesalt_p_0_2.gif?raw=true "CoarseSalt p=0.2")

</td>
<td colspan="1">

![CoarsePepper p=0.2](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/coarsepepper_p_0_2.gif?raw=true "CoarsePepper p=0.2")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
Invert
</small>
</td>
<td colspan="1">
<small>
Invert<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
JpegCompression
</small>
</td>
</tr>
<tr>
<td colspan="1">

![Invert](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/invert.gif?raw=true "Invert")

</td>
<td colspan="1">

![Invert per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/invert_per_channel_true.gif?raw=true "Invert per_channel=True")

</td>
<td colspan="1">

![JpegCompression](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/jpegcompression.gif?raw=true "JpegCompression")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**blur**

</td>
</tr>
<tr>
<td colspan="1">
<small>
GaussianBlur
</small>
</td>
<td colspan="1">
<small>
AverageBlur
</small>
</td>
<td colspan="1">
<small>
MedianBlur
</small>
</td>
</tr>
<tr>
<td colspan="1">

![GaussianBlur](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/gaussianblur.gif?raw=true "GaussianBlur")

</td>
<td colspan="1">

![AverageBlur](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/averageblur.gif?raw=true "AverageBlur")

</td>
<td colspan="1">

![MedianBlur](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/medianblur.gif?raw=true "MedianBlur")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
BilateralBlur<br/>(sigma_color=250,<br/>sigma_space=250)
</small>
</td>
<td colspan="1">
<small>
MotionBlur<br/>(angle=0)
</small>
</td>
<td colspan="1">
<small>
MotionBlur<br/>(k=5)
</small>
</td>
</tr>
<tr>
<td colspan="1">

![BilateralBlur sigma_color=250, sigma_space=250](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/bilateralblur_sigma_color_250_sigma_space_250.gif?raw=true "BilateralBlur sigma_color=250, sigma_space=250")

</td>
<td colspan="1">

![MotionBlur angle=0](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/motionblur_angle_0.gif?raw=true "MotionBlur angle=0")

</td>
<td colspan="1">

![MotionBlur k=5](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/motionblur_k_5.gif?raw=true "MotionBlur k=5")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**color**

</td>
</tr>
<tr>
<td colspan="1">
<small>
AddToHueAndSaturation
</small>
</td>
<td colspan="1">
<small>
Grayscale
</small>
</td>
<td>&nbsp;</td>
</tr>
<tr>
<td colspan="1">

![AddToHueAndSaturation](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/addtohueandsaturation.gif?raw=true "AddToHueAndSaturation")

</td>
<td colspan="1">

![Grayscale](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/grayscale.gif?raw=true "Grayscale")

</td>
<td>&nbsp;</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**contrast**

</td>
</tr>
<tr>
<td colspan="1">
<small>
GammaContrast
</small>
</td>
<td colspan="1">
<small>
GammaContrast<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
SigmoidContrast<br/>(cutoff=0.5)
</small>
</td>
</tr>
<tr>
<td colspan="1">

![GammaContrast](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/gammacontrast.gif?raw=true "GammaContrast")

</td>
<td colspan="1">

![GammaContrast per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/gammacontrast_per_channel_true.gif?raw=true "GammaContrast per_channel=True")

</td>
<td colspan="1">

![SigmoidContrast cutoff=0.5](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/sigmoidcontrast_cutoff_0_5.gif?raw=true "SigmoidContrast cutoff=0.5")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
SigmoidContrast<br/>(gain=10)
</small>
</td>
<td colspan="1">
<small>
SigmoidContrast<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
LogContrast
</small>
</td>
</tr>
<tr>
<td colspan="1">

![SigmoidContrast gain=10](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/sigmoidcontrast_gain_10.gif?raw=true "SigmoidContrast gain=10")

</td>
<td colspan="1">

![SigmoidContrast per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/sigmoidcontrast_per_channel_true.gif?raw=true "SigmoidContrast per_channel=True")

</td>
<td colspan="1">

![LogContrast](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/logcontrast.gif?raw=true "LogContrast")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
LogContrast<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
LinearContrast
</small>
</td>
<td colspan="1">
<small>
LinearContrast<br/>(per_channel=True)
</small>
</td>
</tr>
<tr>
<td colspan="1">

![LogContrast per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/logcontrast_per_channel_true.gif?raw=true "LogContrast per_channel=True")

</td>
<td colspan="1">

![LinearContrast](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/linearcontrast.gif?raw=true "LinearContrast")

</td>
<td colspan="1">

![LinearContrast per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/linearcontrast_per_channel_true.gif?raw=true "LinearContrast per_channel=True")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**convolutional**

</td>
</tr>
<tr>
<td colspan="1">
<small>
Sharpen<br/>(alpha=1)
</small>
</td>
<td colspan="1">
<small>
Emboss<br/>(alpha=1)
</small>
</td>
<td colspan="1">
<small>
EdgeDetect
</small>
</td>
</tr>
<tr>
<td colspan="1">

![Sharpen alpha=1](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/sharpen_alpha_1.gif?raw=true "Sharpen alpha=1")

</td>
<td colspan="1">

![Emboss alpha=1](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/emboss_alpha_1.gif?raw=true "Emboss alpha=1")

</td>
<td colspan="1">

![EdgeDetect](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/edgedetect.gif?raw=true "EdgeDetect")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
DirectedEdgeDetect<br/>(alpha=1)
</small>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td colspan="1">

![DirectedEdgeDetect alpha=1](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/directededgedetect_alpha_1.gif?raw=true "DirectedEdgeDetect alpha=1")

</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**flip**

</td>
</tr>
<tr>
<td colspan="3">
<small>
Fliplr
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Fliplr (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/fliplr.gif?raw=true "Fliplr (+Keypoints, +BBs")![Fliplr (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/fliplr.gif?raw=true "Fliplr (heatmap augmentation)")![Fliplr (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/fliplr.gif?raw=true "Fliplr (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
Flipud
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Flipud (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/flipud.gif?raw=true "Flipud (+Keypoints, +BBs")![Flipud (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/flipud.gif?raw=true "Flipud (heatmap augmentation)")![Flipud (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/flipud.gif?raw=true "Flipud (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**geometric**

</td>
</tr>
<tr>
<td colspan="3">
<small>
Affine
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Affine (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/affine.gif?raw=true "Affine (+Keypoints, +BBs")![Affine (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/affine.gif?raw=true "Affine (heatmap augmentation)")![Affine (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/affine.gif?raw=true "Affine (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
Affine: Modes
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Affine: Modes (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/affine_modes.gif?raw=true "Affine: Modes (+Keypoints, +BBs")![Affine: Modes (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/affine_modes.gif?raw=true "Affine: Modes (heatmap augmentation)")![Affine: Modes (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/affine_modes.gif?raw=true "Affine: Modes (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
Affine: cval
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Affine: cval (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/affine_cval.gif?raw=true "Affine: cval (+Keypoints, +BBs")![Affine: cval (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/affine_cval.gif?raw=true "Affine: cval (heatmap augmentation)")![Affine: cval (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/affine_cval.gif?raw=true "Affine: cval (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
PiecewiseAffine
</small>
</td>
</tr>
<tr>
<td colspan="3">

![PiecewiseAffine (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/piecewiseaffine.gif?raw=true "PiecewiseAffine (+Keypoints, +BBs")![PiecewiseAffine (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/piecewiseaffine.gif?raw=true "PiecewiseAffine (heatmap augmentation)")![PiecewiseAffine (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/piecewiseaffine.gif?raw=true "PiecewiseAffine (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
PerspectiveTransform
</small>
</td>
</tr>
<tr>
<td colspan="3">

![PerspectiveTransform (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/perspectivetransform.gif?raw=true "PerspectiveTransform (+Keypoints, +BBs")![PerspectiveTransform (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/perspectivetransform.gif?raw=true "PerspectiveTransform (heatmap augmentation)")![PerspectiveTransform (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/perspectivetransform.gif?raw=true "PerspectiveTransform (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
ElasticTransformation<br/>(sigma=0.2)
</small>
</td>
</tr>
<tr>
<td colspan="3">

![ElasticTransformation sigma=0.2 (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/elastictransformation_sigma_0_2.gif?raw=true "ElasticTransformation sigma=0.2 (+Keypoints, +BBs")![ElasticTransformation sigma=0.2 (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/elastictransformation_sigma_0_2.gif?raw=true "ElasticTransformation sigma=0.2 (heatmap augmentation)")![ElasticTransformation sigma=0.2 (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/elastictransformation_sigma_0_2.gif?raw=true "ElasticTransformation sigma=0.2 (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
ElasticTransformation<br/>(sigma=5.0)
</small>
</td>
</tr>
<tr>
<td colspan="3">

![ElasticTransformation sigma=5.0 (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/elastictransformation_sigma_5_0.gif?raw=true "ElasticTransformation sigma=5.0 (+Keypoints, +BBs")![ElasticTransformation sigma=5.0 (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/elastictransformation_sigma_5_0.gif?raw=true "ElasticTransformation sigma=5.0 (heatmap augmentation)")![ElasticTransformation sigma=5.0 (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/elastictransformation_sigma_5_0.gif?raw=true "ElasticTransformation sigma=5.0 (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
Rot90
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Rot90 (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/rot90.gif?raw=true "Rot90 (+Keypoints, +BBs")![Rot90 (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/rot90.gif?raw=true "Rot90 (heatmap augmentation)")![Rot90 (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/rot90.gif?raw=true "Rot90 (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**overlay**

</td>
</tr>
<tr>
<td colspan="1">
<small>
Alpha<br/>with EdgeDetect(1.0)
</small>
</td>
<td colspan="1">
<small>
Alpha<br/>with EdgeDetect(1.0)<br/>(per_channel=True)
</small>
</td>
<td colspan="1">
<small>
SimplexNoiseAlpha<br/>with EdgeDetect(1.0)
</small>
</td>
</tr>
<tr>
<td colspan="1">

![Alpha with EdgeDetect1.0](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/alpha_with_edgedetect_1_0.gif?raw=true "Alpha with EdgeDetect1.0")

</td>
<td colspan="1">

![Alpha with EdgeDetect1.0 per_channel=True](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/alpha_with_edgedetect_1_0_per_channel_true.gif?raw=true "Alpha with EdgeDetect1.0 per_channel=True")

</td>
<td colspan="1">

![SimplexNoiseAlpha with EdgeDetect1.0](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/simplexnoisealpha_with_edgedetect_1_0.gif?raw=true "SimplexNoiseAlpha with EdgeDetect1.0")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
FrequencyNoiseAlpha<br/>with EdgeDetect(1.0)
</small>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td colspan="1">

![FrequencyNoiseAlpha with EdgeDetect1.0](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/frequencynoisealpha_with_edgedetect_1_0.gif?raw=true "FrequencyNoiseAlpha with EdgeDetect1.0")

</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**segmentation**

</td>
</tr>
<tr>
<td colspan="1">
<small>
Superpixels<br/>(p_replace=1)
</small>
</td>
<td colspan="1">
<small>
Superpixels<br/>(n_segments=100)
</small>
</td>
<td>&nbsp;</td>
</tr>
<tr>
<td colspan="1">

![Superpixels p_replace=1](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/superpixels_p_replace_1.gif?raw=true "Superpixels p_replace=1")

</td>
<td colspan="1">

![Superpixels n_segments=100](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/superpixels_n_segments_100.gif?raw=true "Superpixels n_segments=100")

</td>
<td>&nbsp;</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**size**

</td>
</tr>
<tr>
<td colspan="3">
<small>
CropAndPad
</small>
</td>
</tr>
<tr>
<td colspan="3">

![CropAndPad (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/cropandpad.gif?raw=true "CropAndPad (+Keypoints, +BBs")![CropAndPad (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/cropandpad.gif?raw=true "CropAndPad (heatmap augmentation)")![CropAndPad (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/cropandpad.gif?raw=true "CropAndPad (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
Crop
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Crop (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/crop.gif?raw=true "Crop (+Keypoints, +BBs")![Crop (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/crop.gif?raw=true "Crop (heatmap augmentation)")![Crop (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/crop.gif?raw=true "Crop (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
Pad
</small>
</td>
</tr>
<tr>
<td colspan="3">

![Pad (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/pad.gif?raw=true "Pad (+Keypoints, +BBs")![Pad (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/pad.gif?raw=true "Pad (heatmap augmentation)")![Pad (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/pad.gif?raw=true "Pad (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
PadToFixedSize<br/>(height'=height+32,<br/>width'=width+32)
</small>
</td>
</tr>
<tr>
<td colspan="3">

![PadToFixedSize height'=height+32, width'=width+32 (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/padtofixedsize_height_height_32_width_width_32.gif?raw=true "PadToFixedSize height'=height+32, width'=width+32 (+Keypoints, +BBs")![PadToFixedSize height'=height+32, width'=width+32 (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/padtofixedsize_height_height_32_width_width_32.gif?raw=true "PadToFixedSize height'=height+32, width'=width+32 (heatmap augmentation)")![PadToFixedSize height'=height+32, width'=width+32 (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/padtofixedsize_height_height_32_width_width_32.gif?raw=true "PadToFixedSize height'=height+32, width'=width+32 (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">
<small>
CropToFixedSize<br/>(height'=height-32,<br/>width'=width-32)
</small>
</td>
</tr>
<tr>
<td colspan="3">

![CropToFixedSize height'=height-32, width'=width-32 (+Keypoints, +BBs)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/croptofixedsize_height_height_32_width_width_32.gif?raw=true "CropToFixedSize height'=height-32, width'=width-32 (+Keypoints, +BBs")![CropToFixedSize height'=height-32, width'=width-32 (heatmap augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_heatmaps/croptofixedsize_height_height_32_width_width_32.gif?raw=true "CropToFixedSize height'=height-32, width'=width-32 (heatmap augmentation)")![CropToFixedSize height'=height-32, width'=width-32 (segmentation map augmentation)](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_segmentation_maps/croptofixedsize_height_height_32_width_width_32.gif?raw=true "CropToFixedSize height'=height-32, width'=width-32 (segmentation map augmentation)")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="3">

**weather**

</td>
</tr>
<tr>
<td colspan="1">
<small>
FastSnowyLandscape<br/>(lightness_multiplier=2.0)
</small>
</td>
<td colspan="1">
<small>
Clouds
</small>
</td>
<td colspan="1">
<small>
Fog
</small>
</td>
</tr>
<tr>
<td colspan="1">

![FastSnowyLandscape lightness_multiplier=2.0](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/fastsnowylandscape_lightness_multiplier_2_0.gif?raw=true "FastSnowyLandscape lightness_multiplier=2.0")

</td>
<td colspan="1">

![Clouds](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/clouds.gif?raw=true "Clouds")

</td>
<td colspan="1">

![Fog](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/fog.gif?raw=true "Fog")

</td>
</tr>
<tr>

</tr>
<tr>
<td colspan="1">
<small>
Snowflakes
</small>
</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td colspan="1">

![Snowflakes](https://raw.githubusercontent.com/aleju/imgaug-doc/master/readme_images/augmenter_videos/augment_images_with_coordsaug/snowflakes.gif?raw=true "Snowflakes")

</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>

</tr>

</table>


## Code Examples

A standard machine learning situation.
Train on batches of images and augment each batch via crop, horizontal flip ("Fliplr") and gaussian blur:
```python
from imgaug import augmenters as iaa

seq = iaa.Sequential([
    iaa.Crop(px=(0, 16)), # crop images from each side by 0 to 16px (randomly chosen)
    iaa.Fliplr(0.5), # horizontally flip 50% of the images
    iaa.GaussianBlur(sigma=(0, 3.0)) # blur images with a sigma of 0 to 3.0
])

for batch_idx in range(1000):
    # 'images' should be either a 4D numpy array of shape (N, height, width, channels)
    # or a list of 3D numpy arrays, each having shape (height, width, channels).
    # Grayscale images must have shape (height, width, 1) each.
    # All images must have numpy's dtype uint8. Values are expected to be in
    # range 0-255.
    images = load_batch(batch_idx)  # you have to implement this function
    images_aug = seq.augment_images(images)  # done by the library
    train_on_images(images_aug)  # you have to implement this function
```

Apply heavy augmentations to images (used to create the image at the very top of this readme):
```python
import imgaug as ia
from imgaug import augmenters as iaa
import numpy as np

# random example images
images = np.random.randint(0, 255, (16, 128, 128, 3), dtype=np.uint8)

# Sometimes(0.5, ...) applies the given augmenter in 50% of all cases,
# e.g. Sometimes(0.5, GaussianBlur(0.3)) would blur roughly every second image.
sometimes = lambda aug: iaa.Sometimes(0.5, aug)

# Define our sequence of augmentation steps that will be applied to every image
# All augmenters with per_channel=0.5 will sample one value _per image_
# in 50% of all cases. In all other cases they will sample new values
# _per channel_.
seq = iaa.Sequential(
    [
        # apply the following augmenters to most images
        iaa.Fliplr(0.5), # horizontally flip 50% of all images
        iaa.Flipud(0.2), # vertically flip 20% of all images
        # crop images by -5% to 10% of their height/width
        sometimes(iaa.CropAndPad(
            percent=(-0.05, 0.1),
            pad_mode=ia.ALL,
            pad_cval=(0, 255)
        )),
        sometimes(iaa.Affine(
            scale={"x": (0.8, 1.2), "y": (0.8, 1.2)}, # scale images to 80-120% of their size, individually per axis
            translate_percent={"x": (-0.2, 0.2), "y": (-0.2, 0.2)}, # translate by -20 to +20 percent (per axis)
            rotate=(-45, 45), # rotate by -45 to +45 degrees
            shear=(-16, 16), # shear by -16 to +16 degrees
            order=[0, 1], # use nearest neighbour or bilinear interpolation (fast)
            cval=(0, 255), # if mode is constant, use a cval between 0 and 255
            mode=ia.ALL # use any of scikit-image's warping modes (see 2nd image from the top for examples)
        )),
        # execute 0 to 5 of the following (less important) augmenters per image
        # don't execute all of them, as that would often be way too strong
        iaa.SomeOf((0, 5),
            [
                sometimes(iaa.Superpixels(p_replace=(0, 1.0), n_segments=(20, 200))), # convert images into their superpixel representation
                iaa.OneOf([
                    iaa.GaussianBlur((0, 3.0)), # blur images with a sigma between 0 and 3.0
                    iaa.AverageBlur(k=(2, 7)), # blur image using local means with kernel sizes between 2 and 7
                    iaa.MedianBlur(k=(3, 11)), # blur image using local medians with kernel sizes between 2 and 7
                ]),
                iaa.Sharpen(alpha=(0, 1.0), lightness=(0.75, 1.5)), # sharpen images
                iaa.Emboss(alpha=(0, 1.0), strength=(0, 2.0)), # emboss images
                # search either for all edges or for directed edges,
                # blend the result with the original image using a blobby mask
                iaa.SimplexNoiseAlpha(iaa.OneOf([
                    iaa.EdgeDetect(alpha=(0.5, 1.0)),
                    iaa.DirectedEdgeDetect(alpha=(0.5, 1.0), direction=(0.0, 1.0)),
                ])),
                iaa.AdditiveGaussianNoise(loc=0, scale=(0.0, 0.05*255), per_channel=0.5), # add gaussian noise to images
                iaa.OneOf([
                    iaa.Dropout((0.01, 0.1), per_channel=0.5), # randomly remove up to 10% of the pixels
                    iaa.CoarseDropout((0.03, 0.15), size_percent=(0.02, 0.05), per_channel=0.2),
                ]),
                iaa.Invert(0.05, per_channel=True), # invert color channels
                iaa.Add((-10, 10), per_channel=0.5), # change brightness of images (by -10 to 10 of original value)
                iaa.AddToHueAndSaturation((-20, 20)), # change hue and saturation
                # either change the brightness of the whole image (sometimes
                # per channel) or change the brightness of subareas
                iaa.OneOf([
                    iaa.Multiply((0.5, 1.5), per_channel=0.5),
                    iaa.FrequencyNoiseAlpha(
                        exponent=(-4, 0),
                        first=iaa.Multiply((0.5, 1.5), per_channel=True),
                        second=iaa.ContrastNormalization((0.5, 2.0))
                    )
                ]),
                iaa.ContrastNormalization((0.5, 2.0), per_channel=0.5), # improve or worsen the contrast
                iaa.Grayscale(alpha=(0.0, 1.0)),
                sometimes(iaa.ElasticTransformation(alpha=(0.5, 3.5), sigma=0.25)), # move pixels locally around (with random strengths)
                sometimes(iaa.PiecewiseAffine(scale=(0.01, 0.05))), # sometimes move parts of the image around
                sometimes(iaa.PerspectiveTransform(scale=(0.01, 0.1)))
            ],
            random_order=True
        )
    ],
    random_order=True
)

images_aug = seq.augment_images(images)
```

Quickly show example results of your augmentation sequence:
```python
from imgaug import augmenters as iaa
import numpy as np

images = np.random.randint(0, 255, (16, 128, 128, 3), dtype=np.uint8)
seq = iaa.Sequential([iaa.Fliplr(0.5), iaa.GaussianBlur((0, 3.0))])

# show an image with 8*8 augmented versions of image 0
seq.show_grid(images[0], cols=8, rows=8)

# Show an image with 8*8 augmented versions of image 0 and 8*8 augmented
# versions of image 1. The identical augmentations will be applied to
# image 0 and 1.
seq.show_grid([images[0], images[1]], cols=8, rows=8)
```

Augment two batches of images in *exactly the same way* (e.g. horizontally flip 1st, 2nd and 5th images in both batches, but do not alter 3rd and 4th images):
```python
from imgaug import augmenters as iaa

# Standard scenario: You have N RGB-images and additionally 21 heatmaps per image.
# You want to augment each image and its heatmaps identically.
images = np.random.randint(0, 255, (16, 128, 128, 3), dtype=np.uint8)
heatmaps = np.random.randint(0, 255, (16, 128, 128, 21), dtype=np.uint8)

seq = iaa.Sequential([iaa.GaussianBlur((0, 3.0)), iaa.Affine(translate_px={"x": (-40, 40)})])

# Convert the stochastic sequence of augmenters to a deterministic one.
# The deterministic sequence will always apply the exactly same effects to the images.
seq_det = seq.to_deterministic() # call this for each batch again, NOT only once at the start
images_aug = seq_det.augment_images(images)
heatmaps_aug = seq_det.augment_images(heatmaps)
```

Augment images *and* **landmarks/keypoints** on these images:
```python
import imgaug as ia
from imgaug import augmenters as iaa
import random
import numpy as np
images = np.random.randint(0, 50, (4, 128, 128, 3), dtype=np.uint8)

# Generate random keypoints.
# The augmenters expect a list of imgaug.KeypointsOnImage.
keypoints_on_images = []
for image in images:
    height, width = image.shape[0:2]
    keypoints = []
    for _ in range(4):
        x = random.randint(0, width-1)
        y = random.randint(0, height-1)
        keypoints.append(ia.Keypoint(x=x, y=y))
    keypoints_on_images.append(ia.KeypointsOnImage(keypoints, shape=image.shape))

seq = iaa.Sequential([iaa.GaussianBlur((0, 3.0)), iaa.Affine(scale=(0.5, 0.7))])
seq_det = seq.to_deterministic() # call this for each batch again, NOT only once at the start

# augment keypoints and images
images_aug = seq_det.augment_images(images)
keypoints_aug = seq_det.augment_keypoints(keypoints_on_images)

# Example code to show each image and print the new keypoints coordinates
for img_idx, (image_before, image_after, keypoints_before, keypoints_after) in enumerate(zip(images, images_aug, keypoints_on_images, keypoints_aug)):
    image_before = keypoints_before.draw_on_image(image_before)
    image_after = keypoints_after.draw_on_image(image_after)
    ia.imshow(np.concatenate((image_before, image_after), axis=1)) # before and after
    for kp_idx, keypoint in enumerate(keypoints_after.keypoints):
        keypoint_old = keypoints_on_images[img_idx].keypoints[kp_idx]
        x_old, y_old = keypoint_old.x, keypoint_old.y
        x_new, y_new = keypoint.x, keypoint.y
        print("[Keypoints for image #%d] before aug: x=%d y=%d | after aug: x=%d y=%d" % (img_idx, x_old, y_old, x_new, y_new))
```

Apply single augmentations to images:
```python
from imgaug import augmenters as iaa
import numpy as np
images = np.random.randint(0, 255, (16, 128, 128, 3), dtype=np.uint8)

flipper = iaa.Fliplr(1.0) # always horizontally flip each input image
images[0] = flipper.augment_image(images[0]) # horizontally flip image 0

vflipper = iaa.Flipud(0.9) # vertically flip each input image with 90% probability
images[1] = vflipper.augment_image(images[1]) # probably vertically flip image 1

blurer = iaa.GaussianBlur(3.0)
images[2] = blurer.augment_image(images[2]) # blur image 2 by a sigma of 3.0
images[3] = blurer.augment_image(images[3]) # blur image 3 by a sigma of 3.0 too

translater = iaa.Affine(translate_px={"x": -16}) # move each input image by 16px to the left
images[4] = translater.augment_image(images[4]) # move image 4 to the left

scaler = iaa.Affine(scale={"y": (0.8, 1.2)}) # scale each input image to 80-120% on the y axis
images[5] = scaler.augment_image(images[5]) # scale image 5 by 80-120% on the y axis
```

Apply an augmenter to only specific image channels:
```python
from imgaug import augmenters as iaa
import numpy as np

# fake RGB images
images = np.random.randint(0, 255, (16, 128, 128, 3), dtype=np.uint8)

# add a random value from the range (-30, 30) to the first two channels of
# input images (e.g. to the R and G channels)
aug = iaa.WithChannels(
  channels=[0, 1],
  children=iaa.Add((-30, 30))
)

images_aug = aug.augment_images(images)
```

You can use more unusual distributions for the stochastic parameters of each augmenter:
```python
from imgaug import augmenters as iaa
from imgaug import parameters as iap
import numpy as np
images = np.random.randint(0, 255, (16, 128, 128, 3), dtype=np.uint8)

# Blur by a value sigma which is sampled from a uniform distribution
# of range 0.1 <= x < 3.0.
# The convenience shortcut for this is: iaa.GaussianBlur((0.1, 3.0))
blurer = iaa.GaussianBlur(iap.Uniform(0.1, 3.0))
images_aug = blurer.augment_images(images)

# Blur by a value sigma which is sampled from a normal distribution N(1.0, 0.1),
# i.e. sample a value that is usually around 1.0.
# Clip the resulting value so that it never gets below 0.1 or above 3.0.
blurer = iaa.GaussianBlur(iap.Clip(iap.Normal(1.0, 0.1), 0.1, 3.0))
images_aug = blurer.augment_images(images)

# Same again, but this time the mean of the normal distribution is not constant,
# but comes itself from a uniform distribution between 0.5 and 1.5.
blurer = iaa.GaussianBlur(iap.Clip(iap.Normal(iap.Uniform(0.5, 1.5), 0.1), 0.1, 3.0))
images_aug = blurer.augment_images(images)

# Use for sigma one of exactly three allowed values: 0.5, 1.0 or 1.5.
blurer = iaa.GaussianBlur(iap.Choice([0.5, 1.0, 1.5]))
images_aug = blurer.augment_images(images)

# Sample sigma from a discrete uniform distribution of range 1 <= sigma <= 5,
# i.e. sigma will have any of the following values: 1, 2, 3, 4, 5.
blurer = iaa.GaussianBlur(iap.DiscreteUniform(1, 5))
images_aug = blurer.augment_images(images)
```

You can **dynamically deactivate augmenters** in an already defined sequence:
```python
import imgaug as ia
from imgaug import augmenters as iaa
import numpy as np

# images and heatmaps, just arrays filled with value 30
images = np.ones((16, 128, 128, 3), dtype=np.uint8) * 30
heatmaps = np.ones((16, 128, 128, 21), dtype=np.uint8) * 30

# add vertical lines to see the effect of flip
images[:, 16:128-16, 120:124, :] = 120
heatmaps[:, 16:128-16, 120:124, :] = 120

seq = iaa.Sequential([
  iaa.Fliplr(0.5, name="Flipper"),
  iaa.GaussianBlur((0, 3.0), name="GaussianBlur"),
  iaa.Dropout(0.02, name="Dropout"),
  iaa.AdditiveGaussianNoise(scale=0.01*255, name="MyLittleNoise"),
  iaa.AdditiveGaussianNoise(loc=32, scale=0.0001*255, name="SomeOtherNoise"),
  iaa.Affine(translate_px={"x": (-40, 40)}, name="Affine")
])

# change the activated augmenters for heatmaps,
# we only want to execute horizontal flip, affine transformation and one of
# the gaussian noises
def activator_heatmaps(images, augmenter, parents, default):
    if augmenter.name in ["GaussianBlur", "Dropout", "MyLittleNoise"]:
        return False
    else:
        # default value for all other augmenters
        return default
hooks_heatmaps = ia.HooksImages(activator=activator_heatmaps)

seq_det = seq.to_deterministic() # call this for each batch again, NOT only once at the start
images_aug = seq_det.augment_images(images)
heatmaps_aug = seq_det.augment_images(heatmaps, hooks=hooks_heatmaps)
```

Images can be augmented in **background processes** using the method `augment_batches(batches, background=True)`,
where `batches` is expected to be a list of image batches or a list of batches/lists of `imgaug.KeypointsOnImage` or a list of `imgaug.Batch`.
The following example augments a list of image batches in the background:
```python
import imgaug as ia
from imgaug import augmenters as iaa
import numpy as np
from skimage import data

# Number of batches and batch size for this example
nb_batches = 10
batch_size = 32

# Example augmentation sequence to run in the background
augseq = iaa.Sequential([
    iaa.Fliplr(0.5),
    iaa.CoarseDropout(p=0.1, size_percent=0.1)
])

# For simplicity, we use the same image here many times
astronaut = data.astronaut()
astronaut = ia.imresize_single_image(astronaut, (64, 64))

# Make batches out of the example image (here: 10 batches, each 32 times
# the example image)
batches = []
for _ in range(nb_batches):
    batches.append(
        np.array(
            [astronaut for _ in range(batch_size)],
            dtype=np.uint8
        )
    )

# Show the augmented images.
# Note that augment_batches() returns a generator.
for images_aug in augseq.augment_batches(batches, background=True):
    ia.imshow(ia.draw_grid(images_aug, cols=8))
```

Images can also be augmented in background processes using the classes `imgaug.BatchLoader` and `imgaug.BackgroundAugmenter`,
which offer a bit more flexibility. (`augment_batches()` is a wrapper around these.)
Using these classes is good practice, when you have a lot of images that you don't want to load at the same time.
```python
import imgaug as ia
from imgaug import augmenters as iaa
import numpy as np
from skimage import data

# Example augmentation sequence to run in the background.
augseq = iaa.Sequential([
    iaa.Fliplr(0.5),
    iaa.CoarseDropout(p=0.1, size_percent=0.1)
])

# A generator that loads batches from the hard drive.
def load_batches():
    # Here, load 10 batches of size 4 each.
    # You can also load an infinite amount of batches, if you don't train
    # in epochs.
    batch_size = 4
    nb_batches = 10

    # Here, for simplicity we just always use the same image.
    astronaut = data.astronaut()
    astronaut = ia.imresize_single_image(astronaut, (64, 64))

    for i in range(nb_batches):
        # A list containing all images of the batch.
        batch_images = []
        # A list containing IDs of images in the batch. This is not necessary
        # for the background augmentation and here just used to showcase that
        # you can transfer additional information.
        batch_data = []

        # Add some images to the batch.
        for b in range(batch_size):
            batch_images.append(astronaut)
            batch_data.append((i, b))

        # Create the batch object to send to the background processes.
        batch = ia.Batch(
            images=np.array(batch_images, dtype=np.uint8),
            data=batch_data
        )

        yield batch

# background augmentation consists of two components:
#  (1) BatchLoader, which runs in a Thread and calls repeatedly a user-defined
#      function (here: load_batches) to load batches (optionally with keypoints
#      and additional information) and sends them to a queue of batches.
#  (2) BackgroundAugmenter, which runs several background processes (on other
#      CPU cores). Each process takes batches from the queue defined by (1),
#      augments images/keypoints and sends them to another queue.
# The main process can then read augmented batches from the queue defined
# by (2).
batch_loader = ia.BatchLoader(load_batches)
bg_augmenter = ia.BackgroundAugmenter(batch_loader, augseq)

# Run until load_batches() returns nothing anymore. This also allows infinite
# training.
while True:
    print("Next batch...")
    batch = bg_augmenter.get_batch()
    if batch is None:
        print("Finished epoch.")
        break
    images_aug = batch.images_aug

    print("Image IDs: ", batch.data)

    ia.imshow(np.hstack(list(images_aug)))

batch_loader.terminate()
bg_augmenter.terminate()
```

## List of augmenters

The following is a list of available augmenters.
Note that most of the below mentioned variables can be set to ranges, e.g. `A=(0.0, 1.0)` to sample a random value between 0 and 1.0 per image,
or `A=[0.0, 0.5, 1.0]` to sample randomly either `0.0` or `0.5` or `1.0` per image.

**arithmetic**

| Augmenter | Description |
| --- | --- |
| Add(V, PCH) | Adds value `V` to each image. If `PCH` is true, then the the sampled values may be different per channel. |
| AddElementwise(V, PCH) | Adds value `V` to each pixel. If `PCH` is true, then the the sampled values may be different per channel (and pixel). |
| AdditiveGaussianNoise(L, S, PCH) | Adds white/gaussian noise pixelwise to an image. The noise comes from the normal distribution `N(L,S)`. If `PCH` is true, then the sampled values may be different per channel (and pixel). |
| AdditiveLaplaceNoise(L, S, PCH) | Adds noise sampled from a laplace distribution following `Laplace(L, S)` to images. If `PCH` is true, then the sampled values may be different per channel (and pixel). |
| AdditivePoissonNoise(L, PCH) | Adds noise sampled from a poisson distribution with `L` being the `lambda` exponent. If `PCH` is true, then the sampled values may be different per channel (and pixel). |
| Multiply(V, PCH) | Multiplies each image by value `V`, leading to darker/brighter images. If `PCH` is true, then the sampled values may be different per channel. |
| MultiplyElementwise(V, PCH) | Multiplies each pixel by value `V`, leading to darker/brighter pixels. If `PCH` is true, then the sampled values may be different per channel (and pixel). |
| Dropout(P, PCH) | Sets pixels to zero with probability `P`. If `PCH` is true, then channels may be treated differently, otherwise whole pixels are set to zero. |
| CoarseDropout(P, SPX, SPC, PCH) | Like `Dropout`, but samples the locations of pixels that are to be set to zero from a coarser/smaller image, which has pixel size `SPX` or relative size `SPC`. I.e. if `SPC` has a small value, the coarse map is small, resulting in large rectangles being dropped. |
| ReplaceElementwise(M, R, PCH) | Replaces pixels in an image by replacements `R`. Replaces the pixels identified by mask `M`. `M` can be a probability, e.g. `0.05` to replace 5% of all pixels. If `PCH` is true, then the mask will be sampled per image, pixel *and additionally channel*. |
| ImpulseNoise(P) | Replaces `P` percent of all pixels with impulse noise, i.e. very light/dark RGB colors. This is an alias for `SaltAndPepper(P, PCH=True)`. |
| SaltAndPepper(P, PCH) | Replaces `P` percent of all pixels with very white or black colors. If `PCH` is true, then different pixels will be replaced per channel. |
| CoarseSaltAndPepper(P, SPX, SPC, PCH) | Similar to `CoarseDropout`, but instead of setting regions to zero, they are replaced by very white or black colors. If `PCH` is true, then the coarse replacement masks are sampled once per image and channel. |
| Salt(P, PCH) | Similar to `SaltAndPepper`, but only replaces with very white colors, i.e. no black colors. |
| CoarseSalt(P, SPX, SPC, PCH) | Similar to `CoarseSaltAndPepper`, but only replaces with very white colors, i.e. no black colors. |
| Pepper(P, PCH) | Similar to `SaltAndPepper`, but only replaces with very black colors, i.e. no white colors. |
| CoarsePepper(P, SPX, SPC, PCH) | Similar to `CoarseSaltAndPepper`, but only replaces with very black colors, i.e. no white colors. |
| Invert(P, PCH) | Inverts with probability `P` all pixels in an image, i.e. sets them to (1-pixel_value). If `PCH` is true, each channel is treated individually (leading to only some channels being inverted). |
| ContrastNormalization(S, PCH) | Changes the contrast in images, by moving pixel values away or closer to 128. The direction and strength is defined by `S`. If `PCH` is set to true, the process happens channel-wise with possibly different `S`. |
| JpegCompression(C) | Applies JPEG compression of strength `C` (value range: 0 to 100) to an image. Higher values of `C` lead to more visual artifacts. |


**blur**

| Augmenter | Description |
| --- | --- |
| GaussianBlur(S) | Blurs images using a gaussian kernel with size `S`. |
| AverageBlur(K) | Blurs images using a simple averaging kernel with size `K`. |
| MedianBlur(K) | Blurs images using a median over neihbourhoods of size `K`. |
| BilateralBlur(D, SC, SS) | Blurs images using a bilateral filter with distance `D` (like kernel size). `SC` is a sigma for the (influence) distance in color space, `SS` a sigma for the spatial distance. |
| MotionBlur(K, A, D, O) | Blurs an image using a motion blur kernel with size `K`. `A` is the angle of the blur in degrees to the y-axis (value range: 0 to 360, clockwise). `D` is the blur direction (value range: -1.0 to 1.0, 1.0 is forward from the center). `O` is the interpolation order (`O=0` is fast, `O=1` slightly slower but more accurate). |


**color**

| Augmenter | Description |
| --- | --- |
| WithColorspace(T, F, CH) | Converts images from colorspace `T` to `F`, applies child augmenters `CH` and then converts back from `F` to `T`. |
| AddToHueAndSaturation(V, PCH, F, C) | Adds value `V` to each pixel in HSV space (i.e. modifying hue and saturation). Converts from colorspace F to HSV (default is F=RGB). Selects channels C before augmenting (default is C=[0,1]). If `PCH` is true, then the the sampled values may be different per channel. |
| ChangeColorspace(T, F, A) | Converts images from colorspace `F` to `T` and mixes with the original image using alpha `A`. Grayscale remains at three channels. (Fairly untested augmenter, use at own risk.) |
| Grayscale(A, F) | Converts images from colorspace F (default: RGB) to grayscale and mixes with the original image using alpha `A`. |


**contrast**

| Augmenter | Description |
| --- | --- |
| GammaContrast(G, PCH) | Applies gamma contrast adjustment following `I_ij' = I_ij**G'`, where `G'` is a gamma value sampled from `G` and `I_ij` a pixel (converted to 0 to 1.0 space). If `PCH` is true, a different `G'` is sampled per image and channel. |
| SigmoidContrast(G, C, PCH) | Similar to GammaContrast, but applies `I_ij' = 1/(1 + exp(G' * (C' - I_ij)))`, where `G'` is a gain value sampled from `G` and `C'` is a cutoff value sampled from `C`. |
| LogContrast(G, PCH) | Similar to GammaContrast, but applies `I_ij = G' * log(1 + I_ij)`, where `G'` is a gain value sampled from `G`. |
| LinearContrast(S, PCH) | Similar to GammaContrast, but applies `I_ij = 128 + S' * (I_ij - 128)`, where `S'` is a strength value sampled from `S`. This augmenter is identical to ContrastNormalization (which will be deprecated in the future). |


**convolutional**

| Augmenter | Description |
| --- | --- |
| Convolve(M) | Convolves images with matrix `M`, which can be a lambda function. |
| Sharpen(A, L) | Runs a sharpening kernel over each image with lightness `L` (low values result in dark images). Mixes the result with the original image using alpha `A`. |
| Emboss(A, S) | Runs an emboss kernel over each image with strength `S`. Mixes the result with the original image using alpha `A`. |
| EdgeDetect(A) | Runs an edge detection kernel over each image. Mixes the result with the original image using alpha `A`. |
| DirectedEdgeDetect(A, D) | Runs a directed edge detection kernel over each image, which detects each from direction `D` (default: random direction from 0 to 360 degrees, chosen per image). Mixes the result with the original image using alpha `A`. |


**flip**

| Augmenter | Description |
| --- | --- |
| Fliplr(P) | Horizontally flips images with probability `P`. |
| Flipud(P) | Vertically flips images with probability `P`. |


**geometric**

| Augmenter | Description |
| --- | --- |
| Affine(S, TPX, TPC, R, SH, O, CVAL, FO, M, B) | Applies affine transformations to images. Scales them by `S` (>1=zoom in, <1=zoom out), translates them by `TPX` pixels or `TPC` percent, rotates them by `R` degrees and shears them by `SH` degrees. Interpolation happens with order `O` (0 or 1 are good and fast). If `FO` is true, the output image plane size will be fitted to the distorted image size, i.e. images rotated by 45deg will not be partially outside of the image plane. `M` controls how to handle pixels in the output image plane that have no correspondence in the input image plane. If `M='constant'` then `CVAL` defines a constant value with which to fill these pixels. `B` allows to set the backend framework (currently `cv2` or `skimage`). |
| AffineCv2(S, TPX, TPC, R, SH, O, CVAL, M, B) | Same as Affine, but uses only `cv2` as its backend. Currently does not support `FO=true`. Might be deprecated in the future. |
| PiecewiseAffine(S, R, C, O, M, CVAL) | Places a regular grid of points on the image. The grid has `R` rows and `C` columns. Then moves the points (and the image areas around them) by amounts that are samples from normal distribution N(0,`S`), leading to local distortions of varying strengths. `O`, `M` and `CVAL` are defined as in `Affine`. |
| PerspectiveTransform(S, KS) | Applies a random four-point perspective transform to the image (kinda like an advanced form of cropping). Each point has a random distance from the image corner, derived from a normal distribution with sigma `S`. If `KS` is set to True (default), each image will be resized back to its original size. |
| ElasticTransformation(S, SM, O, CVAL, M) | Moves each pixel individually around based on distortion fields. `SM` defines the smoothness of the distortion field and `S` its strength. `O` is the interpolation order, `CVAL` a constant fill value for newly created pixels and `M` the fill mode (see also augmenter `Affine`). |
| Rot90(K, KS) | Rotate images `K` times by 90 degrees. (This is faster than `Affine`.) If `KS` is true, the resulting image will be resized to have the same size as the original input image. |


**meta**

| Augmenter | Description |
| --- | --- |
| Sequential(C, R) | Takes a list of child augmenters `C` and applies them in that order to images. If `R` is true (default: false), then the order is random (chosen once per batch). |
| SomeOf(N, C, R) | Applies `N` randomly selected augmenters from from a list of augmenters `C` to each image. The augmenters are chosen per image. `R` is the same as for `Sequential`. `N` can be a range, e.g. `(1, 3)` in order to pick 1 to 3. |
| OneOf(C) | Identical to `SomeOf(1, C)`. |
| Sometimes(P, C, D) | Augments images with probability `P` by using child augmenters `C`, otherwise uses `D`. `D` can be None, then only `P` percent of all images are augmented via `C`. |
| WithColorspace(T, F, C) | Transforms images from colorspace `F` (default: RGB) to colorspace `T`, applies augmenters `C` and then converts back to `F`. |
| WithChannels(H, C) | Selects from each image channels `H` (e.g. `[0,1]` for red and green in RGB images), applies child augmenters `C` to these channels and merges the result back into the original images. |
| Noop() | Does nothing. (Useful for validation/test.) |
| Lambda(I, K) | Applies lambda function `I` to images and `K` to keypoints. |
| AssertLambda(I, K) | Checks images via lambda function `I` and keypoints via `K` and raises an error if false is returned by either of them. |
| AssertShape(S) | Raises an error if input images are not of shape `S`. |


**overlay**

| Augmenter | Description |
| --- | --- |
| Alpha(F, A, B, PCH) | Augments images using augmenters `A` and `B` independently, then overlays the result using alpha `F`. Both `A` and `B` default to doing nothing if not provided. E.g. use `Alpha(0.9, A)` to augment images via `A`, then blend the result, keeping 10% of the original image (before `A`). If `PCH` is set to true, the process happens channel-wise with possibly different `F` (`A` and `B` are computed once per image). |
| AlphaElementwise(F, A, B, PCH) | Same as `Alpha`, but performs the blending pixel-wise using a continuous mask (values 0.0 to 1.0) sampled from `F`. If `PCH` is set to true, the process happens both pixel- and channel-wise. |
| SimplexNoiseAlpha(A, B, PCH, SM, UP, I, AGG, SIG, SIGT) | Similar to `Alpha`, but uses a mask to blend the results from augmenters `A` and `B`. The mask is sampled from simplex noise, which tends to be blobby. The mask is gathered in `I` iterations (default 1-3), each iteration is combined using aggregation method `AGG` (default max, i.e. maximum value from all iterations per pixel). Each mask is sampled in low resolution space with max resolution `SM` (default 2 to 16px) and upscaled to image size using method `UP` (default: linear or cubic or nearest neighbour upsampling). If `SIG` is true, a sigmoid is applied to the mask with threshold `SIGT`, which makes the blobs have values closer to 0.0 or 1.0. |
| FrequencyNoiseAlpha(E, A, B, PCH, SM, UP, I, AGG, SIG, SIGT) | Similar to `SimplexNoiseAlpha`, but generates noise masks from the frequency domain. Exponent `E` is used to increase/decrease frequency components. High values lead to more pronounced high frequency components. Use values in the range -4 to 4, with -2 roughly generated cloud-like patterns. |


**segmentation**

| Augmenter | Description |
| --- | --- |
| Superpixels(P, N, M) | Generates N superpixels of the image at (max) resolution M and resizes back to the original size. Then `P` percent of all superpixel areas in the original image are replaced by the superpixel. (1-P) percent remain unaltered. |


**size**

| Augmenter | Description |
| --- | --- |
| Scale(S, I) | Resizes images to size `S`. Common use case would be to use `S={"height":H, "width":W}` to resize all images to shape `HxW`. `H` and `W` may be floats (e.g. resize to `50%` of original size). Either `H` or `W` may be `"keep-aspect-ratio"` to define only one side's new size and resize the other side correspondingly. `I` is the interpolation to use (default: `cubic`). |
| CropAndPad(PX, PC, PM, PCV, KS) | Crops away or pads `PX` pixels or `PC` percent of pixels at top/right/bottom/left of images. Negative values result in cropping, positive in padding. `PM` defines the pad mode (e.g. use uniform color for all added pixels). `PCV` controls the color of added pixels if `PM=constant`. If `KS` is true (default), the resulting image is resized back to the original size. |
| Pad(PX, PC, PM, PCV, KS) | Shortcut for CropAndPad(), which only adds pixels. Only positive values are allowed for `PX` and `PC`. |
| Crop(PX, PC, KS) | Shortcut for CropAndPad(), which only crops away pixels. Only positive values are allowed for `PX` and `PC` (e.g. a value of 5 results in 5 pixels cropped away). |
| PadToFixedSize(W, H, PM, PCV, POS) | Pads all images up to height `H` and width `W`. `PM` and `PCV` are the same as in `Pad`. `POS` defines the position around which to pad, e.g. `POS="center"` pads equally on all sides, `POS="left-top"` pads only the top and left sides. |
| CropToFixedSize(W, H, POS) | Similar to `PadToFixedSize`, but crops down to height `H` and width `W` instead of padding. |
| KeepSizeByResize(CH, I, IH) | Applies child augmenters `CH` (e.g. cropping) and afterwards resizes all images back to their original size. `I` is the interpolation used for images, `IH` the interpolation used for heatmaps. |


**weather**

| Augmenter | Description |
| --- | --- |
| FastSnowyLandscape(LT, LM) | Converts landscape images to snowy landscapes by increasing in HLS colorspace the lightness `L` of all pixels with `L<LT` by a factor of `LM`. |
| Clouds() | Adds clouds of various shapes and densities to images. Can be senseful to be combined with an *overlay* augmenter, e.g. `SimplexNoiseAlpha`. |
| Fog() | Adds fog-like cloud structures of various shapes and densities to images. Can be senseful to be combined with an *overlay* augmenter, e.g. `SimplexNoiseAlpha`. |
| CloudLayer(IM, IFE, ICS, AMIN, AMUL, ASPXM, AFE, S, DMUL) | Adds a single layer of clouds to an image. `IM` is the mean intensity of the clouds, `IFE` a frequency noise exponent for the intensities (leading to non-uniform colors), `ICS` controls the variance of a gaussian for intensity sampling, `AM` is the minimum opacity of the clouds (values >0 are typical of fog), `AMUL` a multiplier for opacity values, `ASPXM` controls the minimum grid size at which to sample opacity values, `AFE` is a frequency noise exponent for opacity values, `S` controls the sparsity of clouds and `DMUL` is a cloud density multiplier. This interface is not final and will likely change in the future. |
| Snowflakes(D, DU, FS, FSU, A, S) | Adds snowflakes with density `D`, density uniformity `DU`, snowflake size `FS`, snowflake size uniformity `FSU`, falling angle `A` and speed `S` to an image. One to three layers of snowflakes are added, hence the values should be stochastic. |
| SnowflakesLayer(D, DU, FS, FSU, A, S, BSF, BSL) | Adds a single layer of snowflakes to an image. See augmenter `Snowflakes`. `BSF` and `BSL` control a gaussian blur applied to the snowflakes. |
