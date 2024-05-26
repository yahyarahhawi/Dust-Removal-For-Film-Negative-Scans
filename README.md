# Dust-Removal-For-Film-Negative-Scans

This project is an interactive tool for removing dust from images , especially scans of negative film, and previewing the results using Jupyter Notebook and `ipywidgets`. The tool allows users to adjust various parameters to fine-tune the dust removal process and visually inspect the results in real-time. The segmentation of dust utilizes Difference of Gaussian and thresholding to extract dust and remove it effectively while maintaining details across the image



## Authors

- [@yahyarahhawi](https://www.github.com/yahyarahhawi)



### Prerequisites

- Python 3.6 or later
- Jupyter Notebook or JupyterLab
- Required Python packages:
  - `numpy`
  - `matplotlib`
  - `ipywidgets`
  - `skimage`


## Intoduction
As a passionate film photographer and a special collections associate/student archivist at Middlebury College, I scan hundreds of film negatives weekly. A common issue with scanning film negatives using flatbed scanners is the presence of dust particles. Despite thorough brushing, these dust particles invariably appear on the scans, varying greatly in size and shape. This requires time-consuming manual inpainting.

To address this, I developed an algorithm to effectively remove dust particles while preserving most image details. Unlike conventional median filters that smooth the entire image, my algorithm applies regional median filters specifically to the segmented dust particles. Using a combination of difference of Gaussian and thresholding techniques, the algorithm maintains the image's original sharpness, edges, and details.



## How to use:
- use **height**, **width**, and **size** to determine position and size of the preview window.
- Use **Sigma_min** to pick the largest sigma that makes the smallest dust particles in the previw window disappear. Similarly, pick the smallest **Sigma_max** that makes the largest dust particles disappear
- Pick the **intensity** of the median filter. Start big, and then reduce to smallest nubmer before dust particles appear again.
- Pick the largest **Threshold** that still removes the dust particles.
- finally, when satisified with the result, click **save** to save the image

## Demo

![demo dust](https://github.com/yahyarahhawi/Dust-Removal-For-Film-Negative-Scans/assets/170378585/3d323d37-5c1a-4065-9ab2-2dc3a575bd80)



## Methods
### Difference of Gaussian (DoG)
The Difference of Gaussian (DoG) is an image processing technique used to detect edges and shapes of different sizes. Here’s a quick summary:

**Gaussian Blur:** Apply Gaussian blurring to the image twice using two different standard deviations (sigma values), resulting in two blurred images.

**Subtract Blurred Images:** Subtract the second blurred image from the first. This operation highlights regions of the image where there are significant intensity changes, effectively detecting edges.

**Thresholding:** Apply a threshold to the resulting image to emphasize significant edges and reduce noise.

By using two different sigma values, the DoG technique is capable of detecting shapes and features of various sizes. Smaller sigma values highlight finer details, while larger sigma values capture broader structures. This makes DoG particularly effective for identifying edges and shapes across a range of scales within the image.


### Thresholding
Most dust particles are bright artifacts that spread across the image. A good approach to segmenting them is to threshold the image at a given value immediatly below the value of these dust particles.

### Combining both
Having two masks from DoG and thresholding, we combine them together using an AND operation. which results in a segmentation map that captures most dust particles and does not include unwanted regions from original image.
## Results
Here is a before-and-after of the algorithm applied to an example image:

![results](https://github.com/yahyarahhawi/Dust-Removal-For-Film-Negative-Scans/assets/170378585/2af3f2a7-ae10-4988-b521-7558f77c7556)


## Issues

### False Positives in Dust Detection
The algorithm may sometimes incorrectly identify non-dust features as dust particles, especially if they have similar intensity and size characteristics. This can lead to undesired alterations in the image.

### Limited Dust Particle Types
The algorithm is optimized for specific types of dust particles. Unusual shapes or very small dust particles might not be detected or removed effectively.

### Performance on High-Resolution Images
Processing very high-resolution images can be computationally intensive and slow, especially with larger window sizes and higher intensities.

### Dependency on Parameter Tuning
The effectiveness of dust removal heavily relies on proper parameter tuning (e.g., intensity, sigma values, threshold). Users may need to experiment with different settings to achieve optimal results, which can be time-consuming.

### Color Images
The current implementation assumes grayscale images. Additional work is required to extend the algorithm to handle color images effectively.
## Improvements
Future improvements include:
1. Compatability with color images
2. auto mode that optimizes the various parameters
3. Making it more accessible by launching an excutable instead of having to run it inside of jupyter notebook
4. better navigation for previewing
5. additional preview windows for segmentation masks
## Libraries Used
 - This project was developed with the help of **ipywidgets** for creating interactive widgets and **matplotlib** for plotting.
- **skimage** library was also used for image processing functionalities.

