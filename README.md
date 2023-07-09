# Style Transfer: Project Overview
This project demonstrates the application of style transfer techniques using Adaptive Instance Normalization. It aims to transfer the artistic style of one image (style image) onto the content of another image (content image) to create visually appealing and artistic results.

## Code and Resources Used 
**Python Version:** 3.10  
**Packages:** numpy, matplotlib, tensorflow, keras  
**Data source:** https://www.kaggle.com/datasets/ikarus777/best-artworks-of-all-time
http://host.robots.ox.ac.uk/pascal/VOC/voc2007/

**Article:** https://arxiv.org/pdf/1703.06868.pdf

## Data Structure
For downloading data run next lines
! mkdir ~/.kaggle
! cp kaggle.json ~/.kaggle/
! chmod 600 ~/.kaggle/kaggle.json
! kaggle datasets download ikarus777/best-artworks-of-all-time
! unzip -qq best-artworks-of-all-time.zip
! rm -rf images
! mv resized artwork
! rm best-artworks-of-all-time.zip artists.csv

tfds.load("voc")

Dataset consist of 7000 pairs of style and content images

![alt text](https://github.com/HalyshAnton/Style-Transfer/blob/main/data_visual.png)

## Model Building
The model building process consists of the following steps:
* Encoder: pre-trained CNN model is used as the encoder to extract the features from both the style and content images. By passing the images through the encoder, we obtain feature maps that capture the visual content. I have used VGG19 to block4_conv1 layer
* AdaIN: non-trainable part that normalized content features and linearly shift it to style fearture mean and variance(for more details read article)
* Decoder: The reverse of the encoder process is performed using a decoder. It has reversed architecture without any normalization and UpSampling layers instead Pooling ones. This step involves reconstructing the image from the combined features obtained from the AdaIN step.

![alt text](https://github.com/HalyshAnton/Style-Transfer/blob/main/model_architecture.png)

## Model Performance
Here are results from trained model after 50 epochs(for better result more epochs are needed)

![alt text](https://github.com/HalyshAnton/Style-Transfer/blob/main/stylized_images.png)
