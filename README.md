# Deep Clustering Project

The aim of this project is to cluter imagens using deep models. <br/>
The models trained in the 'autoencoder' repository will be used in this project.

## About the Project

The models were developed in Python using Keras.<br/>
The models were validated using 5-folds cross-validation and all of them were tested on the same dataset.<br/>
As examples, we trained the autoencoder with 2 datasets: CIFAR-10 and MNIST.<br/>
For each dataset three steps will be carried out.
* The images will be flattened and clusterized using k-means;
* Each image will be inserted into the encoder derived from the autoendores of the other project. The output of the encoder will be clustered using k-means. <br/>
* A clustering layer is placed on the top of the encoder model and the new model is trained as a self supervised model. This is the deep clusterinig model developed. <br/>

As the autoencoder model was trained with 5-folds cross-validation, the 5 models will be used here. This way, the clusterization using the putpout of the encoder will be done 5 times and 5 deep clustering models will be traied. Model over, the training part of each clusterization will be caried out with the respective subsets used in the traing of each autoendor during the cross-validation, and the same subset of images will be used as test dataset. Hence, the tests realized and the comparison between the models are fair.

## About the Training
In both examples, the models were trained with backpropagation using Adam  algorithm.<br/>
The training was performed for 100 epochs with batch size = 32.<br/>
The loss used while training the model with CIFAR-10 was a combination of mean squared error and cosine similarity (multiplied by minus 1). And the loss used while training the model with MNIST was the mean squared error.


## Models

The models consist of some blocks of convolutional, activation and batch normalization layers and blocks of fully connected (dense) layers. The output of the encoder part of model trained with the CIFAR-10 dataset is an array with size 128x1. The autoencoder trained with the MNIST dataset was a little changed, so that the output size of encoder part could have the same size as the numeber of known classes of this dataset (that is, an array of size 10x1).<br/>
For shrinking and increasing the height and width of the data throughout the model it was used max pooling and up sampling with nearest neighbour interpolation, respectively. All the convolutions were made using same padding.  <br/>
The figures below show the models developed and the legend that explains what each layer is.<br/>
In the image, the data flows from the left to the right. This way, the left grey box represents the original image and the right grey box representes the reconstructed one. 

#### Model trained with MNIST dataset

![model flowchart - mnist](https://user-images.githubusercontent.com/58445878/103463149-0cd0ff80-4d09-11eb-8957-a0079d98d89e.png)

#### Model trained with CIFAR-10 dataset

![model flowchart - cifar10](https://user-images.githubusercontent.com/58445878/103463163-1fe3cf80-4d09-11eb-9375-a5f42160ac97.png)

#### Legend

<img src="https://user-images.githubusercontent.com/58445878/103463169-2b36fb00-4d09-11eb-80e9-b5bff48420d7.png" width="600">


## Results

The images belows show 25 images of each dataset chosed randomely from the test datasets of each dataset (CIFAR-10 / MNIST) and their reconstruction with by one of the models trained in the crossvalidation for each dataset. The graphics for the mean squared error evolution during the training are also presented.

#### Results of the model trained with MNIST dataset

![examples_originalImagens](https://user-images.githubusercontent.com/58445878/103464279-32fa9d80-4d11-11eb-9ad6-9ea8cd79f6d8.jpg)

![examples_ReconstructedImagens_NN0](https://user-images.githubusercontent.com/58445878/103464281-355cf780-4d11-11eb-9864-664fc3c75d93.jpg)

![Encoder_TrainHistory_loss_0](https://user-images.githubusercontent.com/58445878/103463429-122f4980-4d0b-11eb-94f7-f018b1e41191.jpg)

#### Results of the model trained with CIFAR-10 dataset

![examples_originalImagens](https://user-images.githubusercontent.com/58445878/103464293-50c80280-4d11-11eb-90f5-24bbf12864ab.jpg)

![examples_ReconstructedImagens_NN0](https://user-images.githubusercontent.com/58445878/103464297-53c2f300-4d11-11eb-8fa5-2c2a273c9810.jpg)

![Encoder_TrainHistory_Mean_Squared_Error_0](https://user-images.githubusercontent.com/58445878/103463473-60dce380-4d0b-11eb-84ee-46b982e8caf6.jpg)


## Comments

Although the reconstruction of the MNIST images got really good results, the reconstructions of the CIFAR-10 images could be improved. This way, more work will be done with this goal.<br/>
Also, looking at the  mean squared error graphics it is possible to see that there is still a small slope in the end of the 100 epochs. It could be interest to train the models for a little longer to see if the results would be improved.<br/>
Moreover, it is important to remember the ultimate goal is to use this autoencoders to help in the clusterization of these datasets. Then, to get a perfect reconstruction is not the most important here.<br/>
Last, we want to test train an autoencoder with an output with size 10x1 for the encode part, once it will probably help during the clusterization phase.<br/>
