## FPN
### Title: Feature Pyramid Networks for Object Detection
In this paper, they exploit the inherent multi-scale, pyramidal hierarchy of deep convolutional networks to con- struct feature pyramids with marginal extra cost.

<img src="https://pic1.zhimg.com/v2-15a45ce0641bbb9cd3af36a58cbf1714_r.jpg" width="50%">

### Pyramid construction
The Pyramid construction has three part in following.
+ Bottom-up pathway
  + ResNet backbone 

+ Top-down pathway and lateral connections
  + In my view, this construction is somehow similar to FCN
  + They merge corrsponding layers and get M5-M2.
  + They append a 3x3 convolution on each merged map to generate the final feature map
  + What is not shown in the Fig, they append a maxpooling with stride 2 on P5 to get P6.
  + P2-P6 is the input of RPN for bounding box regression and the author only assign anchors of a single scale to each level which is different to Faster R-CNN.
  + P2-P5 is the input of Fast R-CNN ( using ROI pooling ) to get the output.
  + They assign ROIs of different scale to the pyramid levels according to the following formulation:
    k=[k0+log2(√(wh)/224)]
    Here 224 is the canonical ImageNet pre-training size, and k0 is the target level on which an ROI with wxh=224x224 should be mapped to. They set k0 to 4.

<img src="https://pic4.zhimg.com/v2-fc500b77472298d7dacdd303f509c68b_r.jpg" width="80%">

