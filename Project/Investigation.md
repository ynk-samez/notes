## Classical Methods
- dot-product coding 
	- Parameters

		- Gradient of NN: g_ ∈R^D

		- Random Vector: r_ ∈R^D

	- Steps

		- Shared : r

		- Send : c=g^T r∈R

		- Estimate : g from c and r

- Pros/Cons

lAdvantage: compression rate ↑( R^D to R^1)

lDisadvantage: accurecy↓, hard to estimate

lAn improvement for dot-product coding

lStep

lShared:{r_i∈R^D |r_1,r_2,⋯r_n}

lSend:  c_1=g^T r_1, c_2=g^T r_2, ⋯c_n=g^T r_n

lEstimate: g from {c_1,c_2,⋯c_n} and {r_1,r_2,⋯r_n}

lPros/Cons

lAdvantage: Accuracy↑

lDisadvantage: Compression rate ↓


### Adam(Adaptive )

![[Pasted image 20251230114616.png]]
## Concept
- Switch **1-dimensional compression** and  **normal lattice quantization** 
	- $cos(g_t,g_{t+1})\sim 1$  part : we just send the norm of the 2nd difference of the gradient vectors of NN. 
	- $\cos(g_t, g_{t+1})<<1$ part: we have to send  the 2nd difference vectors.
## History of Weight Forecasting/ Accelaration for Neural Networks
- Introspection (2017)
- WNN; Weight Nowcaster Network (2023)
	- periodic skip steps 
	- good for short-range, bad for long-range forecasting
- Farcasting with LFD-2(2024)
- NiNo (2025)
	- a graph-based approach
- Introduce some assumptions
	- we can consider "Flow-based and Time-continuous model"
	- this approach intepret the gradient update as a dynamics which is constrainted by an ODE(Ordinary Differecial Equation)
		- Neural ODE(2018)
			- computationally expensive due to the need for numerical integration
			- not good for high-dimensional models
	-  While we adopt Gaus-

sian initialization for theoretical convenience, modern deep learning models often employ more

structured initialization schemes

```mermaid
graph TD;
    %% Node Definitions
    Start((Start Training Step))
    Grad[Compute Local Gradient: g]
    Pred[Generate Prediction: g_pred = g * m / m]
    Diff[Extract High-Frequency Residual: δ = g - g_pred]
    
    %% Decision Logic (Annulus/Nested Strategy)
    Judge{Check Residual Norm: δ}
    HighRes[Mode: High-Resolution Lattice]
    LowRes[Mode: Low-Resolution Lattice]
    
    %% Quantization Process
    Quant[Quantize δ into Lattice Index: I]
    Trans[Transmit: Index I + Norm g + Mode Flag]
    
    %% Server Side
    Server[Server Receives Packet]
    Dequant[De-quantize I to retrieve δ_hat]
    Recover[Recover Gradient: g_hat = g_pred + δ_hat]
    Update[Update Global Model & Momentum m]
    Sync((Sync Next Step))

    %% Connections
    subgraph Client-Side
	    Start --> Grad
	    Grad --> Pred
	    Grad --> Diff
	    Pred --> Diff
	    Diff --> Judge
	    
	    Judge -- "δ < R_min (Convergence) OR δ > R_max (Abnormal)" --> HighRes
	    Judge -- "R_min < ||δ|| < R_max (Steady State)" --> LowRes
	    
	    HighRes --> Quant
	    LowRes --> Quant
	end
	subgraph Server-Side
	    Quant --> Trans
	    Trans --> Server
	    Server --> Dequant
	    Dequant --> Recover
	    Recover --> Update
	    Update --> Sync
	end
```