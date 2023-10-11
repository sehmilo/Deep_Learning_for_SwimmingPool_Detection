# Deep_Learning_for_SwimmingPool_Detection

## Introduction
Deep learning is a type of machine learning. It relies on multiple layers of nonlinear processing for feature identification and pattern recognition. ArcGIS uses deep learning frameworks to accomplish various deep learning analyses, including object detection. Object detection involves locating specific features within an image. Training a model to detect one object, or multiple objects, saves the time and expense of digitizing and collecting data. It also allows you to expand your analysis by using the model with different datasets and in different locations.

## Scenario
Tax assessors at local government agencies often rely on surveys to estimate property value and calculate property taxes. These surveys are infrequent, which means that there can be some inaccuracy in the assessment records. Swimming pools are an important part of these assessments because they impact the value of a property. You will use ArcGIS deep learning tools to detect all swimming pools in a defined area. Tax assessors can use this information to identify newly constructed pools that were not recorded in the assessment records. This information will help tax assessors identify more appropriate property values and taxes, which can lead to additional revenue for the community.

## Data Description
ArcGIS Pro package and data files for section 5 exercises in the Spatial Data Science: The New Frontier in Analytics MOOC. This data was derived from NAIP imagery provided by the US Department of Agriculture and fictitious data created by Esri. The data and related materials are made available through Esri (https://www.esri.com) and are intended for educational purposes only (see Terms of Use).
link to ddownload data https://www.arcgis.com/home/item.html?id=f283da2e3fd04ef68ebe43ed08646a7c&rsource=https%3A%2F%2Flinks.esri.com%2FSection05%2FData

## Terms of Use
None, USDA data and NAIP Imagery are licensed as public domain.

Use of this Data is restricted to training, demonstration, and educational purposes only. This Data cannot be sold or used for marketing without the express written consent of Environmental Systems Research Institute Inc.THE DATA AND RELATED MATERIALS MAY CONTAIN SOME NONCONFORMITIES, DEFECTS, OR ERRORS. ESRI DOES NOT WARRANT THAT THE DATA WILL MEET USER'S NEEDS OR EXPECTATIONS; THAT THE USE OF THE DATA WILL BE UNINTERRUPTED; OR THAT ALL NONCONFORMITIES, DEFECTS, OR ERRORS CAN OR WILL BE CORRECTED. ESRI IS NOT INVITING RELIANCE ON THIS DATA, AND THE USER SHOULD ALWAYS VERIFY ACTUAL DATA.THE DATA AND RELATED MATERIALS ARE PROVIDED "AS-IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.IN NO EVENT SHALL ESRI AND/OR ITS LICENSOR(S) BE LIABLE FOR COSTS OF PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOST PROFITS, LOST SALES, OR BUSINESS EXPENDITURES, INVESTMENTS, OR COMMITMENTS IN CONNECTION WITH ANY BUSINESS; LOSS OF ANY GOODWILL; OR FOR ANY INDIRECT, SPECIAL, INCIDENTAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES ARISING OUT OF THIS AGREEMENT OR USE OF THE DATA AND RELATED MATERIALS, HOWEVER CAUSED, ON ANY THEORY OF LIABILITY, AND WHETHER OR NOT ESRI OR ITS LICENSOR(S) HAVE BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGE. THESE LIMITATIONS SHALL APPLY NOTWITHSTANDING ANY FAILURE OF ESSENTIAL PURPOSE OF ANY EXCLUSIVE REMEDY.In the event that the data vendor(s) has (have) granted the end user permission to redistribute the Geodata, please use proper proprietary or copyright attribution for the various data vendor(s), and provide the associated metadata file(s) with the Geodata.

## Data Contact
GISTraining@esri.com

## Tags
SpatialDataScience, Esri Training Services, California, Object detection

## Credits (Attribution)
US Department of Agriculture, Esri Training Services - for educational purposes only.

## Create Training Samples
The first step in object detection is to prepare training data that will be used to train the model. There are various ways to prepare training samples:

Use ArcGIS Pro editing tools.
Use the Label Objects For Deep Learning tool.
Use crowdsourced data (for example, community-based damage assessments).
Use preexisting data as training samples (for example, a feature class of building footprints).
In this step, you will prepare training samples by using the Label Objects For Deep Learning tool.

In the Contents pane, select NAIP_AOI.tif.

From the Imagery tab, in the Image Classification group, click Classification Tools and choose Label Objects For Deep Learning.

View result Opens in new window
The Image Classification pane provides tools for you to trace, or digitize, the features that you will use as your training samples.

In the Image Classification pane, if necessary, click the Polygon tool Polygon.

From the Map tab, zoom to the Pool 1 bookmark.

Hint
On the map, click the four corners of the pool to create a rectangular outline, and then double-click the last point of the rectangular outline to finish your polygon.

View result Opens in new window
The Define Class dialog box appears. It allows you to define the class and value of the feature. Each class represents an object that you want to detect. If you wanted to detect pools and tennis courts, you would create two classes with training samples for each class.

In the Define Class dialog box, for Name, type Pool.

For Value, type 0.

Note: All training samples must be labeled with a class value.

Click OK.

Note: To delete a polygon that you created, select the polygon in the Image Classification pane under Labeled Objects, and then click the Delete button Delete button.

Zoom to the Pool 2 bookmark.

Use the Polygon tool to outline the pool.

View result Opens in new window
Note: The color and pixel percentage of your Pool polygons may differ.

In the Image Classification pane, under Labeled Objects, the next pool is automatically added and labeled as Pool.

After creating your training samples, you would use the Image Classification pane's Export Training Data tab to export these training samples into a format that you can use to train your model. Because the creation of training samples can be a time-consuming process, you will proceed with a layer of pre-created training samples.

Close the Image Classification pane.

In the Label Objects warning window, click No

## Review Training Samples
To save time, you will use preexisting data as training samples. You can use preexisting point, line, polygon, or even raster data for your training samples. In the previous step, you created polygons to represent the training samples (pools). In this step, you will use preexisting point data to represent the training samples (pools).

All training sample data must have a class value that distinguishes the types, or classes, of objects to detect. In this step, you will confirm that the pre-created point data includes this class value.

In the Catalog pane, expand Databases, and then expand ObjectDetection.gdb.

Right-click TrainingSamplesComplete and choose Add To Current Map.

In the Contents pane, right-click TrainingSamplesComplete and choose Zoom To Layer.

View result Opens in new window
Note: The points on your map may be a different color. If necessary, you can change the symbology color of the points.

This training samples data uses points to represent swimming pools.

Right-click TrainingSamplesComplete and choose Attribute Table.

View result Opens in new window
This analysis will detect one class: pools. As such, there is only one class value: 0.

Close the attribute table.

## Export training samples
In this step, you will export the pre-created training samples into image chips.

![image](https://github.com/sehmilo/Deep_Learning_for_SwimmingPool_Detection/assets/48839121/5cb56cdd-d15a-4543-909a-be2a15cbe38c)

False-color image with a pool in the image

Image chips use the training sample locations to cut, or chip, the source imagery into defined sub-images that will contain a training sample. These image chips will be used to train the object detection deep learning model.

In the Geoprocessing pane, search for and open the Export Training Data For Deep Learning (Image Analyst Tools) tool.

Hint
You will use this tool to define the properties of the image chips.

Complete the tool by setting the following parameters:

Input Raster: NAIP_AOI.tif
Output Folder: ImageChips
Input Feature Class Or Classified Raster Or Table: TrainingSamplesComplete
Class Value Field: ClassValue
Buffer Radius: 6
For Buffer Radius, point to the parameter name and pause over the geoprocessing input information icon Information button.

The geoprocessing input information icon Information button provides an explanation of how the parameter is used in the tool. Because you are using point data, you can use this parameter to add a buffer around each point, creating circular polygon training samples that will better represent the shapes of the pools. The spatial reference of the input feature class (TrainingSamplesComplete) uses meters as its linear unit. Therefore, a Buffer Radius value of six meters will be appropriate for capturing the images of residential swimming pools. 

For Input Mask Polygons, leave this parameter empty.

This parameter delineates the area where image chips will be created. You want to create image chips for all training samples, so you will leave this parameter empty.

For Image Format, leave the default.

The image format that you choose will depend on the number of bands of your source imagery file.

For Tile Size X and Tile Size Y, leave the defaults.

The tile sizes are the dimensions of the image chip size in X and Y. The unit of measurement is in pixels. Larger tile sizes will require more processing time and power.

For Stride X and Stride Y, leave the defaults.

The stride setting determines how much overlap there will be in each image chip. With a tile size of 256 and a stride of 128, half of the first image chip will overlap with the next image chip. That is useful when you have a small training sample size and want to increase the training sample size.

For Rotation Angle, leave the default.

Rotation can be used to create additional image chips. The original chip is rotated by a specified angle to create additional chips at additional angles. This process can help augment the data.

Note: There is no universally correct tile size, stride, and rotation angle. These values will vary based on your analysis, source imagery, and computing power. The default values provide a baseline, but it is recommended that you try several variations to determine whether your model results improve.

For Reference System, leave the default.

This parameter indicates the reference system that is used to interpret the input image. Because this image is pre-processed orthoimagery, it should be processed using Map Space.

For Output No Feature Tiles, leave the default.

This parameter allows you to include image chips that do not have any training samples. In this analysis, it would create image chips with no pools. These chips can provide more context to the model, identifying objects that may look like a pool but are not. Including false positives like these can potentially improve model results, but it includes additional image chips to process.

For Metadata Format, verify that PASCAL Visual Object Classes is selected.

This parameter defines the format for the image chip labels. The PASCAL Visual Object Classes format is a standardized image dataset format for object class detection.

For Minimum Polygon Overlap Ratio, leave the default.

This parameter sets the minimum overlap percentage for a feature to be included in the training data. The percentage value is expressed as a decimal for this parameter. The default value is 0, which means that all features will be included.

View result Opens in new window
Click Run.

A message appears at the bottom of the Geoprocessing pane to confirm that the tool is complete.

## Review image chips
After the Export Training Data For Deep Learning tool is complete, you can review the image chips from the specified folder location.

Open File Explorer.

Browse to ..\EsriTraining\ObjectDetection\ImageChips.

View result Opens in new window
The tool creates a folder for the image chips that includes the images, label definitions for the images, image statistics, and a model definition file. The model definition file references this image chip information. You will use the model definition file to train the model.

Double-click the Images folder.

Open one of the TIF files.

View result Opens in new window
This image chip is an example of one of the image chips that will be used to train the model to detect swimming pools in the defined area.

Close the image and File Explorer.

Return to ArcGIS Pro and save the project.

If you are continuing to the next exercise, leave ArcGIS Pro open; otherwise, exit ArcGIS Pro.

## Train the model using geopreocessing tool
Next, you will train the model by using the Train Deep Learning Model geoprocessing tool in ArcGIS Pro.

Note: It can take up to four hours to train this model, depending on your computer's processing power. You have been provided the trained model file for this exercise, so you will not run the model.

If necessary, start ArcGIS Pro and sign in with your course credentials.

Open the ObjectDetection.aprx project. 

Hint
In the Geoprocessing pane, search for and open the Train Deep Learning Model (Image Analyst Tools) tool.

For Input Training Data, browse to and select your C:\EsriTraining\ObjectDetection\ImageChips folder.

For Output Model, type PoolsModel_25_SSD.

For Max Epochs, type 25.

The number of epochs defines the number of times that the neural network will process the image chips. The default number of 20 is a baseline that you can adjust based on the results of your model.

Expand Model Parameters.

For Model Type, choose Single Shot Detector (Object Detection).

The model type will determine the deep learning algorithm and neural network that you will use to train your model. The models that are available to you depend on the metadata format that is chosen for the image chips. You chose a metadata format that is associated with object detection, so only the object detection model types are available. For more information about the other model types, go to ArcGIS Pro Help: Train Deep Learning Model (Image Analyst)Opens in new window.

Leave the defaults for the remaining parameters.

View result Opens in new window
Model arguments refer to specific parameter values that are used to train the model. The model arguments will vary based on the model type that you choose. For the Single Shot Detector (Object Detection) model type, you can specify the grid cell size, zoom level, and aspect ratio. These values define how the model examines the image to detect objects. For more information about the Single Shot Detector model, go to ArcGIS API for Python Help: How single-shot detector (SSD) works.Opens in new window

To learn more about the individual model parameters, point to Model Arguments and pause on the geoprocessing input information icon Geoprocessing input information.

Expand Advanced.

Leave the default settings for all fields.

The following graphic is used to explain one of the advanced parameters.

![image](https://github.com/sehmilo/Deep_Learning_for_SwimmingPool_Detection/assets/48839121/d9e1bbf1-776f-4995-867b-ee99b5b1a875)


Graph with learning rate on the x-axis and loss on the y-axis
In this example, the loss (or model error) decreases as the learning rate is increased from 1e-7 to 1e-1. After this point, the loss begins to increase again. The part of the graph between 1e-3 and 1e-1 shows a steeper loss curve and you can choose a learning rate in this range to train the model. By default, the tool chooses a conservative (lower) learning rate (close to 1e-3) to ensure that it does not overshoot the minimum error loss function. However, for faster training, you may pick a higher learning rate (up to 1e-1).

The learning rate controls the weighting adjustment of the neural network. A low learning rate trains the model slowly, while a high learning rate can jump to conclusions and learn the incorrect information. You can specify a learning rate or leave the default. The default will choose the rate in which loss, or model error, is lowest before it starts to increase again, indicating that the learning rate is too high and is introducing error into the model.

To learn more about the other advanced parameters, point to the geoprocessing input information icons Geoprocessing input information.

Note: It can take up to four hours to train this model, depending on your computer's processing power. You have been provided the trained model file for this exercise, so you will not run the model.

After reviewing the parameters, continue to the next step.

## Review the Model 
The Train Deep Learning Model (Image Analyst Tools) tool trains a deep learning model and updates the model definition file (.emd) with this information. You can use this model definition file to detect, or infer, the locations of the remaining swimming pools. By reviewing the results, you can assess the model accuracy to determine whether you should modify the model or proceed with your analysis.

In the remaining exercise steps, you will use the trained model file that was provided for you.

Open File Explorer and browse to ..\EsriTraining\ObjectDetection\Results\PoolsModel_25_SSD.

Double-click the model_metrics.html file.

View result Opens in new window
A web browser opens with model metrics that describe the following information:

Learning rate controls the speed at which the model is trained, which shows how quickly the model parameters are updated. In this graphic, the learning rate shows a range of values, where the smaller number on the left is the learning rate applied to the first few layers of the network, and the larger number on the right is applied to the last few layers. The low learning rate trains the first few layers of the network slowly while the higher learning rate trains the final layers of the network more quickly. The end goal is to identify your optimal learning rate. That can be done by finding the highest learning rate where the loss is still improving; since loss is an indicator of error, a smaller number is more ideal.
The training and validation loss graph compares training and validation losses over the training epochs. A model that performs well typically shows a continual decrease in both training and validation loss over the training epochs. If the validation loss begins to increase, then you may have overfitting, where the model is recognizing a particular set of data too closely and therefore may not generalize well to other data.
Average precision score assesses the performance of object detection models. It measures the average precision for the validation set for each class. An average precision score ranges from 0 to 1, where values closer to 1 indicate better model performance.
Scroll down to Ground Truth/Predictions.

View result Opens in new window
Comparing the ground truth images with the predicted images will also help you determine the accuracy of your model. This model provides a good baseline, predicting most of the pools identified in the ground truth image.

These metrics can help you determine whether you should modify the parameters of this tool (learning rate, number of epochs, grid cell size, and so on) to improve the results of the models. Because modifications would require more processing time, you will proceed with this model.

Close the results and File Explorer, and then return to ArcGIS Pro.

-Step 4: Perform inferencing using the model
After you train the model, you will perform inferencing. Inferencing uses the trained model to extract information from your imagery. In this case, you will extract, or detect, swimming pools for the specified area of interest.

In the Geoprocessing pane, click the Back button Back button.

Search for and open the Detect Objects Using Deep Learning (Image Analyst Tools) tool.

Set the following tool parameters:

For Input Raster, choose NAIP_AOI.tif.
For Output Detected Objects, type SwimmingPoolsAll.
For Model Definition, browse to ..\EsriTraining\ObjectDetection\Results\PoolsModel_25_SSD and select PoolsModel_25_SSD.emd.
You will see some items listed in the Arguments section. These arguments will be used on your image as it passes through the layers of the model. The default arguments use the values that were defined when training the model. You can use these values as a baseline that can be adjusted to refine the inferencing results. The following information provides explanations of each argument.

Padding adds a border of cells around the image. This border is used to ensure that the image maintains its original size as it passes through the model. Padding is most relevant if you are detecting objects that are around the edge of your image.
Grid of cells with the perimeter of the cells grayed out

![image](https://github.com/sehmilo/Deep_Learning_for_SwimmingPool_Detection/assets/48839121/1c940e0a-f5ed-49b2-ac96-69184b7502b5)

The padding in this image is 2 pixels in size, indicated in gray.

Threshold defines the required confidence level for object detection. In this analysis, the threshold is 0.5, meaning that the model has to be at least 50 percent confident that the object is a swimming pool.
NMS_Overlap is the percentage of allowable overlap between features. In this analysis, features that overlap more than 10 percent will be removed.
Batch_Size should be a square number, such as 1, 4, 9, 16, and so on. If the input value is not a perfect square, the analysis will use the largest perfect square that is less than the input. Increasing the batch size can improve tool performance. However, as the batch size increases, more memory is used.
Exclude_Pad_Detections allows you to exclude items in the padded areas. In this analysis, you will exclude the padded areas from inferencing.
Check the Non Maximum Suppression box.

Non Maximum Suppression will identify duplicate features. The feature with the lower confidence level will be removed. The default values for this parameter will use the confidence field to determine which feature has a lower confidence level. Max Overlap Ratio will define how much overlap between features is allowable. The default does not allow any overlap.

On the ribbon, from the Map tab, zoom to the Inference Pools bookmark.

View result Opens in new window
Inferencing can be a time-consuming process based on your computer's processing power and the scale of your analysis. To minimize processing time, you will analyze a smaller area of interest.

At the top of the Geoprocessing pane, click the Environments tab.

Under Processing Extent, update Extent to Current Display Extent.

View result Opens in new window
Coordinates are defined based on the current extent of the map. These coordinates will be used as the processing extent for this tool.

Click Run.

Note: It may take several minutes for the tool to finish running.

View result Opens in new window
The model detected swimming pools for the specified area and created a new feature layer with the results.

-Step 5: Review inferencing results
The swimming pools that the model detected cannot be seen at the current scale. In this step, you will zoom in to the map to review the inferencing results and assess their accuracy.

In the Contents pane, click the SwimmingPoolsAll symbol.

In the Symbology pane, click the Gallery tab.

Under ArcGIS 2D, click Black Outline (2 Pts).

From the Map tab, in the Selection group, click Attributes.

View result Opens in new window
The Attributes pane opens and provides attribute information for features in a selected area. You can also use this pane to zoom to each of the features and determine whether the model detected the appropriate object.

In the Attributes pane, click the Layers tab.

From the Choose A Layer drop-down list, choose SwimmingPoolsAll.

Under SwimmingPoolsAll, click the Step Forward button Step Forward.

View result Opens in new window
The map moves to a detected pool in the SwimmingPoolsAll layer. You can use this tool to review the detected pools, visually assessing the accuracy of the model results. Based on the accuracy of the model results, you would modify the model or continue running inferencing on the entire study area.

Using this model, you can quickly detect the remaining swimming pools in Southern California, providing tax assessors with the information that they need to identify more accurate property values and taxes.

Save the project.

If you would like to train the model using ArcGIS API for Python, proceed to the optional stretch goal; otherwise, save your project and exit ArcGIS Pro.

Esri Academy course: Deep Learning Using ArcGIS ProOpens in new window

-Step 6: Stretch goal (Optional)
Previously, you trained the model by using the Train Deep Learning Model geoprocessing tool. In this stretch goal, you will train the model by using ArcGIS API for Python in a Jupyter Notebook.

The contents of the notebook that you will run describe the process of training a deep learning model with ArcGIS API for Python. It includes the ArcGIS API code and descriptions of each step in the process.

Note: If you run the ssd.fit() cell, it will begin to train the model. It can take up to four hours to train this model, depending on your computer's processing power. Other cells in the notebook may take a few minutes to run as well.

Use the following high-level steps to complete the stretch goal.

From the Windows taskbar, search for and open Python Command Prompt.
In the Python Command Prompt window, type cd, add a space, and then add the file path where you saved the ObjectDetection project. (The code with the file path may look like the following: cd C:\EsriTraining\ObjectDetection.)
Press Enter.
In the Python Command Prompt window, type jupyter-notebook and press Enter.
In the web browser that opens, from the Files tab, click model_training.ipynb.
Click Run Run button to run through each cell in the script.
When you are finished, close the web browser and the Python Command Prompt window.

Save your project and exit ArcGIS Pro.

