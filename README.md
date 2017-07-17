# yolomex
yolomex is a simple Matlab MEX wrapper for YOLO (based on pyyolo by thomaspark-pkj).

## Building libyolo
1. git clone --recursive https://github.com/ignacio-rocco/yolomex.git
2. Set GPU=1 in Makefile to use GPU and adjust CUDA include path
3. make

## Compile yolomex
From Matlab (without CUDA): 
```bash
mex -I"./darknet/include/" -L"." -lyolo yolomex.c
```
With CUDA (adjust CUDA lib path):
```bash
mex -I"./darknet/src" -I"./darknet/include/" CFLAGS="-Wall -Wfatal-errors -Wno-unused-result -fPIC" -L"." -lyolo -L"/usr/local/cuda-7.0/lib64" -lcudart -lcublas -lcurand yolomex.c
```

## Test
From Matlab: 
```bash
datacfg = fullfile(pwd,'darknet/cfg/coco.data');
cfgfile = fullfile(pwd,'darknet/cfg/tiny-yolo.cfg');
weightfile = fullfile(pwd,'tiny-yolo.weights');
filename = fullfile(pwd,'darknet/data/person.jpg');
thresh = 0.24;
hier_thresh = 0.5;
I = imread(filename);

yolomex('init',datacfg,cfgfile,weightfile)

detections=yolomex('test',filename,thresh,hier_thresh)    

detections=yolomex('detect',I,thresh,hier_thresh)  
```
