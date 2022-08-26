# UAY-INVECAS-IITH

This repo contains all the work done at LFOVIA, IIT Hyderabad as part of UAY project titled "Low Cost Design & Manufacture of Indigenous 24 GHz and 77 GHz Retrofittable Automotive Radar for Road Safety and Monitoring Driving Behaviour".

## Abstract

Autonomous and semi-autonomous navigation systems use multiple sensors for perception. Amongst all the sensors, the most prominently used are camera, lidar and radar. Camera and lidar are comparatively more expensive than radar. Also, camera and lidar fail to operate smoothly in adverse weather conditions. Radar, on the other hand, can operate in a wide range of temperature and weather conditions. Given radar's capabilities and recent advancements in deep learning, can a low-cost and robust perception solution be achieved? To address this, we make the following contributions via this work. We present a novel 77 GHz automotive radar dataset composed of both static and moving objects combined with a detailed analysis of the proposed dataset. We also propose using a novel $7 \times 5$ object representation framework for automotive radar data based object classification. We design a lightweight CNN architecture to classify objects present in the automotive radar scene and demonstrate that the proposed CNN delivers strong performance on our dataset. Additionally, we also experiment with the convLSTM architecture to exploit temporal characteristics present in the radar data. Further, we evaluate the performance of standard machine learning algorithms on the proposed dataset. Furthermore, we show that our CNN can also perform well on an open-source automotive radar dataset.

## Table of Contents
 - Dataset : The Dataset is present in the Radar_Dataset folder. It contains radar sequences of 5 individual objects, 4 of them being stationary objects and 1 (human - moving) being the only moving object. Each json file inside the stationary object's folder is named as "Class_distance(in metres)_date time.json". Each json file in the human-moving folder is named as " Class_range of distance from the radar(in metres)_time _date_time.json"

/ Explain contents in the json file also?


<table style="width:100%">
 <tr>
  <th>Objects</th>
  <th>Sequences</th>
  <th>Frames/seq</th>
  <th>Arrays/seq</th>
 </tr>
 <tr>
  <td> Car Vertical</td>
  <td>64</td>
  <td>614</td>
  <td>5895</td>
 </tr>
 <tr>
  <td>Car Horizontal</td>
  <td>22</td>
  <td>441</td>
  <td>3758</td>
 </tr>
 <tr>
  <td>Bike</td>
  <td>13</td>
  <td>951</td>
  <td>8792</td>
 </tr>
  <tr>
  <td>Human</td>
  <td>21</td>
  <td>388</td>
  <td>2688</td>
 </tr>
  <tr>
  <td>Human moving</td>
  <td>17</td>
  <td>992</td>
  <td>9457</td>
 </tr>
</table>

 
 - Radar Codes: 
   - The CNN_codes folder consists of the simple, 2-layer CNN along with a FCN and a softmax layer to perform object classification. The input is the 7x5 range doppler array extracted from the radar and this representation allows us to capture the spatial information which would diffrentiate similar objects like car-vertical and car-horizontal.
 
 CNN Confusion matrix:
 <table style="width:100%">
  <tr>
   <th></th>
   <th>human</th>
   <th>car-v</th>
   <th>car-h</th>
   <th>bike</th>
  </tr>
  <tr>
   <td>human</td>
   <td>3269</td>
   <td>3</td>
   <td>1</td>
   <td>2</td>
  </tr>
    <tr>
   <td>car-v</td>
   <td>0</td>
   <td>4197</td>
   <td>39</td>
   <td>23</td>
  </tr>
    <tr>
   <td>car-h</td>
   <td>0</td>
   <td>15</td>
   <td>3968</td>
   <td>15</td>
  </tr>
    <tr>
   <td>bike</td>
   <td>0</td>
   <td>26</td>
   <td>30</td>
   <td>3299</td>
  </tr>
 </table>
   
   - The Light_Weight_models folder consists of the classical ML models used. Here we compare the results of the CNN which uses 2D representation of the radar data (range and doppler signature) and the classical ML models which uses a 1D flattened representation. We trained several classifiers like k-NN, Random Forest, and Multinomial Logistic Regression on such 1D samples.
   
   Confusion matrix - Random Forest Classifier

