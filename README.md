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
      - [MVCNN \[40\]:](#mvcnn-40)
      - [MHBN \[41\]:](#mhbn-41)
      - [Yang et al. \[42\]:](#yang-et-al-42)
      - [Wei et al. \[47\]:](#wei-et-al-47)
    - [Volumetric-based Methods](#volumetric-based-methods)
      - [Maturana et al. \[48\] (VoxNet):](#maturana-et-al-48-voxnet)
      - [Wu et al. \[6\]:](#wu-et-al-6)
      - [OctNet \[49\]:](#octnet-49)
      - [Wang et al. \[50\]:](#wang-et-al-50)
      - [Le et al. \[51\]:](#le-et-al-51)
      - [Ben-Shabat et al. \[52\]](#ben-shabat-et-al-52)
    - [**Point-based Methods**](#point-based-methods)
      - [Pointwise MLP Methods](#pointwise-mlp-methods)
        - [PointNet \[5\]:](#pointnet-5)
        - [Deep sets \[53\]:](#deep-sets-53)
        - [Qi et al. \[54\] (PointNet++):](#qi-et-al-54-pointnet)
        - [Mo-Net \[55\]:](#mo-net-55)
        - [Point Attention Transformers (PATs) \[56\]](#point-attention-transformers-pats-56)
        - [PointWeb \[57\]](#pointweb-57)
        - [Duan et al. \[58\] (Structural Relational Network (SRN))](#duan-et-al-58-structural-relational-network-srn)
        - [Lin et al. \[59\]:](#lin-et-al-59)
        - [SRINet \[60\]:](#srinet-60)
        - [Yan et al \[61\] (PointASNL)](#yan-et-al-61-pointasnl)
      - [Convolution-based Methods](#convolution-based-methods)
      - [Graph-based Methods](#graph-based-methods)
      - [Hierarchical Data Structure-based Methods](#hierarchical-data-structure-based-methods)
      - [Other Methods](#other-methods)


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

#### MVCNN [40]:
MVCNN [40] is a pioneering work, which simply maxpools multi-view features into a global descriptor. However, max-pooling only retains the maximum elements from a specific view, resulting in information loss

#### MHBN [41]:
integrates local convolutional features by harmonized bilinear pooling to produce a compact global descriptor.
#### Yang et al. [42]:
first leveraged a relation network to exploit the inter-relationships (e.g., region-region relationship and view-view relationship) over a group of views, and then aggregated these views to obtain a discriminative 3D object representation.

#### Wei et al. [47]:
used a directed graph in View-GCN by considering multiple views as graph nodes. The core layer composing of local graph convolution, non-local message passing and selective view-sampling is then applied to the constructed graph. The concatenation of max-pooled node features at all levels is
finally used to form the global shape descriptor.

### Volumetric-based Methods
These methods usually ‍‍`voxelize‍` a point cloud into 3D grids, and then apply a 3D Convolution Neural Network (CNN) on the volumetric representation for shape classification.

#### Maturana et al. [48] (VoxNet):
introduced a volumetric occupancy network called VoxNet to achieve robust 3D object recognition
#### Wu et al. [6]:
proposed a convolutional deep belief based 3D ShapeNets to learn the distribution of points from various 3D shapes 
####  OctNet [49]:
using a hybrid grid-octree structure, which represents the scene with several shallow octrees along a regular grid. The structure of octree is encoded efficiently using a bit string representation, and the feature vector of each voxel is indexed by simple arithmetic

#### Wang et al. [50]:
Octree-based CNN for 3D shape classification. The average normal vectors of a 3D model sampled in the finest leaf octants are fed into the network, and 3D-CNN is applied on the octants occupied by the 3D shape surface. 

**OctNet requires much less memory and runtime for high-resolution point clouds**

#### Le et al. [51]:
proposed a hybrid network called PointGrid, which integrates the point and grid representation for efficient point cloud processing. A constant number of points is sampled within each embedding volumetric grid cell, which allows the network to extract geometric details by using 3D convolutions.

#### Ben-Shabat et al. [52]
transformed the input point cloud into 3D grids which are further represented by 3D modified Fisher Vector (3DmFV) method, and then learned the global representation through a conventional CNN architecture.

### **Point-based Methods**
#### Pointwise MLP Methods 
![A lightweight architecture of PointNet. n denotes the number of input points, M denotes the dimension of the learned features for each point.](assets/fig_4.png)

These methods model each point independently with several shared Multi-Layer Perceptrons (MLPs) and then aggregate a global feature using a symmetric aggregation function.
- * Typical deep learning methods for 2D images cannot be directly applied to 3D point clouds due to their inherent data irregularities.

##### PointNet [5]:
Directly takes point clouds as its input and achieves permutation invariance with a symmetric function. PointNet learns pointwise features independently with several MLP layers and extracts global features with a max-pooling layer
#####  Deep sets [53]:
achieves permutation invariance by summing up all representations and applying nonlinear transformations. Since features are learned independently for each point in PointNet
##### Qi et al. [54] (PointNet++):
proposed a hierarchical network PointNet++ to capture fine geometric structures from the neighborhood of each point

**Layers**:
- the sampling layer
- the grouping layer
- the PointNet based learning layer.
  
PointNet++ learns features from a local geometric structure and abstracts the local features layer by layer.
##### Mo-Net [55]:
is similar to PointNet [5] but it takes a finite set of moments as its input
##### Point Attention Transformers (PATs) [56]
represents each point by its own absolute position and relative positions with respect to its neighbors and learns high dimensional features through MLPs. Then, Group Shuffle Attention (GSA) is used to capture relations between points, and a permutation invariant, differentiable and trainable end-to-end Gumbel Subset Sampling (GSS) layer is developed to learn hierarchical features
##### PointWeb [57]
based on PointNet++, utilizes the context of the local neighborhood to improve point features using Adaptive Feature Adjustment (AFA)
##### Duan et al. [58] (Structural Relational Network (SRN))
proposed a Structural Relational Network (SRN) to learn structural relational features between different local structures using MLP.

##### Lin et al. [59]:

accelerated the inference process by constructing a lookup table for both input and function spaces learned by PointNet. The inference time on the ModelNet and ShapeNet datasets is sped up by 1.5 ms and 32 times over PointNet on a moderate machine

##### SRINet [60]:
first projects a point cloud to obtain rotation invariant representations, and then utilizes PointNet-based backbone to extract a global feature and graph-based aggregation to extract local features

#####  Yan et al [61] (PointASNL)
utilized an Adaptive Sampling (AS) module to adaptively adjust the coordinates and features of points sampled by the Furthest Point Sampling (FPS) algorithm, and proposed a local-nonlocal (L-NL) module to capture the local and long range dependencies of these sampled points.


#### Convolution-based Methods
#### Graph-based Methods
#### Hierarchical Data Structure-based Methods
#### Other Methods