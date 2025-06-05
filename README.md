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
-an **autoregressive** model, which predicts the future trajectory step by step, recursively using its own previous outputs
-a **one shot** model, which outputs the full future trajectory all at once

## Performances
The following table reports the results for the different models after 200 training epochs, including their performances on the test set during the evaluation (weights of the best epoch are taken).

|                                                                                     | Training time | Best epoch | ADE (Total) | ADE (X) | ADE (Z) | FDE (Total) | FDE (X) | FDE (Z) |
|:-----------------------------------------------------------------------------------:|:-------------:|:----------:|:-----------:|:-------:|:-------:|:-----------:|:-------:|:-------:|
| **Autoregressive <br> prediction w/o the point cloud**                              |   15min38sec  |    195     |   0.2920m   | 0.1581m | 0.2077m |   0.6207m   | 0.4069m | 0.3797m |
| **One shot <br> prediction w/o the point cloud**                                    |   3min58sec   |    196     |   0.3750m   | 0.2328m | 0.2372m |   0.9004m   | 0.6409m | 0.4969m |
| **Autoregressive <br> prediction with the <br> point cloud (geometry only)**        |   16min56sec  |    173     |   0.1493m   | 0.0718m | 0.1140m |   0.2700m   | 0.1623m | 0.1777m |
| **One shot <br> prediction with the <br> point cloud (geometry only)**              |   7min6sec    |    165     |   0.1672m   | 0.0818m | 0.1272m |   0.3084m   | 0.1885m | 0.2028m |
| **Autoregressive <br> prediction with the <br> point cloud semantically annotated** |   16min58sec  |    198     |   0.1517m   | 0.0764m | 0.1126m |   0.2840m   | 0.1733m | 0.1861m |
| **One shot <br> prediction with the <br> point cloud semantically annotated**       |   7min44sec   |    199     |   0.1657m   | 0.0830m | 0.1240m |   0.3034m   | 0.1855m | 0.1987m |
