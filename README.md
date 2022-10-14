# Document Scanning with Image Preservation and OCR

## Problem Statement
The goal of this project is to create a document scanner that will scan a page that consists of text and images. The document scanner output will preserve the image and perform OCR. 

## Approach
Edge detection & corner detection will be used to find the document within the image. Then using points along the edge we will apply a 2D homography to unwarp the document. We will then crop the image to contain only the document. Next we will perform text and image detection to segment the document. We will then perform image processing on any detected images to improve their appearance. We will then perform thresholding to make the page background pure white and the text pure black. We will then perform OCR to provide a transcript of the text. We will then upscale the image and provide the final document as a PNG and a PDF. 

## Experiments and Results
We will use the Standard OCR dataset from [Kaggle](https://www.kaggle.com/datasets/preatcher/standard-ocr-dataset) to train our OCR machine learning algorithm. We will implement the training model for the OCR database. We will be using Python libraries, such as Numpy, Pandas, ImageParser, cv2, and scikit, but we plan to write our own code that leverages these Python libraries. To verify the success of our project we would compare the results of our project to other applications such as CamScanner or Tiny Scanner. We would cross reference the outputs and see if our project output is close to the other applications. We could compare the different aspects of the image such as the image or text in both outputs to see where our project falls short or succeeds. 

## Provide a list of experiments that you will perform
To test this project we can test a selection or combinations of different conditions including:
- shadows
- angle
- height
- busy background
- low or high light conditions
- proper document selection within a group pages
- pixel warping
We expect that some of the listed experiments above will lead to bad output that may not be readable for the user. This could result in offset angled documents or sections of the document being unreadable due to shadows or light conditions. Some uncertain outcomes may be what happens with pixel warping or busy background as if we have a solid image detection algorithm these experiments would still yield a successful output. 
