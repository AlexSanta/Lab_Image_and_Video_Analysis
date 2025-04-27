## Performances
Here are reported the results for the different models after 200 training epochs, including their performances on the test set during the evaluation (weights of the best epoch are taken).

|                                                          | Training time | Best epoch | Total ADE | ADE on x | ADE on z | Total FDE | FDE on x | FDE on z |
|:--------------------------------------------------------:|:-------------:|:----------:|:---------:|:--------:|:--------:|:---------:|:--------:|:--------:|
| Autoregressive <br> prediction                           |   33min24sec  |    191     |  0.1338m  |  0.0652m |  0.1019m |  0.2489m  | 0.1429m  |  0.1707  |
| One shot <br> prediction                                 |   9min54sec   |    200     |  0.2951m  |  0.1560m |  0.2149m |  0.6531m  | 0.4155m  |  0.4182m |
| Autoregressive <br> prediction with the <br> point cloud |   33min43sec  |    200     |  0.0946m  |  0.0414m |  0.0754m |  0.1601m  | 0.0872m  |  0.1150m |
| One shot <br> prediction with the <br> point cloud       |   8min48sec   |    195     |  0.1139m, |  0.0537m |  0.0880m |  0.2049m  | 0.1184m  |  0.1410m |
