# Commands 
## download gitignore using curl 
```bash
curl https://raw.githubusercontent.com/c17hawke/general_template/main/.gitignore > .gitignore
```
## Download init_set.sh using curl
```bash
curl https://raw.githubusercontent.com/c17hawke/general_template/main/init_setup.sh > init_setup.sh
```
## Tensorflow verification
```bash  
python -c "import tensorflow as tf;print(tf.config.list_physical_devices('GPU'))"
```
## Installation of Object Detection API

## Create a Tensorflow directory
```bash 
mkdir TensorFlow && cd TensorFlow
```
## Clone the TensorFlow model 
```bash 
git clone https://github.com/tensorflow/models.git
```
remove .git directory of models repository to avoid git conflicts and model folder to .gitignore 
```bash
echo "TensorFlow/models" >> .gitignore
## Run programming language
```python
import os
os.chdir()
```
## Protobuff Installation/Compilation 
```bash
visit the links -  https://github.com/protocolbuffers/protobuf/releases
   - windows user - search for - protoc-3.20.1-win64.zip
   - for mac users - search for - protoc-3.20.1-osx-x86_64.zip
   - for linux users -
        sudo apt install -y protobuf-compiler
Unzip into root folder and add <PATH TO protoc folder>/bin into sytstem environment variable
run the following command:
cd TensorFlow/models/research
protoc object_detection/protos/*.proto --python_out=.
```
## Install COCO API   
```bash 
pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
```
## Install Object Detection API  
```bash 
cp object_detection/packages/tf2/setup.py .
python -m pip install .
```
## Test your installation -
```bash 
python object_detection/builders/model_builder_tf2_test.py
```
## Run example -  
- Create workspace/example_1 directory in project root
```bash
mkdir -p workspace/example_1
```
- cd to workspace/example_1
  ```bash
  cd workspace/example_1
  ```
- Download notebook 
   ```bash
   curl https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/2.2.0/_downloads/7f6123c070712ed53dd2521219dd011c/plot_object_detection_simple.ipynb > plot_object_detection_simple.ipynb 
   ```

## Custom model tranings 
```bash
mkdir workspace/training_demo
cd workspace/training_demo
mkdir -p annotations exported-models models pre-trained-models images/test images/train
```

## Create label map file in training_demo/annotations
and write content as -
```bash
item{
    id:1
    name:'helmet'
}
item{
    id:2
    name:'head'
}
item{
    id:3
    name:'person'
}
```
## curl the generate_tfrecord file into root of training_demo directory
```bash
curl https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/_downloads/da4babe668a8afb093cc7776d7e630f3/generate_tfrecord.py > generate_tfrecord.py
```
## generate tfrecord
### for train dataset
```bash
python generate_tfrecord.py -x images/train -l annotations/label_map.pbtxt -o annotations/train.record
```
### for test datasets
```bash
python generate_tfrecord.py -x images/test -l annotations/label_map.pbtxt -o annotations/test.record
```
# Configuring a training job 

## Go to [model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf2_detection_zoo.md) and download [SSD ResNet50 V1 FPN 640x640 (RetinaNet50)](http://download.tensorflow.org/models/object_detection/tf2/20200711/ssd_resnet50_v1_fpn_640x640_coco17_tpu-8.tar.gz) model 
- extract the download model into training_demo/pre-trained-model directory

## Configure training pipeline  
- create a folder my_ssd_resnet50_v1_fpn in training_demo/models folder
- copy pipeline.config here from pre-trained-model directory
- update it as the documentation - [link](https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest/training.html#preparing-the-workspace)

# Copy training file from TensorFlow/models/research/object_detection/ to the root of training_demo folder  
```bash
cp ../../TensorFlow/models/research/object_detection/model_main_tf2.py .
```
## start training by running the following command -
```bash
python model_main_tf2.py --model_dir=models/my_ssd_resnet50_v1_fpn --pipeline_config_path=models/my_ssd_resnet50_v1_fpn/pipeline.config
```
## Exporting a Trained Model 
```bash 
cp ../../TensorFlow/models/research/object_detection/exporter_main_v2.py .

python exporter_main_v2.py --input_type image_tensor --pipeline_config_path ./models/my_ssd_resnet50_v1_fpn/pipeline.config --trained_checkpoint_dir ./models/my_ssd_resnet50_v1_fpn/ --output_directory ./exported-models/my_model
```
