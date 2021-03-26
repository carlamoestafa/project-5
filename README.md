# IMAGE CLASSIFICATION OF RUNNING ROUTES USING NEURAL NETWORKS

___
## OBJECTIVE
The objective of this project is classify 4 types of running routes: city_run, park_run, riverside_run, seaside_run.


## DATA
Image data was created from 500 screenshots of running routes from websites such as [Strava](https://www.strava.com/local), [Map My Run](https://www.mapmyrun.com/routes/search), [Great Runs](https://greatruns.com/lists/main-lists/#), [Parkrun](https://www.parkrun.fr/events/#geo=5/46.58/2.86), google search etc.
The dataset contains 500 images: 400 images for train data (100 images/class)  & validation, 100 images for test data (25 images/class). 
Data Augmentation was also used during some modeling iterations. 
Data preprocessing prior feeding to the neural networks include vectorization into tensors and normalization.

## MODELING ITERATIONS
he neural network modeling exercises were carried out step-by-step.
During the initial phase, the modeling started with few layers of  only dense classifier layers, increased the size of the layers and finished by modeling which consist of adding   blocks of convolutional networks with dense classifier layers and varying number of epochs were assessed by comparing the train and validation accuracy and cross entropy loss results. 
The conclusion from this phase was that the model that consists of 3 blocks of convolutional networks (32, 64, 128 channels) with dense classifiers(512, 4) was the model that provided best accuracy scores.

The following phase of the modeling was to incorporate regularization such as dropout and data augmentation using the following parameter ranges:

| Parameters           | Evaluation Range |Selected Model | 
|:---------------------|:----------------:|:-------------:|
| RMSprop optimizer lr |0.1 - 0.0001      | 0.0001        | 
| Dropout              | 0.1 - 0.5        | 0.5           | 
| Data Augmentation:   |                  |               |
|  Rotation	           | 10 -40	          | 10            |
|  Width shift 	       | 0.1 – 1          | 0.5           |	
|  Height shift 	     | 0.1 – 0.5        | 0.1           |       	
|  Zoom 		           | 0.1 – 1.5	      | 0.5           |
|  Shear range		     | 0.1 – 0.5	      | 0.25          |

Here is the summary of the selected model from the latest modeling iterations:
![Model Summary](model_summary.pdf)


## RESULTS 
The train and validation accuracy results from the modeling iterations were as follows:
* dense classifier layers only: approx  0.2– 0.3
* 1 layer of Conv2D : up to 0.4
* 2 - 3 layers of Conv2D + dense layers: up to 0.6

It is important to note that all the models evaluated were 'not stable', which means that the evaluation results were not consistent between multiple repeats of model evaluation. Partly, this was probably due to the small size of the dataset.
Dropout regularization and data augmentation helped a little bit but didn't solve the inconsistency. 
Another observation from model evaluations was that models that include data augmentation shown tendency  to perform better at model testing & prediction.

Here the results from the selected model: 

Train & Validation cross entropy loss & accuracy:
![Evaluation Loss & Accuracy]( /Users/carlamoestafa/Documents/GitHub/project-5/results/cnn_augmented_10.png)

Model Test Confusion Matrix:
![Confusion Matrix](/Users/carlamoestafa/Documents/GitHub/project-5/results/test_cnn_aug_10.png)

Command: csvtomd /Users/carlamoestafa/Documents/GitHub/project-5/results/test_cnn_aug_10.csv

We can see from the confusion matrix that the model was struggling classifying the riverside run and it struggled more specifically in differentiating riverside runs from seaside runs. The model was able, however, to classify other classes reasonably well.

Examples of Model Prediction:

[city_95](city_95.png)

Labelled : City Run
Predicted: City Run

Predicted class probabilities: 
|Class                     | Probability|
|:-------------------------|:-----------|        
| Class 0 - city run       | 0.34       |
| Class 1 - park run       | 0.30       |
| Class 2 - riverside run  | 0.27       |
| Class 3 - seaside run    | 0.09       |

[park_5](park_5.png)

Labelled : Park Run
Predicted: Park Run

Predicted class probabilities: 
|Class                     | Probability|
|:-------------------------|:-----------|        
| Class 0 - city run       | 0.32       |
| Class 1 - park run       | 0.34       |
| Class 2 - riverside run  | 0.27       |
| Class 3 - seaside run    | 0.07       |

[river_70]('river_70.png')

Labelled : River Run
Predicted: City Run

Predicted class probabilities: 
|Class                     | Probability|
|:-------------------------|:-----------|        
| Class 0 - city run       | 0.34       |
| Class 1 - park run       | 0.26       |
| Class 2 - riverside run  | 0.31       |
| Class 3 - seaside run    | 0.09       |

[seaside_65]('seaside_65.png')

Labelled : Seaside Run
Predicted: Seaside Run

Predicted class probabilities: 
|Class                     | Probability|
|:-------------------------|:-----------|        
| Class 0 - city run       | 0.1        |
| Class 1 - park run       | 0.04       |
| Class 2 - riverside run  | 0.18       |
| Class 3 - seaside run    | 0.68       |


## CONCLUSIONS

Despite small size of dataset the model was able to do the classification reasonably well.
Larger dataset might help in addressing issue with the stability of the model evaluation and test results. 

## NEXT STEPS
* Try and increase dataset size. 
* Continue with finding the right number of layers, size and other parameters for the 'best model'
* Visualizing heatmaps of class activation to identiy which parts of the image belongin to a given class. 


## PROJECT DELIVERABLES:

[DATASET PREPARATION](project_5_dataset_final.ipynb)

[CNN CLASSIFICATION](project_5_convnet_final.ipynb)

[PROJECT PRESENTATION](project_5_presentation.pptx)
