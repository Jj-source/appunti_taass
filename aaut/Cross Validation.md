2025-02-20 17:24

Status: #child

Tags: [[Machine Learning]]
# Cross Validation

![[crossValidation.png]]

Cross-validation is a robust technique used in machine learning to assess the performance and generalizability of a model. It involves partitioning the dataset into multiple subsets, or "folds," and then training and evaluating the model on different combinations of these folds. The most common method is **k-fold cross-validation**, where the data is divided into *$k$ equally sized folds*. The model is *trained $k$ times, each time using $k-1$ folds for training and the remaining fold for validation*. This process ensures that every data point gets to be in the training and validation set, providing a more reliable estimate of the model's performance compared to a single train-test split. Cross-validation helps in detecting overfitting, as it evaluates the model on multiple subsets, and is particularly useful when dealing with limited data, as it maximizes the use of available samples.