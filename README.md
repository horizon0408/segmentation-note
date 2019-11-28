# detection, segmentation paper note

<a href="https://arxiv.org/pdf/1506.01497.pdf">Faster R-CNN:Towards Real-Time Object Detection with Region Proposal Networks</a>
* the convolutional feature maps used by region-based detectors can also be used for generating region proposal.
    + the system consist of two modules: a FCN for proposing regions and the Fast R-CNN detector
    + shared conv layer(feature extractor), share computation
* Region Proposal Network (RPN)
    + input: any size of image, output: a set of rectangular object proposals, each with an objectness score.
    + after the shared conv layers, to generate region proposal, slide a small network over the feature map. Each sliding window is mapped to a lower-dimensional feature; two fully-connected layers both use the lower-dimensioanl feature to do box-regression and box-classification separately.
    + Anchors
        + novel way to address multiple scales, can use features from single-scale image, no extra cost
        + for each sliding-window location, k proposals of different scales and aspect ratios
        + translation invariant
    + unified with Fast R-CNN: during training, alternates between fine-tuning for region proposal ans fine-tuning for object detection
    

    



<a href="https://arxiv.org/pdf/1703.06870.pdf">Mask R-CNN</a>
* Mask R-CNN = Faster-RCNN + FCN on RoIs (parallel heads)
* decouple mask and class prediction
    + for each RoI, the mask branch has Km^2 dimensional(m×m resolution masks for K classes) output, no competetion among classes
    + per-pixel sigmoid and binary loss rather than per-pixel softmax and multinominal cross-entropy loss
    + for RoI with ground-truth class k, only k-th mask will contribute the mask loss
* RoIAlign
    + Compared to RoIPool(not designed for segemrntaion but object detection so have misalignment), no quantization


