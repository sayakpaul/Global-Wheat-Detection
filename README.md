# Global-Wheat-Detection
Showcases the use of deep learning to detect wheat heads from crops. The project is based on this Kaggle Competition: https://www.kaggle.com/c/global-wheat-detection.

**Here's a description of the prediction task**:

In this competition, you’ll detect wheat heads from outdoor images of wheat plants, including wheat datasets from around the globe. Using worldwide data, you will focus on a generalized solution to estimate the number and size of wheat heads. To better gauge the performance for unseen genotypes, environments, and observational conditions, the training dataset covers multiple regions. You will use more than 3,000 images from Europe (France, UK, Switzerland) and North America (Canada). The test data includes about 1,000 images from Australia, Japan, and China.

[- Source](https://www.kaggle.com/c/global-wheat-detection)

## Data
An overview is available here: https://www.kaggle.com/c/global-wheat-detection/data. 

The dataset includes images that either have wheat heads or do not have them. Here are some examples:

![](https://i.ibb.co/0cFMfFw/download.png)

(The following ones **do not** have any wheat heads)

![](https://i.ibb.co/FHLNgwj/download-1.png)

I used the following command to obtain the data:
```
$ kaggle competitions download -c global-wheat-detection
```

This is an object detection task and the project uses [TensorFlow Object Detection (TFOD) API ](https://github.com/tensorflow/models/tree/master/research/object_detection).

## About the files & directories
```
├── faster_rcnn_resnet101_coco_11_06_2017: Contains the pre-trained checkpoints and frozen inference graph.
│   ├── saved_model
│   │   ├── variables
│   │   └── saved_model.pb
│   ├── checkpoint
│   ├── frozen_inference_graph.pb
│   ├── model.ckpt.data-00000-of-00001
│   ├── model.ckpt.index
│   ├── model.ckpt.meta
│   └── pipeline.config
├── test: Contains the test images of the competition. 
│   ├── 2fd875eaa.jpg
│   ├── 348a992bb.jpg
│   ├── 51b3e36ab.jpg
│   ├── 51f1be19e.jpg
│   ├── 53f253011.jpg
│   ├── 796707dd7.jpg
│   ├── aac893a91.jpg
│   ├── cb8d261a3.jpg
│   ├── cc3532ff6.jpg
│   └── f5a1f0358.jpg
├── train: Contains the training images of the competition. 
├── Basic_EDA.ipynb: Performs basic data visualization on the provided dataset.
├── Data_Prep.ipynb: Prepares the data in a TFOD API compatible format.
├── faster_rcnn_resnet101_pets.config: Training configuration file.
├── generate_tfrecord.py: Utility script for generating TFRecords from `.csv` files.
├── label_map.pbtxt: Label map file.
├── new_train_df.csv: The newly created partial training set.
├── train.csv: Comes with the initial dataset & contain information about the bounding boxes. 
├── train_df.csv: Expanded version of the initial `train.csv` file. 
├── train.record: TFRecord file of the partial training set. 
├── valid_df.csv: The newly created validation set.
└── valid.record: TFRecord file of the validation set.
```

**Note** 

The files that you don't see here in the directory were not intentionally provided because of their sizes. 

## Results

Following are the results I got from TensorBoard while my model was training (following are images from the validation set I prepared):

![](https://i.ibb.co/8Y3fXHF/Screen-Shot-2020-05-06-at-11-17-36-PM.png)

![](https://i.ibb.co/4V4B4ZQ/Screen-Shot-2020-05-06-at-11-18-03-PM.png)

## Steps to reproduce the results
- Follow the instructions from `Data_Prep.ipynb` notebook. 
- Once the new training and validation splits are generated run `generate_tfrecord.py` script for generating the TFRecords. 
- Download the pre-trained checkpoints of Faster RCNN with Inception Network as base by running:
  ```
  wget http://download.tensorflow.org/models/object_detection/faster_rcnn_resnet101_coco_2018_01_28.tar.gz
  ```
- Follow instructions from [this piece](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_pets.md) on how to package an object detection application in TensorFlow Object Detection API and submit a training job to AI Platform. It also shows how to monitor performance with TensorBoard and export the trained model checkpoints as a frozen inference graph. 

This project uses GCS buckets for storing intermediate training checkpoints along with all the other files necessary to run a TFOD API model on AI Platform. Following are the initial files from my GCS bucket:
```
$ gsutil ls gs://global_wd_faster_rcnn/data
gs://global_wheat_detection/data/label_map.pbtxt
gs://global_wheat_detection/data/model.ckpt.data-00000-of-00001
gs://global_wheat_detection/data/model.ckpt.index
gs://global_wheat_detection/data/model.ckpt.meta
gs://global_wheat_detection/data/faster_rcnn_resnet101_pets.config
gs://global_wheat_detection/data/train.record
gs://global_wheat_detection/data/valid.record
```

## Acknowledgement
- ML-GDE program for granting me GCP credits.

The project extensively uses GCP's AI offerings such as AI Platform. Specifically, I used AI Platform Notebooks and AI Platform Jobs. For storage, I used GCS buckets. 
