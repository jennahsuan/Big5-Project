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
* Train
  * train: all videos in train-1.zip (960)
  * train13: all videos in train-2~6.zip (5040)
  * train_6000: all videos in trainset (6000)
* Valid
  * valid: all videos in val-1.zip (960)
  * valid_small: few vidoes from val-1.zip (960)
* Test
  * test: all videos in testset (2000)
  
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
* Dataloader
  * read .dat
  * data structure
  ```
  list[
    np arrays: preprocessed images, ground truth big 5
    sample1 tuple(array[(6*128*128)], array[(5)]),
    sample2 tuple(array[(6*128*128)], array[(5)]),
    sample3 ...
  ]  
  ```