<table style="width:100%">
  <tr>
    <th></th>
    <th>human</th>
    <th>car-v</th>
    <th>car-h</th>
 </tr>
 <tr>
  <td>human</td>
  <td>2097</td>
  <td>0</td>
  <td>0</td>
 </tr>
  <tr>
  <td>car-v</td>
  <td>0</td>
  <td>998</td>
  <td>1001</td>
 </tr>
  <tr>
  <td>car-h</td>
  <td>0</td>
  <td>844</td>
  <td>2048</td>
 </tr>
</table>

 Confusion matrix for k-NN classifier
 
  <table style="width:100%">
  <tr>
    <th></th>
    <th>human</th>
    <th>car-v</th>
    <th>car-h</th>
 </tr>
 <tr>
  <td>human</td>
  <td>2096</td>
  <td>0</td>
  <td>1</td>
 </tr>
  <tr>
  <td>car-v</td>
  <td>0</td>
  <td>998</td>
  <td>1001</td>
 </tr>
  <tr>
  <td>car-h</td>
  <td>0</td>
  <td>1479</td>
  <td>2213</td>
 </tr>
</table>

Confusion matrix for Multinomial Logistic Regression

 <table style="width:100%">
  <tr>
    <th></th>
    <th>human</th>
    <th>car-v</th>
    <th>car-h</th>
 </tr>
 <tr>
  <td>human</td>
  <td>2097</td>
  <td>0</td>
  <td>0</td>
 </tr>
  <tr>
  <td>car-v</td>
  <td>0</td>
  <td>1249</td>
  <td>750</td>
 </tr>
  <tr>
  <td>car-h</td>
  <td>0</td>
  <td>1927</td>
  <td>1765</td>
 </tr>
</table>
 
 -ConvLSTM codes folder contains the codes for our convolutional LSTM models. Since the radar data is a time series of radar frames we can use both the spatial and temporal correlation between the frames. The model was trained on the same data used for the CNN and Lightweight models. The convLSTM model was trained with a sequence of 10 consecutive 128x64 frames ( reconstructed from the 7x5 frames , refer our paper for more details). Each sequence was labelled to the object of which the sequence belonged. The results are as follows
 
 Confusion Matrix of convLSTM: 
 
  <table style="width:100%">
  <tr>
    <th></th>
    <th>human</th>
    <th>car-v</th>
    <th>car-h</th>
 </tr>
 <tr>
  <td>human</td>
  <td>98</td>
  <td>0</td>
  <td>0</td>
 </tr>
  <tr>
  <td>car-v</td>
  <td>0</td>
  <td>101</td>
  <td>9</td>
 </tr>
  <tr>
  <td>car-h</td>
  <td>0</td>
  <td>17</td>
  <td>78</td>
 </tr>
</table>

## Results

<table style="width:100%">
 <tr>
  <th>Model</th>
  <th>Accuracy(%)</th>
  <th>Precision</th>
  <th>Recall</th>
  <th>F1 score</th>
 </tr>
 <tr>
  <td>KNN Classifier</td>
  <td>55</td>
  <td>0.48</td>
  <td>0.56</td>
  <td>0.52</td>
 </tr>
 <tr>
  <td>Random Forest Classifier</td>
  <td>62</td>
  <td>0.54</td>
  <td>0.62</td>
  <td>0.58</td>
 </tr>
 <tr>
  <td>Logistic Regression</td>
  <td>74</td>
  <td>0.58</td>
  <td>0.74</td>
  <td>0.64</td>
 </tr>
 <tr>
  <td>Ensemble</td>
  <td>62</td>
  <td>0.54</td>
  <td>0.63</td>
  <td>0.5</td>
 </tr>
 <tr>
  <td>CNN</td>
  <td><strong>97</strong></td>
  <td><strong>0.97</strong></td>
  <td><strong>0.96</strong></td>
  <td><strong>0.97</strong></td>
 </tr>
 <tr>
  <td>convLSTM(Exp 1)</td>
  <td>94</td>
  <td>0.92</td>
  <td>0.91</td>
  <td>0.91</td>
 </tr>
 <tr>
  <td>convLSTM(Exp 2)</td>
  <td>67</td>
  <td>0.67</td>
  <td>0.67</td>
  <td>0.67</td>
 </tr>

</table>
/Add Carrada results after adding the codes
 
/Installation and dependencies?

/Credits (Contact) ?





