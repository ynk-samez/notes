#Research

## Optimizers
>[! Hint]
>In neural networks, *optimisers* are algorithms that determine how the model’s parameters (weights and biases) are updated during training so that the loss function is minimized.  
They sit between gradients (computed by backpropagation) and parameter updates, deciding the direction, step size, and sometimes the geometry of the update. (wiki)
>![[https___ruder.io_content_images_2016_09_saddle_point_evaluation_optimizers.avif]]

## Theoretic
### SGD ( Stocastic Gradient Descent)
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
		  - $$\theta_t-\theta_{t-1}=-\nabla L(\theta)$$
		  - $$\theta_t=\theta_{t-1}-\nabla L(\theta)$$
	  
		- the input-data is given randomly: shuffled
		   - ![[Pasted image 20260120221520.png]]
##  Practical
### Momentum-SGD
-  Accumulates past gradients as a velocity vector.
- Introduces inertia into parameter updates.
- Reduces oscillations in directions of high curvature.
- Accelerates convergence along consistent descent directions.
	$$\begin{align}
v_t &= \mu v_{t-1} - \eta g_t \\
\theta_{t+1} &= \theta_t + v_t
\end{align}
$$
### Nesterov Accelerated Gradient (NAG)
 - Computes the gradient at a look-ahead position.
- Anticipates the future parameter location before updating.
- Provides more accurate corrective updates than classical momentum.
- Often yields better convergence guarantees.
$$
\begin{align}
v_t &= \mu v_{t-1} - \eta \nabla L(\theta_t + \mu v_{t-1}) \\
\theta_{t+1} &= \theta_t + v_t
\end{align}
$$
### RMSprop
-  Normalizes gradients using an exponential moving average of squared gradients
- Prevents learning rates from shrinking monotonically.
- Handles non-stationary and noisy objectives effectively.
- Serves as a foundation for Adam’s second-moment estimation.
$$
\begin{align}
E[g^2]_t &= \rho E[g^2]_{t-1} + (1-\rho) g_t^2 \\
\theta_{t+1} &= \theta_t
- \eta \frac{g_t}{\sqrt{E[g^2]_t} + \epsilon}
\end{align}
$$
### AdaGrad
- Adapts the learning rate for each parameter individually.
- Scales updates inversely proportional to accumulated squared gradients.
- Performs well for sparse features.
- Suffers from overly aggressive learning rate decay over time.
$$
\begin{align}
G_t &= G_{t-1} + g_t \odot g_t \\
\theta_{t+1} &= \theta_t - \eta \frac{g_t}{\sqrt{G_t} + \epsilon}
\end{align}
$$
### AdaDelta
- Replaces cumulative gradient sums with exponential moving averages.
- Eliminates the need for a manually chosen global learning rate.
- Maintains unit consistency between updates and parameters.
- More robust than AdaGrad for long training runs.
$$
\begin{align}
E[g^2]_t &= \rho E[g^2]_{t-1} + (1-\rho) g_t^2 \\
\Delta \theta_t &= - \frac{\sqrt{E[\Delta \theta^2]_{t-1} + \epsilon}}
{\sqrt{E[g^2]_t + \epsilon}} g_t \\
E[\Delta \theta^2]_t &= \rho E[\Delta \theta^2]_{t-1}
+ (1-\rho)(\Delta \theta_t)^2 \\
\theta_{t+1} &= \theta_t + \Delta \theta_t
\end{align}
$$
### Adam
- Combines momentum with adaptive per-parameter learning rates.
- Uses bias-corrected first and second moment estimates.
- Converges quickly with minimal hyperparameter tuning.
- Widely used as a default optimizer in deep learning(90%?).
$$
\begin{align}
m_t &= \beta_1 m_{t-1} + (1-\beta_1) g_t \\
v_t &= \beta_2 v_{t-1} + (1-\beta_2) g_t^2 \\
\hat{m}_t &= \frac{m_t}{1-\beta_1^t} \\
\hat{v}_t &= \frac{v_t}{1-\beta_2^t} \\
\theta_{t+1} &= \theta_t - \eta
\frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon}
\end{align}
$$
