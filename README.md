# Document Scanning with Image Preservation

## Abstract

The goal of this project is to create a document scanner that will scan a page that consists of text and images. The
document scanner will align the document to fully fit the output as well as setting the text sections to white and black
while preserving the image color. The group accomplished this by detecting the edges of the document, performing a
homography to fill the output and detect the image to preserve it. The group was able to obtain results that look mostly
like a document scanner phone application.

## Teaser Image

<p float="left">
  <img src="Images/Qualitative_Results/input_text_color_im.png" width="49%" />
  <img src="Images/Qualitative_Results/output_text_color_im.png" width="49%" />
</p>

## Introduction

The motivation behind this project was to be able to scan a document that was not aligned with the corners of the image
and return an image that would now “fit” the image. The program would also be able to detect images to preserve the
color as the rest of the document would be set to black and white to improve the text readability. The application of
this program would be scanning and uploading physically received documents that have black text and images that are
colored or not colored. The use of document scanning is quite popular especially in academia or saving information
received through the mail such as tax information. The goal is to be able to have the document available as a digital
version that is not just simply a misaligned picture of the document which allows the user to discard the original
document.

## Approach

The approach the group followed consisted of edge and line detection, homography, image detection and setting text
sections to black and white. The first step for the document scanning was to get the four edges of the document and the
four corners. To do this the group used the Canny edge detection for edges and the Harris corner detector for corners
from OpenCV. Once the edges and lines were found we then applied a homography of the detected document into a new image
which would result in the document filling the output image. Once the document filled the entire space the group used
the layout parser functions to detect the regions where images were present. The layout parser function using one of the
built-in algorithms as a parameter was able to detect images with over an 80 percent confidence and return the rough
location of where the image was. With the locations of the images we could make sure they would not be affected when
setting the rest of the document to black and white. The last step was to combine the document with the preserved images
and the black and white text and return it as the output.

There were quite a bit of difficulties when working on the edge and line detection as the functions used from OpenCV
would return every edge and every corner. In order to solve this problem we selected the four longest edges that are
returned by drawing lines between each corner and removing all lines that intersect with another line. This works for
most cases but will fail if there is an image or line in the document that is longer than one of the edges. Another
issue was that the homography was not perfect and would have slight gaps on the edges. We were not able to get this to
work perfectly, but we tried our best to get it as close as possible. The last issue the group faced was with the layout
parser function not perfectly finding the image. For some reason it always seemed to be slightly shifted over where part
of the image was outside the region. We experimented with other line parser algorithms, but we were not able to get a
perfect result.

### Steps Visualization

<details>
<summary>Click To Expand</summary>

<p float="left">
  <img src="Images/Qualitative_Results/input_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/All_Edges_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Prominent_Edges_Mask_text_gray_ims.png" width="32%" />
</p>

<p float="left">
  <img src="Images/All_Steps/Prominent_Edges_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/All_Corner_Clusters__Enlarged_for_Viewing_Purposes__text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Prominent_Corner_Clusters_Mask_text_gray_ims.png" width="32%" />
</p>

<p float="left">
  <img src="Images/All_Steps/Prominent_Corner_Clusters__Enlarged_for_Viewing_Purposes__text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Prominent_Selected_Corners_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Segments_Connecting_All_Corners_text_gray_ims.png" width="32%" />
</p>

<p float="left">
  <img src="Images/All_Steps/Detected_Intersections_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Intersecting_Edges_Removed_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Four_Longest_Edges_text_gray_ims.png" width="32%" />
</p>

<p float="left">
  <img src="Images/All_Steps/Corresponding_Points_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Unwarped_Image_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Detected_Regions_text_gray_ims.png" width="32%" />
</p>

<p float="left">
  <img src="Images/All_Steps/Images_Mask_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Document_Images_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Non-Images_Mask_text_gray_ims.png" width="32%" />
</p>

<p float="left">
  <img src="Images/All_Steps/Document_Non-Images_text_gray_ims.png" width="32%" />
  <img src="Images/All_Steps/Black___White_Document_Non-Images_text_gray_ims.png" width="32%" />
  <img src="Images/Qualitative_Results/output_text_gray_ims.png" width="32%" />
</p>

</details>

## Experiments and Results

To verify that the program was working correctly the group used a couple of test documents with different backgrounds
and elements. These documents are a collection of class handouts as well as test documents we created. The group
selected certain documents with the goal to see if the program would break such as documents with multiple images or
documents with a table. The documents tested range from just text, just images, a combination of text and images, and
tables. We also changed the way the images were taken and which way the document was angled.

### Verification

Since this was a visual project the verification was done by seeing how the output looks. We displayed the edge lines as
well as the corners detected on the image to show that the first steps are working.

<p float="left">
  <img src="Images/Qualitative_Results/input_text_color_im.png" width="49%" />
  <img src="Images/Verification/1/Prominent_Edges_text_color_im.png" width="49%" />
  <img src="Images/Verification/1/Prominent_Selected_Corners_text_color_im.png" width="49%" />
  <img src="Images/Verification/1/Four_Longest_Edges_text_color_im.png" width="49%" />
</p>

Then we displayed the homography input and output points.

<p float="left">
  <img src="Images/Verification/1/Corresponding_Points_text_color_im.png" width="49%" />
  <img src="Images/Verification/1/Unwarped_Image_Prominent_Edges_text_color_im.png" width="49%" />
</p>

After the document was the main focus we ran the image parser which will outline the image as well as the text blocks.

