
# Score Matching

**Score matching** is a method to train a model to estimate the *score
function* of a data distribution:
```math
\nabla_{x} {log(p(x))}
```

Instead of modeling the full probability distribution, the model
directly learns how the probability changes with respect to the data.
This avoids computing normalization constants.

# How Score Matching Works

The main idea of **score matching** is to train a model \$s_{\theta}(x)\$ to approximate the true score function \$\nabla_{x}{log(p(x))}\$, which indicates how probability
density changes with respect to the data.

### General Procedure

1. **Define a model:**  
   Build a neural network \$s_{\theta}(x)\$ that outputs a vector of the same dimension as the data \$x\$.  
   Each component represents the estimated gradient of the log-probability with respect to one dimension of the data.

2. **Use data samples:**  
   Draw samples \$x \sim p(x)\$ from the data distribution.  
   Importantly, we don’t need to know the explicit formula of \$p(x)\$; only the samples are required.

3. **Train the model:**  
   The model is optimized so that its outputs \$s_{\theta}(x)\$ match the true score function.  
   In practice, this is often done through *denoising score matching* or *diffusion-based* methods, which add noise to data and train the model to predict how to remove it.

4. **Apply the learned score:**  
   Once trained, the score model can be used to guide data generation or transformation.  
   For example, in diffusion models, the learned score function drives the reverse process that transforms noise back into realistic data samples.

---

In summary, **score matching** focuses on learning the geometry of a data distribution—how the probability mass is arranged in space—without directly estimating probabilities.  
