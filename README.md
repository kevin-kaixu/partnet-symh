# PartNet_Dataset

We organize the dataset of PartNet(A Large-scale Benchmark for Fine-grained and Hierarchical Part-level 3D Object Understanding) into the form of our PartNet(A Recursive Part Decomposition Network for Fine-grained and Hierarchical Shape Segmentation) dataset，which uses a top-down recursive hierarchy tree to represent a model.

### Introduction

This dataset is derived from the dataset of the paper published by Stanford University called PartNet(A Large-scale Benchmark for Fine-grained and Hierarchical Part-level 3D Object Understanding),which consists of 24 object categories.Models of their dataset are fine-grained but lack of a top-down recursive hierarchy for fine-grained segmentation of 3D point clouds. We organize their dataset into the form of our PartNet dataset for the purpose of giving their models a hierarchy we designed.This dataset could enable and serve as a catalyst for many tasks such as shape analysis, dynamic 3D scene modeling and simulation, affordance analysis, and others.
### Dataset information

The dataset contains 22699 3D shapes covering 24 shape categories:

|  category_name  |  lamp   | table | knife   |  bag   | bed  | bottle   | bowl   | clock   | display   | dishwasher   | door   | earphone   | faucet   | hat   | storage   | keyboard   | laptop   | microwave   | mug   | refrigerator   | scissors   | trashcan   | vase   | chair   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| number of shapes | 2603 | 5701 | 486 | 158 | 115 | 511 | 100 | 426 | 329 | 198 | 198 | 269 | 826 | 251 | 2546 | 109 | 92 | 81 | 232 | 209 | 112 | 296 | 411 | 6440 |
| number of parts | 12200 | 28958 | 1571 | 358 | 2420 | 1432 | 207 | 1151 | 1174 | 838 | 585 | 1193 | 4025 | 588 | 34564 | 5587 | 270 | 346 | 291 | 947 | 394 | 2565 | 1013 | 40879 |
| maximum parts per shape | 122 | 47 | 5 | 4 | 59 | 5 | 3 | 8 | 5 | 8 | 9 | 8 | 18 | 3 | 100 | 63 | 3 | 8 | 4 | 11 | 5 | 43 | 8 | 30 |
| minimum parts per shape | 2 | 2 | 2 | 2 | 4 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 2 | 13 | 2 | 3 | 2 | 2 | 2 | 2 | 2 | 2 |

***Table 1. Specific information of our dataset.***


### Demonstration

We use a chair as an example to illustrate how our data is organized. This chapter is specifically divided into two parts to elaborate the example. In the first part, we will use a figure to illustrate how to represent a model with a partnet tree. In the second part, we will explain the details of each folder.

#### 1. Representing the model with a partnet tree
![image](https://github.com/PeppaZhu/PartNet_Dataset/blob/master/pictures/picture15.png) 
***Figure 1. The chair is represented as a top-down recursive hierarchy tree.***

As shown in ***Figure 1 (a)***, this is an obj model displayed in Deep Exploration, which represents a chair.As shown in ***Figure 1 (b)***, we organize the model into a partnet tree. Each leaf node represents a part. Then we classify a partnet tree node into three categories: 0 for leaf nodes(e.g. ***node 7***), 1 for adjacent nodes (e.g. ***node 14***, whose left child is adjacent to the right child), and 2 for symmetric nodes (e.g. ***node 9***, which is a rotational symmetric node and has only left child.The child is used to preserve a representative part in symmetric relationships.Then other parts in the symmetric relationship can be obtained by storing symmetric parameters).

#### 2. Folder instructions

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
The mat file under the syms folder stores symmetrical parameters of each symmetrical node. In this example, there are four sets of symmetrical relationships, so four symmetrical parameters are stored. In partnet tree, corresponding ***node 12***,***node 13***,***node 9*** and ***node 8*** in turn.

##### F. the models folder & the obbs folder
The models folder stores models in .obj form. The obbs folder stores the corresponding obb files for each model.

### Accessing to the dataset
You could get the dataset [Here](https://www.dropbox.com/sh/o04yue60joxwkml/AACS0HmBybSgEruM3C5bmAvJa?dl=0).

## Citation
If you use this dataset, please cite the following paper.
```
@inproceedings{Yu_2019_CVPR,
    title = {PartNet: A Recursive Part Decomposition Network for Fine-grained and Hierarchical Shape Segmentation},
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
