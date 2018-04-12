# Object Detection Tutorial

## Introduction
This tutorial explains how to execute a YOLOv2 network with FPGA acceleration.
The model execution utilizes:
* 16-bit quantized weights
* 56x32 DSP Array
* 5MB of on chip SRAM

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
    ```

The following instructions are required should you be using AMI version 18.04.02 and earlier:

1. Install X11 forwarding utilities `sudo yum install xorg-x11-xauth`  

2. Give the root user authorization to control an X Windows server `sudo cp ~centos/.Xauthority /root/`

[COCO]: http://cocodataset.org/#home
[here]: launching_instance.md
