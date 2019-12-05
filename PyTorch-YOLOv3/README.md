### Cloneing repository
	$ git clone https://github.com/mattwells19/USRoadSignRecognition
	$ cd PyTorch-YOLOv3/
	$ sudo pip3 install -r requirements.txt



### Downlading pretrained weights for training
	$ cd weights/
	$ bash download_weights.sh



### Training model
	$ python3 train.py --model_def config/yolov3-custom.cfg --data_config config/custom.data --pretrained_weights weights/darknet53.conv.74 --epochs=50 --checkpoint_interval=5 --evaluation_interval=5
***you will need to download the pretrained weights to use the --pretrained_weights with darknet53.comv.74***



### Detecting Signs
	$ python3 detect.py --weights_path checkpoints/yolov3_ckpt_45.pth --class_path data/custom/classes.names --image_folder data/custom/detect/renamed/ --model_def config/yolov3-custom.cfg --conf_thres=0.9 --nms_thres=0.1
***--weights_path will need to be updated to the location of the new checkpoint after you train***



### Training on Custom Dataset / Data and label setup

#### Custom model
Run the commands below to create a custom model definition, replacing `<num-classes>` with the number of classes in your dataset.
	$ cd config/                                # Navigate to config dir
	$ bash create_custom_model.sh <num-classes> # Will create custom model 'yolov3-custom.cfg'

#### Classes
Add class names to `data/custom/classes.names`. This file should have one row per class name.

#### Image Folder
Move the images of your dataset to `data/custom/images/`.

#### Annotation Folder
Move your annotations to `data/custom/labels/`. The dataloader expects that the annotation file corresponding to the image `data/custom/images/train.jpg` has the path `data/custom/labels/train.txt`. Each row in the annotation file should define one bounding box, using the syntax `label_idx x_center y_center width height`. The coordinates should be scaled `[0, 1]`, and the `label_idx` should be zero-indexed and correspond to the row number of the class name in `data/custom/classes.names`.

#### Define Train and Validation Sets
In `data/custom/train.txt` and `data/custom/valid.txt`, add paths to images that will be used as train and validation data respectively.

#### Train
To train on the custom dataset run:
	$ python3 train.py --model_def config/yolov3-custom.cfg --data_config config/custom.data

Add `--pretrained_weights weights/darknet53.conv.74` to train using a backend pretrained on ImageNet.
