2025-02-20 17:29

Status: #child

Tags: [[Machine Learning]]
# Micro-average and Macro-average
## Example 1: Class Prediction with Bias Toward the Majority Class
Assume you have a class-imbalanced dataset with two classes, and the classifier is biased toward the majority class. You have collected classification performance metrics, such as precision:
$$
\text{Precision (class } i) = \frac{TP_i}{TP_i + FP_i}
$$
### Results:
- **Precision (class 1)**:
  $$
  \text{Precision (class 1)} = \frac{80}{80 + 20} = 0.8
  $$
- **Precision (class 2)**:
  $$
  \text{Precision (class 2)} = \frac{1}{1 + 9} = 0.1
  $$
### Confusion Matrix:

|                  | Estimated class 1 | Estimated class 2 |
| ---------------- | ----------------- | ----------------- |
| **True class 1** | 80                | 9                 |
| **True class 2** | 20                | 1                 |
## Micro-average and Macro-average Definitions

- **Micro-Average Precision**:
  $$
  \text{Micro-Average Precision} = \frac{\sum_{i} TP_i}{\sum_{i} (TP_i + FP_i)}
  $$
  $$
  = \frac{80 + 1}{80 + 1 + 20 + 9} = 73.63\%
  $$
- **Macro-Average Precision**:
$$
  \text{Macro-Average Precision} = \frac{\sum_{i} \text{Precision (class } i)}{\text{number of classes}}
  $$
  $$
  = \frac{0.8 + 0.1}{2} = 45\%
  $$

### Conclusion:
- **Micro-average** is influenced by the majority class due to the larger number of examples. The classifier's performance on the majority class (80%) significantly impacts the micro-average precision (73.63%).
- **Macro-average** considers the performance on both classes equally, so the poor performance on the minority class (10%) lowers the macro-average (45%).
## Example 2: Class Prediction with Bias Toward the Minority Class
Assume you have a class-imbalanced dataset with two classes, and the classifier is biased toward the minority class. You have collected classification precision as follows:
- **Precision (class 1)**:
  $$
  \text{Precision (class 1)} = \frac{20}{20 + 80} = 20\%
  $$
- **Precision (class 2)**:
  $$
  \text{Precision (class 2)} = \frac{9}{9 + 1} = 90\%
  $$
### Confusion Matrix:

|                  | Estimated class 1 | Estimated class 2 |
| ---------------- | ----------------- | ----------------- |
| **True class 1** | 20                | 1                 |
| **True class 2** | 80                | 9                 |
### Results:
- **Micro-Average Precision**:
  $$
  \text{Micro-Average Precision} = \frac{20 + 9}{20 + 9 + 80 + 1} = 26.36\%
  $$
- **Macro-Average Precision**:
  $$
  \text{Macro-Average Precision} = \frac{0.2 + 0.9}{2} = 55\%
  $$
### Conclusion:
- **Micro-average** is influenced by the majority class's poor performance (20%), resulting in a lower micro-average precision (26.36%).
- **Macro-average** considers the minority class's strong performance (90%) equally, increasing the macro-average (55%).
