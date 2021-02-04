# eyeDo: an Android App for the Visually Impaired that uses a Neural Network to recognize Pedestrian Traffic Light in real-time

The dataset and model we used for our project is based on the ones used for the project "ImVisible", explained at this link: https://arxiv.org/abs/1907.09706. 

## Introduction
In this project we trained a model called LytNet, then we converted the model from Pytorch to TorchScript and developed an Android App that uses it to recognize the state of pedestrian traffic lights. The following image represents the approach we followed and the related path options.

![](path.png)

To train and test the LytNet we have used "Pedestrian-Traffic-Lights (PTL)", which is a high-quality image dataset of street intersections, created for this problem of image classification. Images have variations in weather, position and orientation in relation to the traffic light. To download the dataset you can visit the ImVisible project (link above).

## Training

|   | Training | Validation | Testing | Total
|---|----------|------------|---------|-------
Number of Images | 3456 | 864 | 739 | 5059
Percentage | 68.3% | 17.1% | 14.6% | 100%

Use these stats for image normalization:  
mean = [120.56737612047593, 119.16664454573734, 113.84554638827127]  
std=[66.32028460114392, 65.09469952002551, 65.67726614496246]

### Labels

Classes are as follows:

0: Red
1: Green
2: Countdown Green
3: Countdown Blank
4: None

Here are the precisions of networks for each class:

|         | Red | Green | Countdown Green | Countdown Blank | None
|---------|-----|-------|-----------------|-----------------|--------|
Base Precision | 0.97 | 0.94 | 0.99 | 0.90 | 0.76
Base Opt Precision | 0.95 | 0.94 | 0.98 | 0.91 | 0.75
Base Opt Quantized Precision | 0.96 | 0.92 | 0.99 | 0.89 | 0.78
Normalized Precision | 0.92 | 0.96 | 0.97 | 0.91 | 0.45
Normalized Opt Precision | 0.93 | 0.91 | 0.94 | 0.91 | 0.50

Opt stands for Optimized for Mobile.


The network model is adapted from a MobileNetV2, with a larger input size of 768x576 designed for a image classification task that involves a smaller object within the image (such as a traffic light). 

## Conversion
The code that converts a Pytorch model to a TorchScript one is the file "fromPTtoPTScript.py". 

The network needs a [batch, channels, height, width] shape. See fromPTtoPTScript.py for more information about it.

## Application
We developed an Android Application that use the model converted. You can find the repo here: https://github.com/marcoleino/eyeDo_Android/tree/master
