# DR

### Training

1. Convert data to tfrecord
```
$ DATA_DIR=your quality dataset path. (/raid.../ex.../D.../Cash/quality)

$ python download_and_convert_data.py \
      --dataset_name=quality \
      --dataset_dir="${DATA_DIR}"
```
  
  
2. Training
``` 
$ DATASET_DIR=your quality dataset path (/raid.../ex.../D.../Cash/quality)
$ TRAIN_DIR=path to save trained model
$ CHECKPOINT_PATH=path to load pre-trained model

$ python train_image_classifier.py   
      --train_dir=/home/cash/DR/imageQuality/models/trained_blur_20170904/ \   
      --dataset_dir=/home/cash/DR/imageQuality/data/mobilenet_blur_20170830/ \  
      --dataset_name=quality \  
      --dataset_split=train \  
      --model_name=mobilenet_v1 \  
      --max_models_to_keep=100 \  
      --checkpoint_path=/home/cash/DR/imageQuality/models/pre-trained/mobilenet_v1_1.0_224.ckpt \  
      --checkpoint_exclude_scopes=MobilenetV1/Logits
```
