# NVIDIA_TrashDetect
## About The Project
This project uses a Jetson Nano to detect and classify waste. The system is built using **[PyTorch](https://github.com/pytorch/pytorch)** and **[Jetson Inference](https://github.com/dusty-nv/jetson-inference)**, and it can recognize different types of waste, such as plastic bottles, cans, and paper. In the future the system can be used in various settings, such as homes, offices, and public places, to promote recycling and reduce waste.



 
## Getting Started

### Prerequisites

 - Make sure you have set up the Jetson Nano correctly
 - You have installed the Jetson Nano Inference, for more information click: [here](https://github.com/dusty-nv/jetson-inference/blob/master/docs/jetpack-setup-2.md)

### Installation 

 1. add GarbageDetectionModel.onnx  & labels.txt to `jetson-inference/python/training/detection/ssd/models/`
 2. install unzip: `sudo apt install unzip`
 3.  add the GarbageDetection.zip to your home directory and run: 
 `unzip GarbageDetection.zip -d jetson inference/python/training/detection/ssd/data/`


 ## Usage
 ### Run the Model
to get to the detection directory run : `cd jetson-inference/python/training/detection/ssd` 

 to try the model with an image run:
 
    detectnet.py --model=models/GarbageDetectionModel.onnx --input_blob=input_0 --output-cvg=scores --output-bbox=boxes --labels=models/labels.txt input_image.jpg output_image.jpg`

to try the model with a camera run:
    `detectnet.py --model=models/GarbageDetectionModel.onnx --input_blob=input_0 --output-cvg=scores --output-bbox=boxes --labels=models/labels.txt /dev/video0 output_video.mp4`

 - Use `/dev/video0` for an USB camera
 - Use `csi://0`for a Serial camera

### Train the model

 1. run `cd jetson-inference/`
 2. go into the docker `./docker/run.sh`
 3. inside the Docker container, change directories to `cd jetson-inference/python/training/classification`
 4. run `python3 train_ssd.py --dataset-type=voc --data=data/GarbageDetection --model-dir=models/<YOUR-MODEL>`
 5. run this to export your model: `python3 onnx_export.py --model-dir=models/<YOUR-MODEL>`

> **note:** if you run out of memory or your process is "killed" during training, try [Mounting SWAP](https://github.com/dusty-nv/jetson-inference/blob/master/docs/pytorch-transfer-learning.md#mounting-swap) and [Disabling the Desktop GUI](https://github.com/dusty-nv/jetson-inference/blob/master/docs/pytorch-transfer-learning.md#disabling-the-desktop-gui).  
to save memory, you can also reduce the `--batch-size` (default 4) and `--workers` (default 2)

    

  





 
