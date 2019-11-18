#SPPNet
##Title: Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition
An improvement network based on RCNN
##Promblem with RCNN
+ Large amount of calculation
##Solution
To solve the promblem RCNN exists, authors propose a pipeline as shown below:

<img src="https://img-blog.csdn.net/20150710153716157" width="80%">

In RCNN, researchers need to utilize the selective search method to obtain 2000 ROI and input each of them into different AlexNet respectively to obtain 2000 1x4096 vectors. But this operation will take a large amount of calculation. 

So the author proposes that if we can input the whole image into only one AlexNet and get a feature map on conv5 layer and relocate the ROI on the corresponding place of the feature map. In this way, researchers can greatly reduce the amount of calculation.

This method face two challenge:

+ How to relocate the ROI on the corresponding place of feature map
+ The fc layers demand fixed-length vectors as inputs. How to design a network to let the output of this network have the same size when ROI on feature map are always in different size.
###For question one: 

In the detection algorithm, a window is given in the image domain, and author ues it to crop the convolutional feature map which have been sub-sampled several times.So author need to align the window on the feature maps. In their implementation, they project the corner point of a window onto a pixel in the feature maps, suchthat this corner point in the image domain is closest to the center of the receptive file of that feature map pixel. They set the padding to kernel size/2, so the left (top) boundary x'=[x/stride]+1, the right (bottom) boundary x'=[x/stride]-1.

###For question two:

They design a Spp-Net as shown below:
<img src="https://img-blog.csdn.net/20150710160322260" width="70%">

They apply three different pooling layer to the feature map (conv5). Assert the size of feature map is CxHxW, they use a maxpooling with size of HxW, a maxpooling with size of (H/4)x(W/4) and a maxpooling with size of (H/16)x(W/16), so they get three maxtric with size of Cx1, Cx4 (Actually, they get a matric with size of Cx2x2, and they post-operate to get Cx4 vector. In pytorch, we can use tensor.view(C,-1)) and a maxtric with size of Cx16. They concatenate them together and they get a matric with size of Cx(1+4+16), so they get a definitive size input for the fc layer.