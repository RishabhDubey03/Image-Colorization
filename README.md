# Image-Colorization


## RGB and Lab

RGB and CIE Lab (or just "Lab") are two different color spaces, or ways of describing colors.RGB operates on three channels: red, green and blue. Lab is a conversion of the same information to a lightness component L*, and two color components - a* and b*.

RGB color space: <br />
R - indicating how much Red the pixel is <br />
G - indicating how much Green the pixel is <br />
B - indicating how much Blue the pixel is <br />

Lab color space: <br />
L - encodes Lightness of each pixel <br />
a - encode how much green-red each pixel is <br />
b - encode how much yellow-blue each pixel is <br />

<img width="250" alt="image" src="https://user-images.githubusercontent.com/76114538/176742760-7d9f84f6-13f7-4f44-b6c4-2d6b9e619f23.png"> <img width="210" alt="image" src="https://user-images.githubusercontent.com/76114538/176743023-32ed043c-7528-4043-b81f-67f2388fa190.png">




## Our Conditional GAN:

### Generator:
Using Lab color space info, 
1. L channel(which is the grayscale image) is given to the generator model(U-net architecture)  
2. It predict the other two channels (*a, *b) and after its prediction, we concatenate all the channels and we get our colorful image.

<img width="400" alt="image" src="https://user-images.githubusercontent.com/76114538/176705408-a4d4fff3-c5f9-4d02-a493-6fdc0d776536.png">

### Discriminator:
1. The discriminator(convolutional “PatchGAN” classifier), takes these two produced channels and concatenates them with the input grayscale image and decides whether this new 3-channel image is fake or real.
2. Also discriminator(convolutional “PatchGAN” classifier) also takes real images (3-channel images again in Lab color space) that are not produced by the generator and decides whether this new 3-channel image is fake or real.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/76114538/176712855-59f929fc-2638-4eaa-aa5e-1ffe202e8512.png">

### Loss Function for our conditional GAN:

#### Discriminator Loss Function:
<img width="538" alt="image" src="https://user-images.githubusercontent.com/76114538/176714218-defcf8b3-65ff-4c4d-9f2b-ae725ee36f73.png">

Here, </br>
 G - generator model </br>
 D - discriminator </br>
 x - grayscale image </br>
 z - input noise for the generator </br>
 y - the 2-channel output we want from the generator (it can also represent the 2 color channels of a real image) </br>

#### Generator Loss Function:
L1 Loss (mean absolute error) of the predicted colors compared with the actual colors:

 <img width="531" alt="image" src="https://user-images.githubusercontent.com/76114538/176715496-050964fb-fdb8-4b04-859e-07f5d16d2d39.png">
 L1 Loss is preferred over L2 loss because it reduces effect of producing gray-ish images.
 
 Combined loss function will be:
 
 <img width="530" alt="image" src="https://user-images.githubusercontent.com/76114538/176715924-a0ed818d-5fa3-49c3-88d4-da3872e80faf.png">
 
 
## Results

#### After Epoch 1:
Input Image (Black & White), Output Image (Colored), Real Image respectively: </br>

![WhatsApp Image 2022-06-30 at 11 06 20 PM (1)](https://user-images.githubusercontent.com/76114538/176744626-921c3056-2a01-4a4d-9bfb-d59333cbb44a.jpeg)

![WhatsApp Image 2022-06-30 at 11 06 20 PM](https://user-images.githubusercontent.com/76114538/176744817-ae298656-6302-45eb-89f3-fc06378a1c8f.jpeg)


#### After Epoch 23:
Input Image (Black & White), Output Image (Colored), Real Image respectively: </br>

![WhatsApp Image 2022-06-30 at 11 03 47 PM (1)](https://user-images.githubusercontent.com/76114538/176744203-4f55f1cc-c504-47cc-997e-17c8ac409e06.jpeg)

![WhatsApp Image 2022-06-30 at 11 03 47 PM](https://user-images.githubusercontent.com/76114538/176744267-f84dacfc-0c74-4837-bcac-4a18c0317671.jpeg)





