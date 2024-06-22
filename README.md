# DeepLearningModels

## Overview

This repository contains datasets, tutorials, and scripts for training deep learning models in ArcGIS and YOLOv8.

## Repository Contents

### Information in the Folders:

- **Example_Data_RCNN:** Examples of data used for the Mask R-CNN model.
- **Exemple_Convert_Data_For_YOLO:** Examples of data converted for the YOLOv8 model.

### Tutorial: Dataset Export in ArcGIS

#### Dataset Export

To export datasets and train models within or outside ArcGIS, it's crucial to note that not all datasets are universally available for all models, except those trained within ArcGIS. If possible, perform conversions similar to those done with YOLO v8. Also, verify your license type, as the "Image Analysis" extension is required. This can be confirmed in your ArcGIS licenses, as shown in the following images.

#### Configuration and Required Libraries

For subsequent configurations and the use of tools to train a deep learning model, install the deep learning libraries for ArcGIS. These libraries must be compatible with the version of ArcGIS you are using. In this case, they were installed from the Esri-Frameworks GitHub at [Esri Deep Learning Frameworks](https://github.com/Esri/deep-learning-frameworks?tab=readme-ov-file), which also includes an instruction manual.

#### Label Creation for Dataset Export

To create labels, the "Label Objects for Deep Learning" tool within the Deep Learning section was used.

**How to Use:**
1. Create a class on the raster image you wish to export. In our case, the class was named "pool". Assign a value (1 in our case) and proceed to manually detect all desired pools for export in the dataset. In this instance, we marked approximately 761 pools, resulting in 1,500 .jpeg images.

2. Once pools are labeled, utilize the "Export Training Data for Deep Learning" tool. Configure this tool based on the model in use, as dataset formats vary between different models. Parameters were consistent, except for the raster image (infrared and true color were used) and output format (RCNN and Kitty labels for YOLOv8). Below is an image depicting the configuration for export. Initially, .tiff format was used for testing, but ultimately, .jpeg and desired formats were employed.

#### Dataset Preparation for Training

Post-export, the dataset is ready for training. It resides within the "pools" folder, containing respective images and labels.

#### Training the Deep Learning Model

Proceed to use the "Training Deep Learning Model" tool with necessary configurations. For example, in our case, it was configured as follows:
(Refer to each tool's information to determine the best fit for your model or to add necessary elements in the information box displayed by ArcGIS).

Training took approximately 2 hours, resulting in a deep learning model for object detection. Subsequently, the .dlpk format is essential for model application and ArcGIS readability.

#### Using the Trained Model

Finally, deploy the "Detect Objects Using Deep Learning" tool and apply the trained model to desired validation data.

#### Model Analysis

For deeper analysis, the tool was used with thresholds ranging from 0.1 to 0.9 for both infrared and true color, yielding 20 distinct detection types and configured with CPU. This process took around 5 hours. Consequently, 20 different tables were generated for pool detection analysis per threshold, facilitating identification of the most effective detection. This was achieved using the "Compute Accuracy for Object Detection" tool. Each table logs detected pools against actual pools present, providing insights into the best detection criteria.

### Dataset for YOLOv8

#### Dataset Export and Preparation

Specifically for the YOLOv8 dataset, an additional step was necessary as ArcGIS lacks a format tailored to this model. Thus, export was conducted in Kitty labels format, the closest available. Upon data acquisition, a Python script was used to transform and adapt data specifically for the YOLOv8 model.

#### Preprocessing Script

The preprocessing script, named `preprocess_data.ipynb`, resides in this repository and can be opened using Jupyter Notebook. To utilize it effectively, adjust file paths within the script to match your data locations. This script handles data cleaning and final conversion to ensure readiness for YOLOv8 model usage.

**Steps to Use the Script:**
1. Open the Script: Access `preprocess_data.ipynb` via Jupyter Notebook.
2. Update Directories: Adjust file paths within the script to point to your data locations.
3. Execute the Script: Run notebook cells to perform data cleaning and final conversion.

### Tutorial: YOLOv8

#### Tutorial Reference

For training YOLOv8 on a custom dataset, refer to the tutorial available in the following article: [How to Train YOLOv8 on a Custom Dataset](https://blog.roboflow.com/how-to-train-yolov8-on-a-custom-dataset/).

#### Export and Data Conversion from ArcGIS Pro

As data was exported from ArcGIS Pro, a Python script was enabled, requiring only directory adjustments for data conversion. This script proves especially useful when exporting in Kitty labels, the most similar data format.
