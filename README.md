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
## Show programming language
```python
import os
os.chdir()
```
