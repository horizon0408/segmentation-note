# segmentation-note

<a href="https://arxiv.org/pdf/1703.06870.pdf">Mask R-CNN</a>
* Mask-RCNN = Faster-RCNN + FCN on RoIs (parallel heads)
* decouple mask and class prediction
    + for each RoI, the mask branch has Km^2 dimensional(m×m resolution masks for K classes) output, no competetion among classes
    + per-pixel sigmoid and binary loss rather than per-pixel softmax and multinominal cross-entropy loss
    + for RoI with ground-truth class k, only k-th mask will contribute the mask loss
* RoIAlign
    + Compared to RoIPool(not designed for segemrntaion but object detection so have misalignment), no quantization


