# MidDeep_Learning
## Data

Download the following data from the [COCO website](https://archive.org/download/MSCoco2014), and place them, as instructed below, into the `cocoapi` subdirectory located *inside* this project's directory (the subdirectory was created when cloning the COCO API repo as shown in the **Setup** section above):

* under **Annotations**, download:
  - **2014 Train/Val annotations [241MB]** (extract `captions_train2014.json`, `captions_val2014.json`, `instances_train2014.json` and `instances_val2014.json`, and place them in the subdirectory `cocoapi/annotations/`)
  - **2014 Testing Image info [1MB]** (extract `image_info_test2014.json` and place it in the subdirectory `cocoapi/annotations/`)
* under **Images**, download:
  - **2014 Train images [83K/13GB]** (extract the `train2014` folder and place it in the subdirectory `cocoapi/images/`)
  - **2014 Val images [41K/6GB]** (extract the `val2014` folder and place it in the subdirectory `cocoapi/images/`)
  - **2014 Test images [41K/6GB]** (extract the `test2014` folder and place it in the subdirectory `cocoapi/images/`)
  
## Setup COCOAPI

1. Clone the [COCO API repo](https://github.com/cocodataset/cocoapi) into *this project's directory*:
```
git clone https://github.com/cocodataset/cocoapi.git
```

2. Setup COCO API (also described in the readme [here](https://github.com/cocodataset/cocoapi)):
```
cd cocoapi/PythonAPI
make
cd ..
```
