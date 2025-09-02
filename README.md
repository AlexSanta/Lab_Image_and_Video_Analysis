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
| **Autoregressive <br> prediction w/o the point cloud**                              |   6min34sec   |     77     |   0.3949m   | 0.2287m | 0.2668m |   0.9389m   | 0.6436m | 0.5437m |
| **One shot <br> prediction w/o the point cloud**                                    |   2min8sec    |     65     |   0.3853m   | 0.2337m | 0.2540m |   0.9220m   | 0.6435m | 0.5252m |
| **Autoregressive <br> prediction with the <br> point cloud (geometry only)**        |   7min41sec   |     91     |   0.3698m   | 0.2116m | 0.2598m |   0.7965m   | 0.5456m | 0.4746m |
| **One shot <br> prediction with the <br> point cloud (geometry only)**              |   3min8sec    |     36     |   0.3710m   | 0.2081m | 0.2591m |   0.8306m   | 0.5524m | 0.4937m |
| **Autoregressive <br> prediction with the <br> point cloud semantically annotated** |   8min7sec    |     26     |   0.3744m   | 0.2206m | 0.2540m |   0.8195m   | 0.5366m | 0.5055m |
| **One shot <br> prediction with the <br> point cloud semantically annotated**       |   3min19sec   |     77     |   0.3685m   | 0.1952m | 0.2686m |   0.8056m   | 0.5146m | 0.5099m |
