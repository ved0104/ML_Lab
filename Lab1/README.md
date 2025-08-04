# Linear Regression with Batch & Online SGD in Python (from Scratch)

This project demonstrates how to build linear regression models using both Batch SGD (Stochastic Gradient Descent) and Online (Stochastic) SGD entirely from scratch in a Jupyter Notebook. The workflow includes data handling, gradient computation, training loops, and evaluation using Mean Squared Error (MSE)—all without any machine learning libraries.

## Dataset Example

The provided dataset has four columns:  
`TV`, `Radio`, `Newspaper` (advertising spend), and `Sales` (units sold).
```
TV,Radio,Newspaper,Sales
230.1,37.8,69.2,22.1
44.5,39.3,45.1,10.4
...
```

## Main Steps

1. **Prepare Data:**
   - Use pandas/numpy to load and structure the tabular data.
   - Add a bias column to your feature matrix for intercept fitting.

2. **Implement Mean Squared Error:**
   ```python
   def MSE(y, y_pred):
       return np.mean(np.power(y - y_pred, 2))
   ```

3. **Batch SGD:**
   - Updates weights after evaluating the gradient on the entire dataset.
   - **Key**: The gradient must use the **error vector** (`y_pred - y`), not the scalar MSE.
   ```python
   def batch_sgd(X, y, lr=0.00001, epochs=1000):
       np.random.seed(0)
       n_samples, n_features = X.shape
       weights = np.random.randn(n_features)
       for epoch in range(epochs):
           y_pred = X.dot(weights)
           error = y_pred - y  # Vector of errors
           grad = 2 * X.T.dot(error) / n_samples
           weights -= lr * grad
       return weights
   ```

4. **Online (Stochastic) SGD:**
   - Updates weights for each data point individually.
   ```python
   def online_sgd(X, y, lr=0.00001, epochs=1000):
       np.random.seed(0)
       n_samples, n_features = X.shape
       weights = np.random.randn(n_features)
       for epoch in range(epochs):
           for i in range(n_samples):
               xi = X[i, :]
               yi = y[i]
               y_pred = xi.dot(weights)
               error = y_pred - yi
               grad = 2 * xi * error
               weights -= lr * grad
       return weights
   ```

5. **Monitoring Training:**
   - Calculate and print the MSE with the `MSE()` function to evaluate model performance, but do not use scalar MSE for gradients.

## Key Points

- **Always** use the error vector, not the MSE scalar, when computing gradients for SGD.
- Use the scalar MSE only for evaluation/monitoring, not during weight updates.

## Usage

1. Copy the notebook code snippets and run them step-by-step.
2. Optionally, paste or load your own data in a similar format.
3. Compare the trained weights and MSEs from both algorithms.
4. Make predictions using the trained weight vectors.

**Happy learning and experimenting with linear regression from scratch!**