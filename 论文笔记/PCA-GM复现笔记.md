## PCA-GM的复现

## How to build the adjacency matrix A

input: point 

 



**Pascal VOC Keypoint** (mean accuracy is on the last column)

| method  | aero | bike | bird | boat | bottle | bus  | car  | cat  | chair | cow  | table | dog  | horse | mbike | person | plant | sheep | sofa | train | tv   | mean     |
| ------- | ---- | ---- | ---- | ---- | ------ | ---- | ---- | ---- | ----- | ---- | ----- | ---- | ----- | ----- | ------ | ----- | ----- | ---- | ----- | ---- | -------- |
| GMN     | 31.9 | 47.2 | 51.9 | 40.8 | 68.7   | 72.2 | 53.6 | 52.8 | 34.6  | 48.6 | 72.3  | 47.7 | 54.8  | 51.0  | 38.6   | 75.1  | 49.5  | 45.0 | 83.0  | 86.3 | 55.3     |
| PCA-GM  | 40.9 | 55.0 | 65.8 | 47.9 | 76.9   | 77.9 | 63.5 | 67.4 | 33.7  | 65.5 | 63.6  | 61.3 | 68.9  | 62.8  | 44.9   | 77.5  | 67.4  | 57.5 | 86.7  | 90.9 | **63.8** |
| rebuild | 46.4 | 64.1 | 60.2 | 55.2 | 77.5   | 72.3 | 63.9 | 69.2 | 39.7  | 62.1 | 48.9  | 63.5 | 64.1  | 61.9  | 41.2   | 80.4  | 67.3  | 67.0 | 81.4  | 90.1 | **63.8** |

**Willow Object Class**