#ResearchProject
## Optimizers
>[! Hint]
>In neural networks, *optimisers* are algorithms that determine how the model’s parameters (weights and biases) are updated during training so that the loss function is minimized.  
They sit between gradients (computed by backpropagation) and parameter updates, deciding the direction, step size, and sometimes the geometry of the update. (wiki)
- **SGD (Stocastic Gradient Descent)**
	- The most primal things among all optimisers for NN
	 - This is given as 
	 - $$
\theta \leftarrow \theta-\eta\frac{\partial L(\theta)}{\partial w}
$$
		 - $\theta$ : parameter such as weights, biases
		 - $L$: Loss function, normally this is non-convex
	 - Gradient decent(GD) based approach today is the de facto standard of NN's optimizer
	 - In GD, the direction in which the parameters should be update is given as the gradient of the loss function.
	 - $$
	 \frac{d\theta}{dt}=-\nabla L(\theta)
	  $$
	  - In mini-batch 
	  - 