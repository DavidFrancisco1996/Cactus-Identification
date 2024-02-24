# Aerial Cactus Identification

The objective of this project is to identify whether aerial images contain columnar cacti, as part of the [Aerial Cactus Identification](https://www.kaggle.com/c/aerial-cactus-identification/data) competition. This competition is based on resesearch previously hosted on kaggle - original dataset can be found [here](https://www.kaggle.com/irvingvasquez/cactus-aerial-photos). 


## Sample images for classification:

The training dateset includes 17,500 32x32 jpeg aerial images images. Each training image is labeled as whether or not it columnar cactus are present in the image. Test predictions are generated for submission on 4000 32x32 pixel jpeg aerial images. 

#### Cacti: 

<p align="left"><a href="Cacti"><img src="/images/1.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/2.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/3.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/4.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/11.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/5.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/6.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/7.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/8.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/9.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/10.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/12.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/13.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/14.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/15.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/16.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/17.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/18.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/19.jpg" align="center" height="100" hspace="5"></a><a href="Cacti"><img src="/images/20.jpg" align="center" height="100" hspace="5"></a></p>

## Data Augmentation
Keras' [`ImageDataGenerator`](https://keras.io/preprocessing/image/#imagedatagenerator-class) class allows the augmentation of input image to artificially expand the total size of the input training dataset:

```python
train_datagen = ImageDataGenerator(rescale=1./255,
                                   validation_split=0.1,
                                   rotation_range=40,
                                   shear_range=0.2,
                                   width_shift_range=0.2,
                                   height_shift_range=0.2,
                                   horizontal_flip=True,
                                   zoom_range=0.2,
                                   fill_mode='nearest')
```

## Transfer Learning - VGG16 Base Layers
For an initial attempt, I explored using a frozen [VGG16](https://arxiv.org/abs/1409.1556) base model pretrained on the [ImageNet](http://www.image-net.org) dataset. I did not retrain these layer given the similarity of cacti to other objects in the imagenet dataset. 


## Model Parameters:
<p align="center"><a href="model params"><img src="/images/model_params.png" align="center" width="600" ></a></p>


## Evaluation
After 200 training epochs, the model settled at a validation loss of ~0.10 and a validation accuracy of ~0.96
<p align="center"><a href="Loss + Accuracy"><img src="/images/acc.png" align="center" width="600" ></a></p>

## Submission Score
Submission with this model scores an area under the ROC curve of 0.9929 on the test dataset. 
