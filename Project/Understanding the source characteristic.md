#Research
## Optimizers
>[! Hint]
>In neural networks, *optimisers* are algorithms that determine how the model’s parameters (weights and biases) are updated during training so that the loss function is minimized.  
They sit between gradients (computed by backpropagation) and parameter updates, deciding the direction, step size, and sometimes the geometry of the update. (wiki)
- **SGD ( Stocastic Gradient Descent)**
	- The most primal things among all optimisers for NN
	 - This is given as 
	 - $$
\theta \leftarrow \theta-\eta\frac{\partial L(\theta)}{\partial w}
$$
		 - $\theta$ : parameter such as weights, biases
		 - $L$: Loss function, normally this is non-convex
			 - There are several types of Loss functions
			 - In the following equations $f(x,\theta)$  represents Neural Network, $x$ represents input-data.
				 - *MSE (Mean Square Error)*
					 - $$
			 L(\theta)=\frac{1}{n}\sum(y_i -f(x,\theta))^2
					  $$
				  - *MAE (Mean Abusolute Error)*
					  - $$L(\theta)=\frac{1}{n}\sum(|y_i -f(x,\theta)|)$$
				  - *MSLE (Mean Squared Logarithmic Error)*
					  -  $$ L(\theta)=\frac{1}{n}\sum(\log(1+y_i) -\log(1+f(x,\theta)))^2$$
				  - *Cross Entropy*
					  - loss function  for classification task
					  -   $$ L(\theta)=-\sum_k t_k \log f(x,\theta)$$
					  - where $t_k$ is the label representing correct-or-not
						  - if the prediction was correct : 1 otherwise : 0
	 - GD based approach today is the de facto standard of NN's optimizer
	 - In GD, the direction in which the parameters should be update is given as the gradient of the loss function.
	 - $$
	 \frac{d\theta}{dt}=-\nabla L(\theta)
	  $$
	   - In SGD, 