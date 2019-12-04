### Cloneing repository
$ git clone https://github.com/mattwells19/USRoadSignRecognition
$ cd PyTorch-YOLOv3/
$ sudo pip3 install -r requirements.txt



### Downlading pretrained weights for training
$ cd weights/
$ bash download_weights.sh



### Training model
***you will need to download the pretrained weights to use the --pretrained_weights with darknet53.comv.74***
$ python3 train.py --model_def config/yolov3-custom.cfg --data_config config/custom.data --pretrained_weights weights/darknet53.conv.74 --epochs=50 --checkpoint_interval=5 --evaluation_interval=5



### Detecting Signs
***--weights_path will need to be updated to the location of the new checkpoint after you train***
$ python3 detect.py --weights_path checkpoints/yolov3_ckpt_45.pth --class_path data/custom/classes.names --image_folder data/custom/detect/renamed/ --model_def config/yolov3-custom.cfg --conf_thres=0.9 --nms_thres=0.1



