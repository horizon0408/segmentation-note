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
* unified with Fast R-CNN, 4-step alternating training
    + during training, alternates between fine-tuning for region proposal ans fine-tuning for object detection
    

    

<a href="https://arxiv.org/pdf/1703.06870.pdf">Mask R-CNN</a>
* Mask R-CNN = Faster-RCNN + FCN on RoIs (parallel heads)
* decouple mask and class prediction
    + for each RoI, the mask branch has Km^2 dimensional(m×m resolution masks for K classes) output, no competetion among classes
    + per-pixel sigmoid and binary loss rather than per-pixel softmax and multinominal cross-entropy loss
    + for RoI with ground-truth class k, only k-th mask will contribute the mask loss
* RoIAlign
    + Compared to RoIPool(not designed for segemrntaion but object detection so have misalignment), no quantization

<a href="https://arxiv.org/pdf/1801.00868.pdf">Panoptic Segmentation</a>
* semantic segmentation + instance segmentation
    + semantic segmentation: 
        + assign class label to each pixel, no need to disinguish instance within the same class
        + recognize *stuff*, amorphous and uncountable regions of similar texture like grass, sky, road
    + instance segmentation: 
        + detect *things*, countable objects like pedestrian, bicycle
    + panoptic segmentation:
        + assign each pixel a semantic label and an instance id; 
        + for *stuffs*, the instance id is ignored (will belong to the same instance)
        + no overlap predictions are possible
        
* panoptic quality(PQ) metric
    + segment matching
        + match only if the intersection over union (IoU) is strictly greater than 0.5
        + at most 1 predicted segment can be matched with each GT segment (non-overlapping)
    + PQ computation
        + calculate for each class independently and average over classes
        + all segments receive equal importance regardless of their area
        + can be seens as multiplication of a segmentation quality(SQ) and a recognition quality(RQ)
        + no evaluation on void labels(out of class pixels, ambiguous/unknown pixels)
        
        
