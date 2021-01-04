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

## About the Deep Clustering Model
The clustering layer used was developed by Chengwei Zhang and copied from his public repository ([Keras_Deep_Clustering](https://github.com/Tony607/Keras_Deep_Clustering)).<br/>
The encoder used in the deep clustering model trained with the MNIST dataset was the one trained with the same dataset in the project from my respository ([autoencoder](https://github.com/luizamarnet/autoencoder)). The outpout of this encoder is an array of size 10x1.<br/>
As expalined by [Chengwei Zhang](https://www.dlology.com/blog/how-to-do-unsupervised-clustering-with-keras/), the clustering layer calculates the probability that each sample belongs to each cluster using  student's t-distribution. To do this, the weights that connect the clustering layer with the encoder output layer are used as center clusters. <br/>
Also, the labels used while training the deep clustering are updated after some iterations, updating the distribution target. For this reason the model is called self supervised.<br/>




## Results

Up to now, only the MNIST dataset was used in this project. The results obtained until now are presented below.<br/>
Although the true labels of the classes are not used during any part of the training, once it is a cluserization problem, they are used to avaliate the results and analyse if the model is able to separete the clusters according to the known classes. <br/>
The confusion matrix above shows the true labels against the clusterization resulted from flattening the image and apply k-means. Considering the class of each clustering as the majority class of the cluster, the accuracy obtained for the test dataset was: 59.41000 %.
![confusionMatrix_originalImage](https://user-images.githubusercontent.com/58445878/103501716-cd500380-4e2d-11eb-8139-65201d731444.jpg)
Next, using the outputs of the encoder and clusterizing then, the results were improved. Remembering that we used 5-folds cross-validation while training the autoencoders, the same 5 encoders were used here. This way, the new accurecy for the clusterization, testing the five encoders, was 87.22600 % with standard deviation equal to 3.13242 %. The two confusion matrix below show the results of the clusterization of the outputs of 2 of the 5 encoders.

![confusionMatrix_encodedImage_CNN_0](https://user-images.githubusercontent.com/58445878/103501970-94fcf500-4e2e-11eb-8c87-a1cad7d894b7.jpg)

![confusionMatrix_encodedImage_CNN_1](https://user-images.githubusercontent.com/58445878/103502006-acd47900-4e2e-11eb-9004-22be10bf261e.jpg)


Last, also considering the 5-folds cross-validation while traing the deep clustering models, the accuracy for the clusterization with the deep model was 93.47000 %, with standard deviation equal to 4.35613 %. The confusion matrix below show the results founded when training the deep clustering model with 2 of the 5 pre trained encoders.


![confusioMatrix_KerasDeepClusteringModel_0](https://user-images.githubusercontent.com/58445878/103502142-12286a00-4e2f-11eb-8614-cbfa0cc44f8c.jpg)

![confusioMatrix_KerasDeepClusteringModel_0](https://user-images.githubusercontent.com/58445878/103502146-15235a80-4e2f-11eb-88a7-30b4064040c5.png)

## Steps Concluded and Future Works




## Comments

Although the reconstruction of the MNIST images got really good results, the reconstructions of the CIFAR-10 images could be improved. This way, more work will be done with this goal.<br/>
Also, looking at the  mean squared error graphics it is possible to see that there is still a small slope in the end of the 100 epochs. It could be interest to train the models for a little longer to see if the results would be improved.<br/>
Moreover, it is important to remember the ultimate goal is to use this autoencoders to help in the clusterization of these datasets. Then, to get a perfect reconstruction is not the most important here.<br/>
Last, we want to test train an autoencoder with an output with size 10x1 for the encode part, once it will probably help during the clusterization phase.<br/>
