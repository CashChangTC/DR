# DR

# Image Quality

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
$ CHECKPOINT_PATH=path to load trained model (/home/.../models/trained/model.ckpt-10339)

$ python eval_image_classifier.py \
      --checkpoint_path=${CHECKPOINT_PATH} \
      --dataset_dir=${DATASET_DIR} \
      --dataset_name=quality \
      --dataset_split_name=test \
      --model_name=mobilenet_v1
```
- Classify

List test files' absolute path into the file
```
$ ls -d -1 $PWD/*.* > abspath_file.txt
```

```
$ INPUT_FILE=your test dataset list filename file (/home/.../data/mobilenet_blur_20170830/test/20170830_test_1.txt)
$ OUTPUT_FILE=output predict file (/home/.../data/mobilenet_blur_20170830/test/pred_20170830_test_1.txt)
$ CHECKPOINT_PATH=path to load trained model (/home/.../models/trained/model.ckpt-10339)

$ python classify_image.py \
      --infile=${INPUT_FILE} \
      --outfile=${OUTPUT_FILE} \
      --checkpoint_path=${CHECKPOINT_PATH} \
      --model_name=mobilenet_v1 \
      --preprocessing_name=inception_v3 \
      --num_classes=2 \
      --eval_image_size=32
```
