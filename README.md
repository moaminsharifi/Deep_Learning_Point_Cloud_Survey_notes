# Deep Learning for 3D Point Clouds: A Survey Notes 

[Article in Arxiv](https://arxiv.org/abs/1912.12033)

in this repo I write some notes when I read article.
--
## 1- Introduction:
### Point Cloud usage:

- Computer vision
- Autonomous driving
- Robotics
- Medical treatment

### Sensors:
- LiDAR
- RGB-D (Kinect, RealSense, Apple depth)

### Common formats for 3D data
- depth image
- point cloud
- meshes
- volumetric
### 3D point cloud challenges
- small scale of datasets
- high dimensionality
- unstructured nature of 3D point cloud

### 3D Point Cloud datasets
 - [6] MobileNet
 - [7] ScanObjectNN
 - [8] ShapeNet
 - [9] PartNet 
 - [10] S3DIS 
 - [11] ScanNet
 - [12] Semantic3D
 - [13] ApolloCar3D
 - [14],[15] **KITTI Vision Benchmark Suite **

### 3D Point Cloud Tasks:
- 3D shape classification
- 3D Object Detection
- 3D Point Cloud Segmentation


## Background

### Datasets Type
 - Synthetic Dataset: 
    - objects are complete
    - without any occlusion and Background
 - Real-world Dataset:
    - some objects are contaminated with background noises
    - occluded with background noise
### Datasets
 - [6] MobileNet
 - [7] ScanObjectNN
 - [8] ShapeNet
 - [9] PartNet 
 - [10] S3DIS 
 - [11] ScanNet
 - [12] Semantic3D
 - [13] ApolloCar3D
 - [14],[15] **KITTI Vision Benchmark Suite **
### Metrics
 - **Classification**
    - `Overall Accuracy` (OA): mean of all classes
    - `Mean Class Accuracy` (mAcc): mean accuracy for all shape classes
- **Object Tracking**
    - `Average Precision` (AP)
    - `Precision` and `Success` use in overall performance of a 3D single object tracker
    - `Average Multi-Object Tracking Accuracy` (AMOTA) and `Average Multi-Objet Tracking Precision` (AMOTP) for evaluate 3D multi-object tracking
- **Segmenting**
    - `mean Intersection over Union` (mIou) and `mean class Accuracy` (mAcc) for evaluate performance
    - `mean Average Precision` (mAP) in instance segmentation

## 3D Shape Classification
Methods for this task usually learn the embedding of each point first and then extract a global shape embedding from the whole point cloud using an aggregation method. Classification is finally achieved by feeding the global embedding into several fully connected layers. 

#### 3D Shape Classification methods
- **Multi-View Based**:
    - Project an unstructured point cloud into 2D images

- **Volumetric Based**
    - convert a point cloud to 3D volumetric representation. then use 2D or 3D `convolutional` for classification
- **Point Based**
    - directly work on raw point cloud without any `voxelization`

### Multi-View Based Methods

### Volumetric-based Methods
### **Point-based Methods**