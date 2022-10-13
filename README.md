# Big5-Project

## Data
### First Impressions Data (2017) :

https://chalearnlap.cvc.uab.cat/dataset/24/description/

* train-1~6.zip
* val-1~2.zip
* test-1~2.zip
* gt : 'extraversion', 'neuroticism', 'agreeableness', 'conscientiousness', 'openness'

each zip folder contains about 960 clips, clips length = 15s

---
### Google Drive Data Description

* Preprocessed data
  * **data_v1**: 6 random frame per video, frame size 128
    * trian_set.dat (train-1.zip)(734)
    * valid_set.dat (val-1.zip)(764)
    * test_set.dat (test-1~2.zip)(1845)
  * **data_v2**: 6 random frame per video, frame size 128
    * train_set.dat(train-2~6.zip)(4300)
  * **data_v3**: 6 random frame per video, frame size 128, try not drop any videos
    * train_set.dat(train-2~6.zip)(5034)
    * valid_set.dat (val-1.zip)(960)
    * valid_set_2.dat (val-2.zip)(960)
    * test_set.dat (test-1~2.zip)(1998)
* Train
  * train: all videos in train-1.zip (960)
  * train13: all videos in train-2~6.zip (5040)
  * train_6000: all videos in trainset (6000)
* Valid
  * valid: all videos in val-1.zip (960)
  * valid_2: all videos in val-2.zip (960)
  * valid_small: few vidoes from val-1.zip (960)
* Test
  * test: all videos in testset (2000)
  
---
## Main
* big5.ipynb
  * regression
  * criterion: accuracy=1-MAE
* big5_classification.ipynb
  * classification
  * criterion: accuracy, precision, recall
---
## Code Cell Description

* extract folder
  * only for extracting folders in Drive
* Packages*
  * remember to rerun if colab shut down
* Configuration*
  * settings for model, training, preprocess data...
  * define root directory
  * define checkpoint & logs name: date, note
* Helper
  * functions to detect face, extract audio and frames
  * import dlib
* Build New Dataset
  * use functions in helper to build traian, valid, test dataset
  * list of tuples save as .dat
  * ***never run it if you are using .dat***
* Dataloader*
  * pytorch Dataset for latter use
    * dim: input channel, default = 1 
  * return 
  ```ruby
      sample = {'images': images,             # size: N frames, H, W
                'label': float(class_label),  # 0. or 1.  
                'audio': audio,               # None now
                'uid': uid,                   # video name
                'value': org_value}           # origin annotation value 
                                              # in big5.ipynb, 'label' is original 5 value
  ```
  * augmentation (horizon flip)
* Load data
  * read .dat 
  * data structure in .dat
  ``` ruby
  list[
    # np arrays: preprocessed images, ground truth big 5
    sample1 tuple(array[(6*128*128)], array[(5)]),
    sample2 tuple(array[(6*128*128)], array[(5)]),
    sample3 ...
    ...
  ]  
  ```
  * in classification.ipynb, find Q40 & Q60 to filter 20% data in the center
  * no need to filter them in regression
* Model*
  * model classes and helper function
  * CNN block
  * resnet 
  * it is OK to run all of them
  * model input: ***Batch size, Channel(1 for gray scale), Depth(N frame), H, W***
* Build model
  * only choose one of the model to build
    * CNN Block
    * Resnet
    * Pretrain
  * Then run Optimizer & Checkpoint 
* Train Helper*
  * loss function 
  * train & valid module: input batches into model
* Train
  * Tensorboard for monitoring the training process, may need to wait a bit for it to show up
  * main: do serveral time of training & validing (epoch)
* Test
  * Run cells with * before testing: Packages, Config, Dataloader, Model, Train Helper 
  * Then build test dataloader and model to inference

---

## Resource
Code Source: https://github.com/grimmdaniel/personality-trait-prediction

Competition: [Chalearn 2017 Looking at People CVPR/IJCNN Competition](https://chalearnlap.cvc.uab.cat/challenge/23/description/)

Leaderboard(Results), Evaluation Criterion: [Platform](https://competitions.codalab.org/competitions/15975#learn_the_details-evaluation)