<p float="left">
  <img src="Images/Verification/1/Detected_Regions_text_color_im.png" width="49%" />
</p>

After we found the image we showed that the program can pull out the image and make the text black and white.

<p float="left">
  <img src="Images/Verification/1/Document_Images_text_color_im.png" width="49%" />
  <img src="Images/Verification/1/Black___White_Document_Non-Images_text_color_im.png" width="49%" />
</p>

Then finally we display the last output with the image and the text combined.

<p float="left">
  <img src="Images/Qualitative_Results/output_text_color_im.png" width="49%" />
</p>

With this we can show how we verified the steps to get to a successful output.

### Testing different inputs

#### Document with 4 pictures

With this input you can see how the program will at first detect too many points but our algorithm which is described
above will first remove all lines that have an intersection then just take the four longest lines.

*Add images here*

#### Landscape document with tables

With this document we are testing a landscape portrait document with tables. We used this to test our program since we
wanted to see what would happen with the line and corner detection. With this input we can see that each table was not
detected as lines and corners but there were some random corner points detected. You can see like the example above the
algorithm was successfully able to get rid of the lines that have an intersection and just leave the document edge
lines.

*Add images here*

#### Failure with background

In this input there are two main failures, a point detected outside the image and the image detection messing up the
final output. As you can see above the point detected in the logo on the table makes the final outline not be around the
image but connect to the logo. This will cause the homography to be less than perfect. The second issue is the image
detection. Since the entire document is an image the image detection does not work as intended, and thus leads to a poor
result.

*Add images here*

### Parameters

While coding the project the group did have some parameters that were used. These parameters mostly were used for the
edge detection and corner detection functions we used from OpenCV. We used the recommended values that were given in the
example code and tuned it slightly to work best for our project.

## Qualitative Results

### Document with Just Text

<p float="left">
  <img src="Images/Qualitative_Results/input_text_doc.png" width="49%" />
  <img src="Images/Qualitative_Results/output_text_doc.png" width="49%" />
</p>

### Document with Color Image

<p float="left">
  <img src="Images/Qualitative_Results/input_text_color_im.png" width="49%" />
  <img src="Images/Qualitative_Results/output_text_color_im.png" width="49%" />
</p>

### Document with Multiple Gray Images

<p float="left">
  <img src="Images/Qualitative_Results/input_text_gray_ims.png" width="49%" />
  <img src="Images/Qualitative_Results/output_text_gray_ims.png" width="49%" />
</p>

### Document with Multiple Color Images

<p float="left">
  <img src="Images/Qualitative_Results/input_color_ims.png" width="49%" />
  <img src="Images/Qualitative_Results/output_color_ims.png" width="49%" />
</p>

### Document with Table

<p float="left">
  <img src="Images/Qualitative_Results/input_landscape_tables.png" width="49%" />
  <img src="Images/Qualitative_Results/output_landscape_tables.png" width="49%" />
</p>

### Failure with Corner Detection

<p float="left">
  <img src="Images/Qualitative_Results/input_bad_corner_detect.png" width="49%" />
  <img src="Images/Qualitative_Results/output_bad_corner_detect.png" width="49%" />
</p>

### Failure with Image Detection

<p float="left">
  <img src="Images/Qualitative_Results/input_bad_im_detect.png" width="49%" />
  <img src="Images/Qualitative_Results/output_bad_im_detect.png" width="49%" />
</p>

### Failure with Image Detection 2

<p float="left">
  <img src="Images/Qualitative_Results/input_bad_im_detect2.png" width="49%" />
  <img src="Images/Qualitative_Results/output_bad_im_detect2.png" width="49%" />
</p>

## Conclusion

This report has shown how the group has created a successful document scanner program by giving an overview of the
approach used, the experiments and verification steps, and showing off some successful examples. Although the project
works for most of the test cases we used there are some areas for improvement. These areas of improvement consist of
having more accurate homography, and removing errors when having a busy background. One way the group thought this could
be done is using a machine learning algorithm to optimize the parameters used during edge detection. Overall the group
feels that they have delivered a successful project that can take most documents and output a document that is similar
to what you would expect from a document scanner application.

## References

- [https://stackoverflow.com/a/62856504](https://stackoverflow.com/a/62856504)
- [https://www.tutorialkart.com/opencv/python/opencv-python-resize-image/](https://www.tutorialkart.com/opencv/python/opencv-python-resize-image/)
- [https://stackoverflow.com/a/45560545](https://stackoverflow.com/a/45560545)
- [https://homepages.inf.ed.ac.uk/rbf/HIPR2/hough.html](https://homepages.inf.ed.ac.uk/rbf/HIPR2/hough.html)
- [https://docs.opencv.org/3.4/dc/d0d/tutorial_py_features_harris.html](https://docs.opencv.org/3.4/dc/d0d/tutorial_py_features_harris.html)
- [https://scikit-learn.org/stable/modules/clustering.html](https://scikit-learn.org/stable/modules/clustering.html)
- [https://stackoverflow.com/a/3252222](https://stackoverflow.com/a/3252222)
- [https://layout-parser.readthedocs.io/en/latest/notes/modelzoo.html#example-usage](https://layout-parser.readthedocs.io/en/latest/notes/modelzoo.html#example-usage)
- [https://towardsdatascience.com/document-parsing-with-python-ocr-75543448e581](https://towardsdatascience.com/document-parsing-with-python-ocr-75543448e581)
