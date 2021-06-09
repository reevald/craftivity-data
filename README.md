# Craftivity-Data
This project focuses on providing data for Craftivity applications. The data provided is in the form of a Trashnet dataset, ML Model for garbage classification, and craft data based on the type of Garbage.

## Dataset
The dataset spans six classes: glass, paper, cardboard, plastic, metal, and trash. Currently, the dataset consists of 2527 images:

- 501 glass  
- 594 paper  
- 403 cardboard  
- 482 plastic  
- 410 metal  
- 137 trash  

Source : TrashNet (https://github.com/garythung/trashnet)

## Model ML
<table>
<tr><th colspan=2>TEST ACCURACY<br/><br/>with 70/15/15 ~ train/val/test</th></tr>
<tr>
  <td>w/o Transfer Learning</td>
  <td>w/ Transfer learning</td>
</tr>
<tr>
  <td>74.54%</td>
  <td>85.68%</td>
</tr>
</table>

![img1](assets/images/acc-and-loss.jpg)  

### TensorFlow Lite (TFLite Model)
Model with transfer learning (MobileNetV2 with Fine-Tuning), then converted to tflite model (float and quantization). By using 15 random images from the test dataset, the accuracy of the model is obtained as follows:  
<table>
<tr>
  <td>Float Model</td>
  <td>Quantization Model</td>
</tr>
<tr><th colspan=2>TEST ACCURACY TFLITE</th></tr>
<tr>
  <td>86.67%</td>
  <td>86.67%</td>
</tr>
<tr>
<th colspan=2>MODEL SIZE</th>
</tr>
<tr>
<td>8693KBs</td>
<td>2660KBs</td>
</tr>
</table>

The float model has been tested using the sample template provided by TensorFlow Lite (https://github.com/reevald/examples/tree/master/lite/codelabs/flower_classification/android/finish) with the following results:  

![img2](assets/images/testing-model.jpg)

### TensorFlow Js (TFJs Model)
Model with transfer learning (MobileNetV2 with Fine-Tuning), then converted to tfjs model (float and quantization).  

<table>
<tr>
  <td>Float Model</td>
  <td>Quantization Model</td>
</tr>
<tr>
<th colspan=2>TOTAL MODEL SIZE (FOLDER)<br><br>(model.json & group*-shard*.bin)</th>
</tr>
<tr>
<td>8950KBs</td>
<td>2344KBs</td>
</tr>
</table>  

To ensure the tfjs model runs well, the model is tested directly on the web: https://craftivity.profematika.com/trash-to-treasure  

Note:
- Please allow the use of the webcam on the web, if you will use the camera for image input.
- The initial process may take a few seconds.
- Some devices with WebGL that do not support 32 bit floating point textures, such as the Vivo Y53 (tested), may not be able to access the machine learning features on the website. (source: https://www.tensorflow.org/js/guide/platform_environment)

<video style="width: 100%; max-height: 100%;" controls>
  <source src="assets/video/rcd-demo.webm" type="video/webm">
</video>

## Usage on Google Colab

### Step 1
Open google colab to access jupyter notebook via the following link:
- For TFLite (Android)  
tflite-model-maker.ipynb  
https://colab.research.google.com/drive/1V2-jmHNjT2dm-9LtqfMG9ZQ0lVmsJzAS?usp=sharing
- For TFJs (Web)  
tfjs-model-maker.ipynb  
https://colab.research.google.com/drive/1s19d3_n7eLgnMffWlxMz28VW8v92VqOC?usp=sharing


### Step 2
Look at the menu bar, select file -> save a copy in drive, it will automatically make a copy in a new tab. Make sure that pop-up windows are not blocked. In this new tab, we will execute the cell by cell until the machine learning model is formed.
### Step 3
Run cells sequentially from top to bottom, each section equipped with related descriptions and references. Make sure the electricity and internet connection is in good condition. The resulting output is a tflite or tfjs model with float and quantization types that are ready to be deployed to Android or Web.

## Acknowledgments
- Thanks to Allah
- Thanks to Bangkit Academy 2021 instructor staff for a great class!
- Thanks to my team B21-CAP0046
- Thanks to my mentor Javentira Lienata

## TODOs
- Improve model accuracy with neural network architectures, update datasets, use other transfer learning, and more
- Try deploy model on cloud