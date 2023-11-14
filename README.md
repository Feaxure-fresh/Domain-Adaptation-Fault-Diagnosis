# Transfer Learning for Fault Diagnosis

## Overview
Welcome to our repository dedicated to advancing the field of cross-domain fault diagnosis through transfer learning. Our focus lies in Single-source Unsupervised Domain Adaptation (SUDA) and Multi-source Unsupervised Domain Adaptation (MUDA), offering a rich collection of resources and methodologies.

## Featured Methods
Our repository includes a diverse range of state-of-the-art methods, each accompanied by relevant publications and direct access to implementation code in `models`. Highlights include:

- **ACDANN** - Integrating expert knowledge with domain adaptation for unsupervised fault diagnosis. [Published in TIM 2021](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9612159) | [View Code](/models/ACDANN.py)
- **ADACL** - Adversarial domain adaptation with classifier alignment for cross-domain intelligent fault diagnosis of multiple source domains. [Published in Measurement Science and Technology 2020](https://iopscience.iop.org/article/10.1088/1361-6501/abcad4/pdf) | [View Code](/models/ADACL.py)
- **BSP** - Transferability vs. discriminability: Batch spectral penalization for adversarial domain adaptation. [Published in ICML 2019](http://proceedings.mlr.press/v97/chen19i/chen19i.pdf) | [View Code](/models/BSP.py) 
- **CDAN** - Conditional adversarial domain adaptation. [Published in NIPS 2018](http://papers.nips.cc/paper/7436-conditional-adversarial-domain-adaptation) | [View Code](/models/CDAN.py) 
- **CORAL** - Deep coral: Correlation alignment for deep domain adaptation. [Published in ECCV 2016](https://arxiv.org/abs/1607.01719) | [View Code](/models/CORAL.py)
- **DAN** - Learning transferable features with deep adaptation networks. [Published in ICML 2015](http://ise.thss.tsinghua.edu.cn/~mlong/doc/deep-adaptation-networks-icml15.pdf) | [View Code](/models/DAN.py)
- **DANN** - Unsupervised domain adaptation by backpropagation. [Published in ICML 2015](http://proceedings.mlr.press/v37/ganin15.pdf) | [View Code](/models/DANN.py)
- **IRM** - Invariant risk minimization. [Published in ArXiv](https://arxiv.org/abs/1907.02893) | [View Code](/models/IRM.py)
- **MCD** - Maximum classifier discrepancy for unsupervised domain adaptation. [Published in CVPR 2018](http://openaccess.thecvf.com/content_cvpr_2018/papers/Saito_Maximum_Classifier_Discrepancy_CVPR_2018_paper.pdf) | [View Code](/models/MCD.py)
- **MDD** - Bridging theory and algorithm for domain adaptation. [Published in ICML 2019](http://proceedings.mlr.press/v97/zhang19i/zhang19i.pdf) | [View Code](/models/MDD.py)
- **MFSAN** - Aligning domain-specific distribution and classifier for cross-domain classification from multiple sources. [Published in AAAI 2019](https://ojs.aaai.org/index.php/AAAI/article/view/4551) | [View Code](/models/MFSAN.py) 
- **MSSA** - A multi-source information transfer learning method with subdomain adaptation for cross-domain fault diagnosis. [Published in Knowledge-Based Systems 2022](https://reader.elsevier.com/reader/sd/pii/S0950705122001927?token=03BD384CA5D6E0E7E029B23C739C629913DE8F8BB37F6331F7D233FB6C57599BFFC86609EE63BE2F9FC43871D96A2F61&originRegion=us-east-1&originCreation=20230324021230) | [View Code](/models/MSSA.py)
- **MixStyle** - Domain generalization with mixstyle. [Published in ICLR 2021](https://arxiv.org/abs/2104.02008) | [View Code](/models/MixStyle.py)

## Getting Started
### Requirements
Our code runs fine with the following prerequisites:
*  Python 3 (>=3.8)
*  Pytorch (>=1.10)
*  Numpy (>=1.21.2)
*  Pandas (>=1.5.3)
*  tqdm (>=4.46.1)
*  Scipy (>=1.10)

### Repository Access
You can access our repository either by direct download or using git clone. Here’s how:
#### Direct Download
1. Click on the 'Code' button and select 'Download ZIP'.
2. Extract the ZIP file to your desired location.
#### Using Git Clone
1. Open your command line interface.
2. Navigate to the directory where you wish to clone the repository.
3. Run the command: `git clone https://github.com/your-repository-link.git`


### Accessing Datasets
Our repository supports several public datasets for fault diagnosis, with accompanying loading code. These include:
- **[CWRU](https://engineering.case.edu/bearingdatacenter)** - Case Western Reserve University dataset.
- **[MFPT](https://www.mfpt.org/fault-data-sets)** - Machinery Failure Prevention Technology dataset.
- **[PU](https://mb.uni-paderborn.de/kat/forschung/datacenter/bearing-datacenter)** - Paderborn University dataset.
- **[XJTU](https://biaowang.tech/xjtu-sy-bearing-datasets)** - Xi’an Jiaotong University dataset.
- **[IMS](https://www.kaggle.com/datasets/vinayak123tyagi/bearing-dataset?resource=download)** - Intelligent Maintenance Systems dataset.

### Within-dataset transfer
According to different operation conditions, divide a specific dataset into folders like "op_0", "op_1" and so on. In each "op_?" folder, use subfolders for different categories, which contain the fault data.

For example, CWRU dataset can be divided into 4 folders according to 4 motor speed. In each folder, data of this operation condition can be classified into 9 fault classes, such as 7 mil Inner Race fault, 14 mil Inner Race fault, 7 mil Outer Race fault and so on (referring to [this article](https://ieeexplore.ieee.org/abstract/document/9399341)). Then, the dataset folder is organized as
```
.
└── dataset
    └── CWRU
        ├── op_0
        │   ├── ball_07
        │   │   └── 122.mat
        │   ├── inner_07
        │   │   └── 109.mat
        │   ...
        ├── op_1
        │   ├── ball_07
        │   │   └── 123.mat
        │   ...
        ├── op_2
        ...
```

### Cross-dataset transfer
You can also try to implement transfer among different datasets. In this case, the categories of faults contained in each dataset must be the same.

For example, organize CWRU and MFPT datasets as follows for one-to-one transfer.
```
.
└── dataset
    ├── CWRU
    │   ├── inner
    |   |    ├── ***.mat
    |   |    |   ***.mat
    |   |    ...
    │   ├── normal
    │   └── outer
    └── MFPT
        ├── inner
        ├── normal
        └── outer
```
Note: It is highly recommended to modify the dataset loading code based on custom training. Make sure that `datasetname` in the loading code is consistent with names of your subfolders. The sampling length can also be changed by adjusting the `signal_size` inside.

## Usage
### Load trained weights
```shell
python train.py --model_name CNN --load_path ./CNN/single_source/model.pth --target_name CWRU_3 --num_classes 9 --cuda_device 0
```
### Within-dataset transfer
One-to-one transfer (such as CWRU operation condition 0 to condition 1).
```shell
python train.py --model_name CNN --source_name CWRU_0 --target_name CWRU_1 --train_mode single_source --num_classes 9 --cuda_device 0
``` 
Many-to-one transfer. 
```shell
python train.py --model_name MFSAN --source_name CWRU_0,CWRU_1 --target_name CWRU_2 --train_mode multi_source --num_classes 9 --cuda_device 0
``` 
### Cross-dataset transfer
One-to-one transfer.
```shell
python train.py --model_name CNN --source_name CWRU --target_name MFPT --train_mode single_source --num_classes 3 --cuda_device 0
``` 
Many-to-one transfer. 
```shell
python train.py --model_name MFSAN --source_name CWRU,PU --target_name MFPT --train_mode multi_source --num_classes 3 --cuda_device 0
``` 

## Contact
If you have any problem with our code or have some suggestions, feel free to contact Jinyuan Zhang (feaxure@outlook.com) or describe it in Issues.

## Citation
If you use this toolbox or benchmark in your research, please cite this project. 
```latex
@misc{dafd,
    author = {Jinyuan Zhang},
    title = {TL-Bearing-Fault-Diagnosis},
    year = {2022},
    publisher = {GitHub},
    journal = {GitHub repository},
    howpublished = {\url{https://github.com/Feaxure-fresh/TL-Bearing-Fault-Diagnosis}},
}
```

