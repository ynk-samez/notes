
## Contents
1. [preliminaries](#preliminaries)
	1. [the decision of the scaling parameter for lattices](#the%20decision%20of%20the%20scaling%20parameter%20for%20lattices)
	2. [works on lattice quantisation](#works%20on%20lattice%20quantisation)
2. [Investigation](#Investigation)

## preliminaries 
### Decision of the scaling parameter for lattices
- MSE of lattice quantisation depends on the scaling parameter $\beta$ 
$$
\mathcal{C}= \frac{\beta}{M}\Lambda/\beta\Lambda
$$
- it's hard to find the optimal $\beta$, since there are some local minimums in particular $n\geq2$  ![[Pasted image 20260102195658.png]]

## Investigation

>[!tip] What is characteristic of NN's gradients?  
>To answer this question is important even though our interest is in the quantisation technique itself, since NNs are the source which produces the vectors we treat. The optimal way to quantify depends on the source's characteristics.
- ** What I conducted **
	- observed the gradients and their dynamics from NN
	- task : classification
	- datasets: 
		- *MNIST* (images of handwritten numbers)　this is relatively easy
		- *CIFAR-10* (images of 10 types of flowers) this is relatively difficult 
	- Architectures : 
		- I compared some architectures to evaluate whether the results can be generalised or not.
			- *Simple DNN(5 hidden layers)*
				- non-practical but simple, enough for MNIST
			- *ResNet*
				- This can be said as the origin of  ''Transformer''(most practical architecture today) 
				- won the ML competition in 2014 
			- *DenseNet*
				- this has some skip connections among the blocks
				- ![[Pasted image 20260103185246.png]]
			- *AlexNet*
				- practical but complex, required a fertile computation source
				- This has won the classification competition in 2012 
				- ![[Pasted image 20260103185717.png]]
					```python
					## definition on Pytorch library
			class AlexNet(nn.Module):
			    def __init__(self, num_classes=1000):
			        super().__init__()
			        self.features = nn.Sequential(
			            nn.Conv2d(3, 64, kernel_size=11, stride=4, padding=2),
			            nn.ReLU(inplace=True),
			            nn.MaxPool2d(kernel_size=3, stride=2),
			            nn.Conv2d(64, 192, kernel_size=5, padding=2),
			            nn.ReLU(inplace=True),
			            nn.MaxPool2d(kernel_size=3, stride=2),
			            nn.Conv2d(192, 384, kernel_size=3, padding=1),
			            nn.ReLU(inplace=True),
			            nn.Conv2d(384, 256, kernel_size=3, padding=1),
			            nn.ReLU(inplace=True),
			            nn.Conv2d(256, 256, kernel_size=3, padding=1),
			            nn.ReLU(inplace=True),
			            nn.MaxPool2d(kernel_size=3, stride=2),
			        )
			        self.avgpool = nn.AdaptiveAvgPool2d((6, 6))
			        self.classifier = nn.Sequential(
			            nn.Dropout(p=0.5),
			            nn.Linear(256 * 6 * 6, 4096),
			            nn.ReLU(inplace=True),
			            nn.Dropout(p=0.5),
			            nn.Linear(4096, 4096),
			            nn.ReLU(inplace=True),
			            nn.Linear(4096, num_classes),
			        )
			        ```
		- *Inception (a.k.a GoogLeNet)*
		- *Transformer*
			- the most practical architecture today. 
			- these can perform any tasks (forecasting/generation/ classification etc.) but,
			- These require a lot of memory space(GPU resources) to conduct; we can't let this architecture learn locally (maybe) and moreover we don't have to do it.
	- optimizers: 
		- SGD
		- momentum SGD
		- RMSprop
		- Ada
		- Adam
		- AdamW
- **Results from investigations**
	- the gradient vector at a time is a I.I.D gaussian source
	- that is, most elements are close to zero, and few elements have value which are far from zero.
	- but 
## Idea
>[!Assumption on the source]
>the gradient vectors $\{\mathbb{g}_t\}$  makes a flow dynamics. 
>that is, $\forall L\in \mathbb{R}, s.t. \mathbb{E}[g_{t+1}-g_{t}]\leq L$ 
- There is no guarantee that this assumption is always true.
- but this holds in most cases
	- because 