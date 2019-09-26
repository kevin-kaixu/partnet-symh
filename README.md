# The PartNet Symmetry Hierarchy Dataset (PartNet-Symh)

The PartNet-Symh dataset augments the PartNet dataset by adding a recursive hierarchical organization of fine-grained parts for each shape. The PartNet dataset was originally proposed in the paper "PartNet: A Large-scale Benchmark for Fine-grained and Hierarchical Part-level 3D Object Understanding". The symmetry hierarchies were used to train the PartNet model in our paper "PartNet: A Recursive Part Decomposition Network for Fine-grained and Hierarchical Shape Segmentation". In general, PartNet-Symh can be used to train any Recursive Neural Networks models for part-level shape structure encoding/decoding, e.g., GRASS [Li et al. 2017].

### Introduction

PartNet consists of 24 object categories. The 3D models in the dataset are composed of fine-grained parts. We construct a recursive symmetry hierarchy [Wang et al. 2011] based on the fine-grained parts. The data organization follows the original PartNet dataset.

### Basic information

The dataset contains 22699 3D shapes covering 24 shape categories:

|  category_name  |  lamp   | table | knife   |  bag   | bed  | bottle   | bowl   | clock   | display   | dishwasher   | door   | earphone   | faucet   | hat   | storage   | keyboard   | laptop   | microwave   | mug   | refrigerator   | scissors   | trashcan   | vase   | chair   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| number of shapes | 2603 | 5701 | 486 | 158 | 115 | 511 | 100 | 426 | 329 | 198 | 198 | 269 | 826 | 251 | 2546 | 109 | 92 | 81 | 232 | 209 | 112 | 296 | 411 | 6440 |
| number of parts | 12200 | 28958 | 1571 | 358 | 2420 | 1432 | 207 | 1151 | 1174 | 838 | 585 | 1193 | 4025 | 588 | 34564 | 5587 | 270 | 346 | 291 | 947 | 394 | 2565 | 1013 | 40879 |
| maximum parts per shape | 122 | 47 | 5 | 4 | 59 | 5 | 3 | 8 | 5 | 8 | 9 | 8 | 18 | 3 | 100 | 63 | 3 | 8 | 4 | 11 | 5 | 43 | 8 | 30 |
| minimum parts per shape | 2 | 2 | 2 | 2 | 4 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 13 | 2 | 3 | 2 | 2 | 2 | 2 | 2 | 2 |

***Table 1. Specific information of our dataset.***


### Explanation with an Example

We use a chair as an example to illustrate how our data is organized. We first show a figure to illustrate how to represent a part-based model with a symmetry hierarchy. We then explain the details of data organization.

