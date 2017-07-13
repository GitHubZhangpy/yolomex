# yolomex
yolomex is a simple Matlab MEX wrapper for YOLO (based on pyyolo by thomaspark-pkj).

## Building libyolo
1. git clone --recursive https://github.com/thomaspark-pkj/pyyolo.git
2. (optional) Set GPU=1 and CUDNN=1 in Makefile to use GPU.
3. make

## Compile yolomex
From Matlab: 
```bash
mex -I"./darknet/include/" -L"." -lyolo yolomex.c
```

## Test
From Matlab: 
```bash
datacfg = 'cfg/coco.data'
cfgfile = 'cfg/tiny-yolo.cfg'
weightfile = '../tiny-yolo.weights'
filename = 'data/person.jpg'
thresh = 0.24
hier_thresh = 0.5
I = imread(filename);

yolomex('init',datacfg,cfgfile,weightfile)

detections=yolomex('test',filename,thresh,hier_thresh)    

detections=yolomex('detect',I,thresh,hier_thresh)  
```
