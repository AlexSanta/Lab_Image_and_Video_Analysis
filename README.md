## Project Work Overview
The laboratory activity focuses on predicting the future trajectory of a radio-controlled vehicle based on data collected during controlled driving sessions.<br>
At each time instant, the available information includes:
- the **past 3D trajectory** of the vehicle (over the previous few seconds)
- the **future 3D trajectory** of the vehicle (used as ground truth)
- the **3D point cloud** of the surrounding environment captured at the current instant
- the **RGB image** of the scene observed by the camera at the current instant

The steps performed are:
1. training a GRU to predict the future trajectory based solely on the ***past trajectory***<br>
2. extending the model by providing both the ***past trajectory*** and the ***current 3D point cloud*** (geometry only) as input for future trajectory prediction

## Performances
The following table reports the results for the different models after the training, including their performances on the test set during the evaluation (weights of the best epoch are taken).

|                                                              | Training epochs | Training time | Best epoch | ADE (Total) | ADE (X) | ADE (Z) | FDE (Total) | FDE (X) | FDE (Z) |
|:------------------------------------------------------------:|:---------------:|:-------------:|:----------:|:-----------:|:-------:|:-------:|:-----------:|:-------:|:-------:|
| **Autoregressive <br> prediction**                           |       200       |   33min24sec  |    191     |   0.1338m   | 0.0652m | 0.1019m |   0.2489m   | 0.1429m | 0.1707m |
| **One shot <br> prediction**                                 |       200       |   9min54sec   |    200     |   0.2951m   | 0.1560m | 0.2149m |   0.6531m   | 0.4155m | 0.4182m |
| **Autoregressive <br> prediction with the <br> point cloud** |       150       |   24min52sec  |    134     |   0.0924m   | 0.0442m | 0.0708m |   0.1765m   | 0.0976m | 0.1240m |
| **One shot <br> prediction with the <br> point cloud**       |       150       |   10min24sec  |    145     |   0.1020m   | 0.0429m | 0.0829m |   0.1724m   | 0.0920m | 0.1239m |
