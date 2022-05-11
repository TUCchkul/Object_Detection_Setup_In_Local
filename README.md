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