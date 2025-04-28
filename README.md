# Project Work Overview
The laboratory activity focuses on predicting the future trajectory of a radio-controlled vehicle based on data collected during controlled driving sessions.<br>
At each time instant, the available information includes:
- the **past 3D trajectory** of the vehicle (over the previous fiew seconds)
- the **future 3D trajectory** of the vehicle (used as ground truth)
- the **3D point cloud** of the surrounding environment captured at the current instant

The two steps performed are:
- training a GRU to predict the future trajectory based solely on the ***past trajectory***
- extending the model by providing both the ***past trajectory*** and the ***current 3D point cloud*** (geometry only) as input for future trajectory prediction

## Performances
The following table reports the results for the different models after 200 training epochs, including their performances on the test set during the evaluation (weights of the best epoch are taken).

|                                                              | Training time | Best epoch | ADE (Total) | ADE (X) | ADE (Z) | FDE (Total) | FDE (X) | FDE (Z) |
|:------------------------------------------------------------:|:-------------:|:----------:|:-----------:|:-------:|:-------:|:-----------:|:-------:|:-------:|
| **Autoregressive <br> prediction**                           |   33min24sec  |    191     |   0.1338m   | 0.0652m | 0.1019m |   0.2489m   | 0.1429m | 0.1707m |
| **One shot <br> prediction**                                 |   9min54sec   |    200     |   0.2951m   | 0.1560m | 0.2149m |   0.6531m   | 0.4155m | 0.4182m |
| **Autoregressive <br> prediction with the <br> point cloud** |   33min43sec  |    200     |   0.0946m   | 0.0414m | 0.0754m |   0.1601m   | 0.0872m | 0.1150m |
| **One shot <br> prediction with the <br> point cloud**       |   8min48sec   |    195     |   0.1139m   | 0.0537m | 0.0880m |   0.2049m   | 0.1184m | 0.1410m |
