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
