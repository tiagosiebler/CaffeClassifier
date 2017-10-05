# Card Classifier

Use pretrained neural networks to estimate what playing card is currently given via image. Output returns top 5 matches, each with degree of certainty. 

Example output:
```[
{ "value": 0.9929, "match":"8c"}
,
{ "value": 0.0071, "match":"8s"}
,
{ "value": 0.0000, "match":"8h"}
,
{ "value": 0.0000, "match":"8d"}
,
{ "value": 0.0000, "match":" noise"}
]```

## Prerequisites
- OpenCV 3
- Caffe
- libboost_system (brew install boost)
- libglog (brew install glog)

### Caffe Notes
In the Makefile.config, ensure the following is present and uncommented:

```CPU_ONLY := 1
OPENCV_VERSION := 3
BLAS_INCLUDE := $(shell brew --prefix openblas)/include 
BLAS_LIB := $(shell brew --prefix openblas)/lib```

Then:
```make all -j8
make test -j8
make runtest
make distribute -j8```

## Usage
`CaffeClassifier deploy.prototxt network.caffemodel mean.binaryproto labels.txt targetImage.jpg`


## Notes
- This process is too slow to be used in a live scenario, but can be used to build a dictionary for later access. Assuming there is a limited dataset.
- This Xcode project is heavily based on the C++ classification example from the Caffe repo by the Berkeley Vision and Learning Center: https://github.com/BVLC/caffe/blob/master/examples/cpp_classification/classification.cpp