#### 1. Symmetry hierarchy
![image](https://github.com/PeppaZhu/PartNet_Dataset/blob/master/pictures/picture15.png) 
***Figure 1. A chair model is represented with a recursive symmetry hierarchy.***

As shown in ***Figure 1***, a chair model is represented with a recursive symmetry hierarchy. Each leaf node represents a part. There are three types of nodes in the hierarchy: Type 0 -- Leaf nodes (e.g. **node 7**), Type 1 -- Adjacency nodes (e.g. ***node 14***, indicating the proximity relations between two adjacent parts), and Type 2 -- Symmetry nodes (e.g. ***node 9***, which represents either a reflectional or a rotational symmetry relations of multiple parts). A symmetry node stores the parameters (e.g., reflection axis) of the corresponding symmetry. Please see [Wang et al. 2011] and [Li et al. 2017] for more detailed definition of symmetry hierarchy. 

#### 2. Data organization

There are seven folders in each of our data models. 

##### A. the ops folder
Each mat file in the ops folder stores a corresponding type of the node of a partnet tree, as shown in ***Table 2*** for the corresponding type of the node in ***Figure 1 (b)***.(0 for leaf nodes, 1 for adjacent nodes and 2 for symmetric nodes).

|  node ordinal number  | *node 7*  | *node 2* | *node 12*    |  *node 3*   | *node 13*  | *node 14*  | *node 15* | *node 6* | *node 4* | *node 9* | *node 5* | *node 1* | *node 8* | *node 10* | *node 11* | *node 16* | *node 17* |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- |---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| node type | 0 | 0 | 2 | 0 | 2 | 1 | 1 | 0 | 0 | 2 | 0 | 0 | 2 | 1 | 1 | 1 | 1 |

***Table 2. Node type.***


##### B. the part_fix folder
The mat file under the part_fix folder stores the box index corresponding to the leaf node of a model. 

##### C. the boxes folder
The mat file under the boxes folder stores the box corresponding to each leaf node of a model.

##### D. the labels folder
The mat file under the labels folder corresponds to the type identification of each leaf node. As shown in ***Table 3***,***node 7*** represents the back of the chair (labeled by number 0),***node 6*** represents the chair cushion (labeled by number 1),***node 1***,***node 4*** and ***node 5*** represent legs (labeled by number 2),and ***node 2*** and ***node 3*** represents  armrest of the chair (labeled by number 3).  

|  node ordinal number  |  *node 7*   | *node 2* | *node 3*    | *node 6*    |  *node 4*    | *node 5*   | *node 1*    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| node label | 0 | 3 | 3 | 1 | 2 | 2 | 2 |

***Table 3. Node label.***


##### E. the syms folder
The mat file under the syms folder stores symmetrical parameters of each symmetrical node. In this example, there are four sets of symmetrical relationships, so four symmetrical parameters are stored. In partnet tree, corresponding to ***node 12***, ***node 13***, ***node 9*** and ***node 8*** in turn.

##### F. the models folder & the obbs folder
The models folder stores models in .obj form. The obbs folder stores the corresponding obb files for each model.

### Accessing to the dataset
You could get the dataset [Here](https://www.dropbox.com/sh/o04yue60joxwkml/AACS0HmBybSgEruM3C5bmAvJa?dl=0).

### Reference
***[Wang et al. 2011]*** Yanzhen Wang, Kai Xu, Jun Li, Hao Zhang, Ariel Shamir, Ligang Liu, Zhi-Quan Cheng, and Yueshan Xiong, "Symmetry Hierarchy of Man-Made Objects", Computer Graphics Forum (Special Issue of Eurographics 2011), 30(2): 287-296.

***[van Kaick et al. 2013]*** Oliver van Kaick, Kai Xu, Hao Zhang, Yanzhen Wang, Shuyang Sun, Ariel Shamir and Daniel Cohen-Or, "Co-Hierarchical Analysis of Shape Structures", ACM Transactions on Graphics (SIGGRAPH 2013), 32(4).

***[Li et al. 2017]*** Jun Li, Kai Xu, Siddhartha Chaudhuri, Ersin Yumer, Hao Zhang and Leonidas Guibas, "GRASS: Generative Recursive Autoencoders for Shape Structures", ACM Transactions on Graphics (SIGGRAPH 2017), 36(4).

## Citation
If you use this dataset, please cite the following papers.
```
@InProceedings{Yu_2019_CVPR,
    title = {{PartNet}: A Recursive Part Decomposition Network for Fine-grained and Hierarchical Shape Segmentation},
    author = {Fenggen Yu and Kun Liu and Yan Zhang and Chenyang Zhu and Kai Xu},
    booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    pages = {to appear},
    month = {June},
    year = {2019}
}
```

```
@InProceedings{Mo_2019_CVPR,
    author = {Mo, Kaichun and Zhu, Shilin and Chang, Angel X. and Yi, Li and Tripathi, Subarna and Guibas, Leonidas J. and Su, Hao},
    title = {{PartNet}: A Large-Scale Benchmark for Fine-Grained and Hierarchical Part-Level {3D} Object Understanding},
    booktitle = {The IEEE Conference on Computer Vision and Pattern Recognition (CVPR)},
    month = {June},
    year = {2019}
}
```
