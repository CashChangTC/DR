# DR

### Train

- Convert data to tfrecord
```
$ DATASET_DIR=your quality dataset path (/home/.../data/mobilenet_blur_20170830)

$ python download_and_convert_data.py \
      --dataset_name=quality \
      --dataset_dir="${DATASET_DIR}"
```
  
- Training    

``` 
$ TRAIN_DIR=path to save trained model (/home/.../models/trained)
$ DATASET_DIR=your quality dataset path (/home/.../data/mobilenet_blur_20170830)
$ CHECKPOINT_PATH=path to load pre-trained model (/home/.../models/pre-trained/mobilenet_v1_1.0_224.ckpt)

$ python train_image_classifier.py \  
      --train_dir=${TRAIN_DIR} \   
      --dataset_dir=${DATASET_DIR} \  
      --dataset_name=quality \  
      --dataset_split=train \  
      --model_name=mobilenet_v1 \  
      --max_models_to_keep=100 \  
      --checkpoint_path=${CHECKPOINT_PATH} \  
      --checkpoint_exclude_scopes=MobilenetV1/Logits
```

### Test

- Evaluation

```
$ DATASET_DIR=your quality dataset path (/home/.../data/mobilenet_blur_20170830)
$ CHECKPOINT_PATH=path to load pre-trained model (/home/.../models/trained/model.ckpt-10339)

$ python eval_image_classifier.py \
      --checkpoint_path=${CHECKPOINT_PATH} \
      --dataset_dir=${DATASET_DIR} \
      --dataset_name=quality \
      --dataset_split_name=test \
      --model_name=mobilenet_v1
```
