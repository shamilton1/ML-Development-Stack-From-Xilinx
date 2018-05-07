# Object Detection Tutorial

## Introduction
You only look once (YOLO) is a state-of-the-art, real-time object detection algorithm.  
The algorithm was published by Redmon et al. in 2016 via the following publications:
[YOLOv1](https://arxiv.org/abs/1506.02640),
[YOLOv2](https://arxiv.org/abs/1612.08242).  
This application requires more than just simple classification. The task here is to detect the presence of objects, and localize them within a frame. Please refer to the papers for full algorithm details, and/or watch [this.](https://www.youtube.com/watch?v=9s_FpMpdYW8). In this tutorial, the network was trained on the 80 class [COCO dataset.](http://cocodataset.org/#home)

## Background
The authors of the YOLO papers used their own programming framework called "Darknet" for research, and development. The framework is written in C, and was [open sourced.](https://github.com/pjreddie/darknet) Additionally, they host documentation, and pretrained weights [here.](https://pjreddie.com/darknet/yolov2/) Currently, the Darknet framework is not supported by Xilinx's ML Suite. Additionally, there are some aspects of the YOLOv2 network that are not supported by the Hardware Accelerator, such as the leaky ReLU activation function. For these reasons the network was modified, retrained, and converted to caffe. In this tutorial we will run the network accelerated on an FPGA using 16b quantized weights and a hardware kernel implementing a 56x32 systolic array with 5MB of image RAM. All convolutions/pools are accelerated on the FPGA fabric, while the final sigmoid, softmax, and non-max suppression functions are executed on the CPU.

### Network Modifications
* Leaky ReLU replaced by ReLU
* "reorg" layer a.k.a. "space_to_depth" layer replaced by MAX POOL

## Running the Network
This demo was provided as part of the 18.04.02 AMI release.

For instructions on launching and connecting to aws instances, see [here][].

1. Connect to F1  

2. Navigate to `/home/centos/xfdnn_18_04_02/pyxdnn/examples/yolov2/python`

3. Execute `sudo ./run_xdnn.sh` to run images in the DemoImages directory through the YOLOv2 network

```
    # You will see a series of prints for each image indicating:
    #   1. The objects detected in the image
    #   2. The score or confidence of the classification for each object
    #   3. The coordinates of bounding boxes for each object (Two coordinates pairs given: lower-left, upper-right)
    #      Recall that the origin (0,0) is given as the upper left corner of the image.
    # Additionally, the demo will display each image with bounding boxes drawn
    # This is accomplished using PIL, OpenCV, and X11 forwarding to your local display
    # Press enter to cycle through images
    
    
[centos@ip-172-31-29-35 python]$ sudo ./run_xdnn.sh 
=============== pyXDNN =============================
Running with images: dog.jpg eagle.jpg              
[XBLAS] # kernels: 1                                
[XDNN] using custom DDR banks 1                     
Device/Slot[0] (/dev/xdma0, 0:0:1d.0)               
xclProbe found 1 FPGA slots with XDMA driver running
CL_PLATFORM_VENDOR Xilinx                           
CL_PLATFORM_NAME Xilinx                             
CL_DEVICE_0: 0x192f180                              
CL_DEVICES_FOUND 1, using 0                         
loading kernel.aws.max.support.608.apr2.awsxclbin   
[XBLAS] kernel0: kernelSxdnn_0                      
Running network input 608x608 and output 19x19      
Loading weights/bias/quant_params to FPGA...        
Preparing Input...                                  
['dog.jpg', 'eagle.jpg']                            
Preparing Output...                                 
Reading labels...                                   
Loading script...                                   
Running 2 image(s)                                  

Total FPGA: 155.485153 ms
Image Time: (77.742577 ms/img):

Results for image 0: dog.jpg
Found 3 boxes               
Obj 0: dog                  
         score = 0.639982   
         (xlo,ylo) = (136,529)
         (xhi,yhi) = (306,210)
Obj 1: car                    
         score = 0.432358     
         (xlo,ylo) = (419,173)
         (xhi,yhi) = (689,81) 
Obj 2: bicycle                
         score = 0.572274     
         (xlo,ylo) = (112,475)
         (xhi,yhi) = (564,92) 
                                  
oimage = dog.jpg                                                        
Saving new image with bounding boxes drawn as out/dog.jpg

Results for image 1: eagle.jpg
Found 1 boxes
Obj 0: bird
         score = 0.855054
         (xlo,ylo) = (152,464)
         (xhi,yhi) = (606,51)

oimage = eagle.jpg
Saving new image with bounding boxes drawn as out/eagle.jpg

Success!

```

The following instructions are required should you be using AMI version 18.04.02 and earlier:

1. Install X11 forwarding utilities `sudo yum install xorg-x11-xauth`  

2. Give the root user authorization to control an X Windows server `sudo cp ~centos/.Xauthority /root/`


[here]: launching_instance.md
