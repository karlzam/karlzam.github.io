# DL Models

## General

### Performance Metrics

## Models 

### YOLO 

### RetinaNet

#### Abstract
- Paper compared performance to YOLOv2 which it outperformed (and also outperformed Faster R-CNN)
- Dense sampling algorithms have always been trailing the accuracy of two-stage detectors until this paper
- They discovered that the extreme foreground-background class imbalance encountered during training of dense detectors is central cause 
- Added a new loss function that down-weights the loss assigned to well-classified examples 
  - Focuses training on hard examples and prevents the vast number of easy negatives from overwhelming the detector during training 
- RetinaNet matches the speed of one-stage detectors and surpasses the accuracy of two-stage detectors (in 2018)

#### Important Takeaways 
- One-stage algorithms (YOLO) are faster than R-CNN
- RetinaNet matches the two-stage performance of Faster R-CNN (and FPN, Mask R-CNN) 
- Does this by identifying class imbalance during training as the main obstacle and proposes a new loss function 
- Loss function is a "dynamically scaled cross entropy loss" where the scaling factor decays to zero as confidence in the correct class increases 
- This scaling factor can automatically down-weight the contribution of easy examples during training and rapidly focus the model on hard examples 
- RetinaNet similar to RPN, SSD, FPN
- Emphasis that the results are due to loss function and not novel architecture 
- Class imbalance: the loss due to frequent class can dominate total loss and cause instability during training
- At the beginning they set the probability of the rare class to be low so that the model expects it to be rare
- Uses the feature pyramid network (FPN) as backbone of RetinaNet
  - Each level of pyramid can detect objects of a different scale 
- Built FPN on top of ResNet architecture 
- we only decode box predictions from at most 1k top-scoring predictions per FPN level, after thresholding detector confidence at 0.05
- The top predictions from all levels are merged and non-maximum suppression with a threshold of 0.5 is applied to yield the final detections
- Uses SGD (stochastic gradient descent)
- **One of the most important design factors in a one-stage detecton system is how densely it covers the space of possible image boxes**
- Used 3 scales and 3 aspect ratios per location
- Increasing beyond 6-9 anchors did not show further gains

#### Code
- FB code: https://github.com/facebookresearch/detectron2 
- Above link updated from detectron to detectron 2, so more up to date than paper 
- Detectron2 includes the retinanet model 
- Info on detectron2: https://ai.meta.com/blog/-detectron2-a-pytorch-based-modular-object-detection-library-/


