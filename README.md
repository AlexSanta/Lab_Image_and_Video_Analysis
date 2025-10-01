## Project Work Overview
The laboratory activity focuses on predicting the future trajectory of a radio-controlled vehicle based on data collected during controlled driving sessions.<br>
At each time instant, the available information includes:
- the **past 3D trajectory** of the vehicle (over the previous few seconds)
- the **future 3D trajectory** of the vehicle (used as ground truth)
- the **3D point cloud** of the surrounding environment captured at the current instant
- the **RGB image** of the scene observed by the camera at the current instant

The steps performed are:
1. training a GRU to predict the future trajectory based solely on the ***past trajectory***<br>
2. extending the model by providing both the ***past trajectory*** and the ***current 3D point cloud*** (geometry only) as input for future trajectory prediction<br>
3. further extending the model by incorporating both the ***past trajectory*** and the ***current 3D point cloud with semantic per-point classification*** (obtained via ***Mask2Former***) to predict the future trajectory

For each of the above steps, two prediction strategies were implemented:
- an **autoregressive** model, which predicts the future trajectory step by step, recursively using its own previous outputs
- a **one shot** model, which outputs the full future trajectory all at once

## Performances
The following table reports the results for the different models after 100 training epochs, including their performances on the test set during the evaluation (weights of the best epoch are taken).

|                                                                                     | Training time | Best epoch | ADE (Total) | ADE (X) | ADE (Z) | FDE (Total) | FDE (X) | FDE (Z) |
|:-----------------------------------------------------------------------------------:|:-------------:|:----------:|:-----------:|:-------:|:-------:|:-----------:|:-------:|:-------:|
| **Autoregressive <br> prediction w/o the point cloud**                              |   6min37sec   |     90     |   0.3892m   | 0.2263m | 0.2611m |   0.9289m   | 0.6399m | 0.5329m |
| **One shot <br> prediction w/o the point cloud**                                    |   2min18sec   |     81     |   0.3904m   | 0.2260m | 0.2657m |   0.9413m   | 0.6301m | 0.5557m |
| **Autoregressive <br> prediction with the <br> point cloud (geometry only)**        |   7min42sec   |     28     |   0.3890m   | 0.2354m | 0.2607m |   0.8673m   | 0.6369m | 0.4750m |
| **One shot <br> prediction with the <br> point cloud (geometry only)**              |   3min10sec   |     21     |   0.3663m   | 0.2205m | 0.2470m |   0.8372m   | 0.5761m | 0.4912m |
| **Autoregressive <br> prediction with the <br> point cloud semantically annotated** |   7min40sec   |     82     |   0.3645m   | 0.2101m | 0.2541m |   0.8139m   | 0.5492m | 0.4941m |
| **One shot <br> prediction with the <br> point cloud semantically annotated**       |   3min20sec   |     15     |   0.3685m   | 0.2065m | 0.2563m |   0.8136m   | 0.5318m | 0.4918m |
