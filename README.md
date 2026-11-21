# Chinese Handwritten Character Recognition

## Model Results

Three CNN models were trained for **3 epochs** and evaluated on the same test set of **162,550 images from 13,022 classes**.

| Model | Parameters | Test Accuracy (Top-1) | Test Top-5 Accuracy | Test Loss |
|---|---:|---:|---:|---:|
| **A2** | **2,368,009** | **74.577%** | **93.985%** | **0.948** |
| B | 1,149,001 | 48.442% | 76.010% | 2.284 |
| C | 295,929 | 3.029% | 9.701% | 6.717 |

**A2 performed best**, followed by B and C. Top-1 accuracy means the first prediction is correct; Top-5 accuracy means the correct answer appears among the five highest-ranked predictions.

## Model Differences and Their Effect on Accuracy

All three models used **48 × 48 grayscale inputs, batch size 1,024, Adam with an initial learning rate of 0.0003, and 3 training epochs**. They shared the same data splits, augmentation, LeakyReLU activation, and dropout rate of 0.3. The main differences were model depth, convolution filters, and hidden Dense units.

| Architecture | A2 | B | C |
|---|---|---|---|
| Convolution layers | 3 | 2 | 1 |
| Filters per layer | 32 → 64 → 128 | 16 → 32 | 8 |
| Hidden Dense units | 128 | 64 | 16 |
| Output units | 13,065 | 13,065 | 13,065 |

**A2 — deeper and larger:** Three convolution layers can combine simple stroke features into more complex character patterns. More filters and a 128-unit Dense layer provide a larger representation for distinguishing similar characters. This is consistent with A2 achieving the highest test accuracy, **74.577%**.

**B — medium capacity:** Two convolution layers with fewer filters and 64 Dense units provide less capacity than A2. B learned useful character features but made more classification errors, achieving **48.442%** test accuracy. It used about half as many parameters as A2.

**C — smallest capacity:** One convolution layer with only 8 filters and 16 Dense units restricts the features available to separate thousands of character classes. Its **3.029%** test accuracy is consistent with insufficient capacity or insufficient learning within three epochs.

The results suggest that the deeper, larger architecture was more effective under these training settings. However, several architectural features changed together, so the accuracy differences cannot be attributed to layer count alone. More parameters do not guarantee higher accuracy in every experiment.
