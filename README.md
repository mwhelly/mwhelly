## RETINAL SCANNER: An Eye Disease Image Classifier Project 
### By Mark Whelly 

August 2022

![image](https://user-images.githubusercontent.com/104471340/212449720-33047973-177a-4f26-bded-dd31d15da432.png)


## :ledger:  TABLE OF CONTENTS

- [Introduction](#Introduction)
- [Data Source](#key-Data-Source)
- [Data Exploration & Preprocessing](#bar_chart-Data-Exploration-&-Preprocessing) 
- [Modeling](#chart_with_upwards_trend-Modeling)
- [Conclusions](#high_brightness-Conclusions)

## :earth_africa:  Introduction

Eye disease affects people around the world, resulting in reduced quality of life to individuals, and impacts to local communities and economies due to strains to health care systems and lost productivities.

The World Health Organization (WHO) predicts that eye diseases incidence will continue to increase in coming decades owing to a number of factors including lifestyle (increased screen time usage, more sedentary habits with reduced excercise), diet (higher sugar intakes leading to diabetes, reduced nutrients relating to eye health), and increased demand on systems as populations age and demographics shift to proportionally more senior citizens. WHO recommends the use of deep learning (CNN) to support and complement human health care practitioners by providing rapid and accurate screening capabilities for retinal images. Computer image classifiers could be used to prescreen thousands of images and reduce health care costs, as well as reducing potential burnout of health care staff. 

This project involves developing image classifier models to detect eye disease in people's retinal images, using transfer learning with the Inception V3 convolutional neural network model.

*A total of 4 CNN models were developed and optimized progressively in this project:*

MODEL 1 - general disease detection (all 45 diseases, classifying outcomes as diseased or healthy)

MODEL 2 - single disease detection model, optimized for Diabetic Retinopathy (related to diabetes)

MODEL 3 - single disease detection model, optimized for Macular Degeneration

MODEL 4 - Multiclass model designed to identify if 1 of 3 diseases were present in images. Diseases include myopia, BRVO related to blood clots and strokes, and macular hazing (glaucoma).

A total of 3200 colour images were available. The data set was presplit 60:20:20 (Train/Validation/Test groups), and approximately 20% of all images were healthy, in each of the 3 groups.

The data was imported to my Google Drive from the kaggle website, and then modeling was performed within the Google Colab Environment.

## :key:  Data Source

The data was obtained from the dataset 'Retinal Disease Classification' on kaggle.com, authored by Larxel. 
Original data was obtained from the journal Data volume 6(14), by Pachade et al. 2021.


## :bar_chart: Data Exploration & Preprocessing

### Data Exploration

The 3200 colour images from the kaggle data set were already grouped into 3 folders (Train, Validation, Test groups, with subfolders 'normal' and 'abnormal' within each of the 3 groups).
There were 2560 disease images and 640 healthy images, therefore it was an imbalanced dataset for Model 1 and data augmentation was used to increase the number of healthy images to be similar to disease image datasets.
NOTE: Initial modeling of the dataset was done (not shown), and then images were pre-processed and results were greatly improved (recall, precision, accuracy). Therefore, only the Model 1 results with pre-processed images are presented within the MODEL 1 notebook.

Initial examination of the number of images per disease type was examined, to identify the most predominant diseases. Correlation of diseases was also carried out. These findings shaped the development of the 5 models in this project.


### Data Preprocessing
Images were copied within Google Drive, and separated into folders, to retain a copy of original images. The copies were transformed using contrast histogram equalization (EQH). A number of transformations were tried out, and this (EQH) appeared to provide the best visual improvement across a wide number of images based on random testing and visual observations prior to modeling.

Below are two images with the original on left and the EQH transformed versions on the right. The CNN model is dependent on being to able to detect patterns in images that are related to eye disease. Therefore, increasing the contrast of images to allow better resolution of details such as spots or changes in veins, would be expected to improve the likelihood of correct detection of eye condition.

![image](https://user-images.githubusercontent.com/104471340/212449258-0dd4de5d-b4e1-4b7b-a94f-ffae38a27ea0.png)
![image](https://user-images.githubusercontent.com/104471340/212449265-2a34e3d9-2390-4996-8231-53edabf9225e.png)



### Image Standardization
All images resolution were standardized to the same dimensions within each model. The aspect ratio of images were also retained the same for all models.

### Data Augmentation
As mentioned, the dataset was imbalanced and therefore augmentation was used to increase the number of healthy images to have approximately similar numbers to diseased image set. This involved image flip (on X or Y axis), rotation (up to 40 degrees), and varying brightness (factor of 1 to 1.4 times original).

Model 1 had a decent number of data per group, and included images that could have multiple diseases present (because the model was simply classifying as healthy vs diseased). However, for Models 2, 3 and 4, images with multiple diseases present were Excluded from analyses and modeling. THis greatly reduced the available dataset, but allowed for focused modeling on each disease of interest.   The number of healthy cases available for Models 2-4 were particularly limited. Additional data would be useful to build on the current model results.


## :chart_with_upwards_trend: Modeling

Models were optimized by varying parameters including which original layers were frozen in the base model, image resolution used (150 to 1440 pixels), the number of dense layers and nodes/layer used, varying % dropout, optimizers used (Adam, RMSProp, or SGD), and learning rates. Each model was optimized following A/B testing with 10-30 experiments, evaluated by recall, F1 score, and accuracy.

The results of the 
-MODEL 1: 45 disease pooled - 94% recall, 88% accuracy

-MODEL 2: Diabetic Retinopathy - 94% recall, 95% accuracy

-MODEL 3: Macular Degeneration - 94% recall, 88% accuracy

-MODEL 4: Multiclass Model (Myopia - 94% recall, strokes/clots - 82% recall, and cataracts - 77% recall).


## :high_brightness: Conclusions

The results of Retinal Scanner modeling indicate promising outcomes in regards to recall (ability to detect disease cases and not miss cases), precision (ability to correctly label disease cases) and overall accuracy. The results are tabulated above for each of the 4 models.  Further work could include:
- application of the models to larger datasets to evaluate more broad application and improve model metrics, 
- additional modeling development for rare diseases of interest, 
- development of multi-label classifiers.

Please let me know what you think of the models and if you have improvements or suggestions on next steps. Thanks!
