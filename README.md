# Deep Clustering Project

The aim of this project is to cluter imagens using deep models. <br/>
The models trained in the [autoencoder](https://github.com/luizamarnet/autoencoder) repository will be used in this project.

## About the Project

The models were developed in Python using Keras and scikit-learn.<br/>
The models were validated using 5-folds cross-validation and all of them were tested on the same dataset.<br/>
The models will be trained with 2 datasets: CIFAR-10 and MNIST.<br/>
For each dataset three steps will be carried out.
* The images will be flattened and clusterized using k-means;
* Each image will be inserted into the encoder derived from the autoendores of the other project. And the output of the encoder will be clustered using k-means. <br/>
* A clustering layer will be placed on the top of the encoder model and the new model will be trained as a self supervised model. This is the deep clusterinig model that we want to train. <br/>

As the autoencoder model was trained with 5-folds cross-validation, the 5 models will be used here. This way, the clusterization using the output of the encoder will be done 5 times and 5 deep clustering models will be trained. Moreover, the training part of each clusterization will be carried out with the respective subsets used in the training of each autoencodor during the cross-validation, and the same subset of images will be used as test dataset. Hence, the tests realized and the comparison between the models are fair.

## About the Deep Clustering Model
The clustering layer used was developed by Chengwei Zhang and copied from his public repository ([Keras_Deep_Clustering](https://github.com/Tony607/Keras_Deep_Clustering)). <br/>
The encoder used in the deep clustering model trained with the MNIST dataset was the one that was trained with the same dataset in the project from my [autoencoder](https://github.com/luizamarnet/autoencoder) repository. The output of this encoder is an array of size 10x1.<br/>
As expalined by [Chengwei Zhang](https://www.dlology.com/blog/how-to-do-unsupervised-clustering-with-keras/), the clustering layer calculates the probability that each sample belongs to each cluster using  student's t-distribution. To do this, the weights that connect the clustering layer with the encoder output layer are used as centers of the clusters. The authors idea for this layer was inspired by the t-SNE algorithm by Laurens van der Maaten and Geoffrey Hinton presented in the article 'Visualizing Data using t-SNE'.<br/>
Also, the labels used while training the deep clustering model are updated after some iterations based on the model's own outputs, updating the target distribution. For this reason the model is called self supervised.<br/>


## Results

Up to now, only the MNIST dataset was used in this project. The results obtained until now are presented below.<br/>
Although the true labels of the classes are not used during any part of the training, once it is a cluserization problem, they are used to avaliate the results and analyse if the models are able to separete the clusters according to the known classes. <br/>
The confusion matrix below shows the true labels against the clusters resulted from flattening the image and applying k-means. Considering the class of each cluster as the majority class of the cluster, the accuracy obtained for the test dataset was: 59.41000 %.

<img src="https://user-images.githubusercontent.com/58445878/103501716-cd500380-4e2d-11eb-8139-65201d731444.jpg" width="600">

Next, using the outputs of the encoder and clusterizing then, the result were improved. Remembering that, since we used 5-folds cross-validation while training the autoencoders, the same respective 5 encoders were used here. This way, the new accuracy for the clusterization, testing the five encoders, was 88.24000 % with standard deviation equal to 2.52979 %. The two confusion matrices below show the results of the clusterization of the outputs of 2 of the 5 encoders.

<img src="https://user-images.githubusercontent.com/58445878/104114187-41802080-52e0-11eb-973e-6aa196e7caf2.jpg" width="600">

<img src="https://user-images.githubusercontent.com/58445878/104114188-447b1100-52e0-11eb-94cc-2fb806c21a1d.jpg" width="600">

Last, also considering the 5-folds cross-validation while traing the deep clustering models, the accuracy for the clusterization with the deep model was 93.49000 %, with standard deviation equal to 4.39761 %. The confusion matrices below show the results for training the deep clustering model with 2 of the 5 pretrained encoders.


<img src="https://user-images.githubusercontent.com/58445878/104114203-6c6a7480-52e0-11eb-90ec-451f1bffeff9.jpg" width="600">

<img src="https://user-images.githubusercontent.com/58445878/104114206-6ffdfb80-52e0-11eb-828a-84e2d947ebb6.jpg" width="600">



## Steps Concluded and Future Works

- [x] To cluster the MNIST dataset flattening the images and applying k-means;
- [x] To compress the MNIST dataset images using the encoders trained and to cluster their outputs applying k-means;
- [x] To train the deep clustering model using the MNIST dataset;
- [ ] To cluster the CIFAR-10 dataset flattening the images and applying k-means;
- [ ] To compress the CIFAR-10 dataset images using the encoders trained and to cluster the outputs applying k-means;
- [ ] To train the deep clustering model using the CIFAR-10 dataset.


## Comments

As we see in the results, the deep clustering model huge improved the results of the clusterization of the MNIST dataset when comparing with the other two clusterizations. <br/>
Nevertheless, the models perfomed better in the deep clustering models trained with some of the pre trained encoders and get confused between some numbers in others. Maybe, improving the results of the autoencoders from which the encoders were taken could solve this problem.
