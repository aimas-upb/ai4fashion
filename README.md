# ai4fashion

The dataset used for this project is created by extracting and processing images from two other datasets:
   * LookBook from https://dgyoo.github.io/
   * SmallFashion from https://www.kaggle.com/paramaggarwal/fashion-product-images-small
   
Lookbook dataset 

1.
  - extracting the catalogue images searching by a specific part of the image name ('CLEAN1')
  - resize images to 256*256 and add white borders to get a similar image format
  - see [lookbookResizedCatalogueImages.ipynb](https://github.com/ami-lab/ai4fashion/blob/master/lookbookResizedCatalogueImages.ipynb)
2.
  - get the dominant color for images of the dataset created
  - see [LookbookGetDominantColor.ipynb](https://github.com/ami-lab/ai4fashion/blob/master/LookbookGetDominantColor.ipynb)
  
SmallFashion dataset
  - extracting the catalogue images (manually)
  - each image size was already 256*256
  - get the dominant color for each image
  - see [SmallFashionGetDominantColor.ipynb](https://github.com/ami-lab/ai4fashion/blob/master/SmallFashionGetDominantColor.ipynb)
  
In order to get the dominant color, the idea behind it was to divide the color space in specific intervals and assign a color to an image
by taking into account the RGB values and saturation.
The method used is similar for both cases (images from Lookbook and SmallFashion), with small diferences in order to get better results.

The results were not entierly correct and some of the images had to be annotated manually. Further improvements can be made.

The dataset was created using all the previously obtained images. Moreover, annotations were assigned to each image related to the product type.

The information regarding the dominant color and the product type can be found in the name of the image.
Ex: red_originalImgName_1

Colors used: black, blue, brown, green, grey, orange, pink, purple, red, white, yellow.
See Color distribution ![colorDistribution.png](https://github.com/ami-lab/ai4fashion/blob/master/results/colorDistribution.png)

Product types:
1-Dresses, 2-Tops, 3-TShirts, 4-Shirts, 5-Blouses, 6-Jackets, 7-Shorts, 8-Pants, 9-Jeans, 10- Skirts, 11-Jumpsuits, 12-Coats.
See Product type distribution ![productTypeDistribution.png](https://github.com/ami-lab/ai4fashion/blob/master/results/productTypeDistribution.png)


 * Using DCGAN to generate catalogue style clothing (https://pytorch.org/tutorials/beginner/dcgan_faces_tutorial.html)
      - Number of workers for dataloader: workers = 2
      - Batch size during training: batch_size = 128
      - Spatial size of training images. All images will be resized to this size using a transformer: image_size = 64
      - Number of channels in the training images: nc = 3
      - Size of z latent vector: nz = 100
      - Size of feature maps in generator: ngf = 64
      - Size of feature maps in discriminator: ndf = 64
      - Number of training epochs: num_epochs = 25
      - Learning rate for optimizers: lr = 0.0002
      - Beta1 hyperparam for Adam optimizers: beta1 = 0.5
      - No GPUs available (CPU mode)
      
The discriminator is made up of strided convolution layers, batch norm layers, and LeakyReLU activations.

The generator is comprised of convolutional-transpose layers, batch norm layers, and ReLU activations. The input is a latent vector, z, that is drawn from a standard normal distribution and the output is a 3x64x64 RGB image. 
      
 Results:
 ![training_result.png](https://github.com/ami-lab/ai4fashion/blob/master/results/training_result.png)
 ![loss_plot.png](https://github.com/ami-lab/ai4fashion/blob/master/results/loss_plot.png)
 ![loss.png](https://github.com/ami-lab/ai4fashion/blob/master/results/loss.png)
 
