# Xilinx ML Suite

### Tutorials
- [Image Classification GoogLeNet-v1 Demo][]
- [DeepDetect REST Tutorial][]
- [DeepDetect Webcam Tutorial][]
- [Caffe Tutorial][]
- [MxNet Tutorial][]
- [Quantization Tutorial][]
- [Compiler Tutorial][]
- [Prototxt to FPGA Tutorial][]
- [Using xfDNN Python APIs Tutorial][]




### Release Notes

- xfdnn_18_04_02
  - Added TesnforFlow Tutorial
  - Added Yolov2 Models and Example

- xfdnn_18_03_09
	- Added Python Streaming and Multi-Process APIs and Tutorials
	- Updates to Compiler and Quantizer

- xfdnn_17_12_15
	- General script and documentation cleanup
	- Added Compiler Tutorial
	- Added End to End Tutorial


- xfdnn_17_11_13.1
	- Supported Frameworks:
		- Caffe
		- MxNet
	- Models
		- 8/16-bit GoogLeNet v1
		- 8/16-bit ResNet50
		- 8/16-bit Flowers102
		- 8/16-bit Places365
	- Examples
		- DeepDetect REST Tutorial
		- DeepDetect Webcam
		- Caffe Image Classification
		- MxNet Image Classification
		- x8 FPGA Pooling GoogLeNet v1 Demo
	- xfDNN Tools
		- Compiler
		- Quantizer
	- Known Issues:
		- libdc1394 error: Failed to initialize libdc1394
			- Some of the examples will report this error, but it can be ignored.

### Questions and Support

- [AWS F1 Application Execution on Xilinx Virtex UltraScale Devices][]
- [SDAccel Forums][]

[Image Classification GoogLeNet-v1 Demo]:tutorials/image_classification.md
[DeepDetect REST Tutorial]:tutorials/deepdetect_rest.md
[DeepDetect Webcam Tutorial]:tutorials/deepdetect_webcam.md
[Quantization Tutorial]:tutorials/quantize.md
[Compiler Tutorial]:tutorials/compile.md
[Prototxt to FPGA Tutorial]:tutorials/endtoend.md
[Caffe Tutorial]:tutorials/caffe.md
[MxNet Tutorial]:tutorials/mxnet.md
[Using xfDNN Python APIs Tutorial]: tutorials/pythonexample.md

[AWS F1 Application Execution on Xilinx Virtex UltraScale Devices]: https://github.com/aws/aws-fpga/blob/master/SDAccel/README.md
[SDAccel Forums]: https://forums.xilinx.com/t5/SDAccel/bd-p/SDx
