# Deep Learning for 3D Point Clouds: A Survey Notes 

[Article in Arxiv](https://arxiv.org/abs/1912.12033)

in this repo I write some notes when I read article.
# Table of content
- [Deep Learning for 3D Point Clouds: A Survey Notes](#deep-learning-for-3d-point-clouds-a-survey-notes)
- [Table of content](#table-of-content)
  - [1- Introduction:](#1--introduction)
    - [Point Cloud usage:](#point-cloud-usage)
    - [Sensors:](#sensors)
    - [Common formats for 3D data](#common-formats-for-3d-data)
    - [3D point cloud challenges](#3d-point-cloud-challenges)
    - [3D Point Cloud datasets](#3d-point-cloud-datasets)
    - [3D Point Cloud Tasks:](#3d-point-cloud-tasks)
  - [Background](#background)
    - [Datasets Type](#datasets-type)
    - [Datasets](#datasets)
    - [Metrics](#metrics)
  - [3D Shape Classification](#3d-shape-classification)
      - [3D Shape Classification methods](#3d-shape-classification-methods)
    - [Multi-View Based Methods](#multi-view-based-methods)
      - [`MVCNN [40]`:](#mvcnn-40)
      - [`MHBN [41]`:](#mhbn-41)
      - [`Yang et al. [42]`:](#yang-et-al-42)
      - [`Wei et al. [47]`:](#wei-et-al-47)
    - [Volumetric-based Methods](#volumetric-based-methods)
    - [**Point-based Methods**](#point-based-methods)

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
 - [14],[15] **KITTI Vision Benchmark Suite**

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

These methods first project a 3D shape into multiple views and extract view-wise features, and then fuse these features for accurate shape classification. 

#### `MVCNN [40]`:
MVCNN [40] is a pioneering work, which simply maxpools multi-view features into a global descriptor. However, max-pooling only retains the maximum elements from a specific view, resulting in information loss

#### `MHBN [41]`:
integrates local convolutional features by harmonized bilinear pooling to produce a compact global descriptor.
#### `Yang et al. [42]`:
first leveraged a relation network to exploit the inter-relationships (e.g., region-region relationship and view-view relationship) over a group of views, and then aggregated these views to obtain a discriminative 3D object representation.

#### `Wei et al. [47]`:
used a directed graph in View-GCN by considering multiple views as graph nodes. The core layer composing of local graph convolution, non-local message passing and selective view-sampling is then applied to the constructed graph. The concatenation of max-pooled node features at all levels is
finally used to form the global shape descriptor.

### Volumetric-based Methods
### **Point-based Methods**