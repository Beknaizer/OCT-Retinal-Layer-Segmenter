<!-- ![]( | width=100)
 -->
<img src="/for_readme/OCT.png" width=400 height=130 >

# OCT - Retinal Layer Segmenter
A deep learning algorithm for multiclass semantic segmentation of retinal layers in Optical Coherence Tomography images.

## Table of contents
* [General info](#general-info)
* [Retinal layers](#retinal-layers)
* [Dataset](#dataset)
* [Technologies](#technologies)
* [Architecture](#architecture)
* [Usage](#usage)
* [Checkpoints](#checkpoints)

## General info
This is the deep learning based approach to segement retina layers on Optical Coherence Tomogrpahy images. The main aim of project is to automate segmentation process of layers by using neural networks. 

![Alt text](/for_readme/ezgif.com-gif-maker.gif "Optional title")

## Dataset

[Dataset](<https://dataverse.scholarsportal.info/dataset.xhtml?persistentId=doi:10.5683/SP/WLW4ZT> "Optional title") is publicly available. It is OCT Image Database (OCTID) of
University of Waterloo, 2018 year. There is a fovea-centered OCT image of 25
healthy patients. Size 750 x 500 pixels, grayscale images. Images in dataset I used as 'X' label, but for 'Y' (ground truth) i segmented it manually by using [makesense.ai](<https://www.makesense.ai/>) tool.

## Retinal layers
  Segmentation of retinal layers on OCT images is important. Because it gives the ability to identify eye disease by observing images. Identifying eye disease in the next way: it depends on the height of each layer in the image. And the correct way of its segmentation greatly facilitates the visual prediction of the diagnosis. Nowadays problem is that more than 300M people in the world have diseases related to diabetic macular edema, age related macular degeneration, diabetic retinopathy and so on. Studies show that retinal structure changes are triggered before the vision field problems occur. Therefore the segmentation of retina layers on OCT image is important in timely treatment of diseases, and deep learning algorithms can make it much faster and in most cases more accurate than humans of course, if you write and train your algorithm in the right way. 

 Algorithms can segemnt 8 layers:
- NFL - nerve fiber layer;
- GCL+IPL - ganglion cell layer, inner plexiform layer;
- INL - inner nuclear layer;
- OPL - outer plexiform layer;
- ONL - outer nuclear layer;
- Ellipsoid zone; 
- RPE - retinal pigment epithelium;
- Choroid; 

![](/for_readme/layers.png)
	
## Technologies
Project is created with:

* <img src="https://brandslogos.com/wp-content/uploads/images/large/python-logo.png" width=16 height=16> Pyhton version: 3.8.10
* <img src="https://avatars.githubusercontent.com/u/15658638?s=280&v=4" width=16 height=16> Tensorflow version: 2.4.1
* <img src="/for_readme/pngwing.com.png" width=16 height=16> Numpy version: 1.22.4
* <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/84/Matplotlib_icon.svg/1200px-Matplotlib_icon.svg.png" width=16 height=16> Matplotlib version: 3.5.2
* <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/53/OpenCV_Logo_with_text.png/487px-OpenCV_Logo_with_text.png" width=16 height=16> OpenCV version: 4.5.5
* <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Keras_logo.svg/1200px-Keras_logo.svg.png" width=16 height=16> Keras versoin: 2.4.0


## Architecture
 
UNet is a specially designed architecture of CNN for image segmentation in different cases, but originally, for biomedical images. It is designed to identify not only bold obvious border lines, but also thin barely noticeable lines. Because of this reason originally it was designed for biomedical images, where you should segment vessels on eye images for example and so on. It is a sequence of convolution that decreases image size till some moment and vice versa upsample it again by adding additional info from corresponding previous layer. Because of this reason it is called UNet, this type of processes create U shaped architecture. Below, you can view a detailed UNet architecture which a used in this work.


<img src="/for_readme/256.png">

As you can see in figure upper, algorithm takes a grayscale image with 640x640x1 as input and gives 640x640x9 as output image. Each layer in the output image is a retinal layer in the OCT image.

<img src="/for_readme/layers_1by1.gif">

IoU(Intersection over Union) - is a common evaluation metric for semantic image segmentation. Mean IoU of algorithm - 75.4%. As activation function I used ReLu, as validation metrics - simple accuracy of keras.models library. Final value of accuracy - 96.45%, loss - 0.1016 (decreased from 2.01).

<img src="/for_readme/accuracy&loss.png">

## Usage
>json_mask_reading.ipynb

This is jupyter-notebook for converting JSON files with coordinates to segmented masks of original OCT images. For segmenting I used [makesense.ai](<https://www.makesense.ai/>) tool. As result it gives in type of VGG JSON. </br>:hammer_and_wrench: Variables that should be changed:
* *json_file* - local path to VGG JSON file
* *original_images* - local path to original OCT images
* *result_save* - local path to store result images -segmented masks
* *class_dict* - your label names in VGG JSON (segmentation classes)

>simple_unet.py

It is python file that contain UNet architecture model as class. This class we will use in the main segmentation file. </br>:heavy_check_mark: *Nothing needs to be changed* 

>multiclass_segmentation.ipynb

It is jupyter-notebook file that contain main part of segmentation algorithm.</br> :hammer_and_wrench: Variables that should be changed:
* *TRAIN_PATH_X* - local path to original OCT images (X-label)
* *TRAIN_PATH_Y* - local path to segmeted OCT imaes, maskes (Y-label)
* *n_classe* - number of classes for segmentation
* *SIZE_X* - width of image (optional, default 640 pixels)
* *SIZE_Y* - height of image (optional, default 640 pixels)

## Checkpoints
 [Here](https://drive.google.com/drive/folders/1zKkv0BsFAHi2BV7oUBiD8FRK_HDMaViE?usp=sharing) you can download already trainded weights for OCTID dataset.
