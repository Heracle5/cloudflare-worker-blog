## RV

### property

- PDF: Continuous-valued RV
  - $\text{p}(z)\ge0$ for all z 

  -  $\int p(z)dz=1$

- PMF: Discrete-valued RV
  - $\text{Pr}\{z=i\}\ge0$ for all i
  - $\sum\limits_{z}\text{Pr}\{z\}=1$

### Distributions

#### Conditional distributions

- Conditional density function: $p(z|x)$:
  - $p(x,z)=p(z|x)p(x)$ 
  - and if $p(x)\neq 0$, $p(z|x)=\frac{p(x,z)}{p(x)}$

#### Total Prob

- Discrete: $\text{Pr}\{z\}=\sum\limits_{x\in S_x}\text{Pr}\{x,z\}=\sum\limits_{x\in S_x}\text{Pr}\{z|x\}\text{Pr}\{x\}$
- Continuous: $p(z)=\int_{x\in S_x}p(x,z)dx=\int_{x\in S_x}p(z|x)p(x)dx$



### Expectation, Covariance, the gaussian distribution

#### Expected value and covariance

- Expected value: $\mathbb{E}\{x\}=\int xp(x)dx$

- Covariance matrix: $\text{Cov}\{x\}=\mathbb{E}\{[x-\mathbb{E}\{x\}][x-\mathbb{E}\{x\}]^T\}$

  

#### Law of Large number

- $\lim\limits_{n\to\infin}\frac{1}{n}\sum\limits_{i=1}^{n}x_i=\mathbb{E}_{p(x)}\{x\}$

   

#### Gaussian Dist

- Pdf: $p(x)=N(x;\mu, Q)=\frac{1}{\sqrt{|2\pi Q|}}\exp{(-\frac{1}{2}(x-\mu)^TQ^{-1}(x-\mu))}$
- Linear comb: $z=Ax+By$, and $\mu_z=\mathbb{E}\{Ax+By\}=A\mu_x+B\mu_y$, and $Q_z=\text{Cov}\{Ax+By\}=\text{Cov}\{Ax\}+\text{Cov}\{By\}+\text{Cov}\{Ax,By\}+\text{Cov}\{By,Ax\}=AQ_xA^T+BQ_yB^T$

## Bayesian Statistics

Suppose we wish to estimate $\theta$ given measurements $y$.
		Key steps in a Bayesian method:

- Modeling. Model what we know about $\theta$ (using a prior $p(\theta)$ ) and the how the measurements $y$ relate to $\theta$ (using a density $p(y \mid \theta)$ ).

- Measurement update. Combine what we knew before (the prior) with our measurement (with $p(y \mid \theta)$, also called the likelihood) to summarize what we know about $\theta(p(\theta \mid y))$.

- Decision making. Given what we know about $\theta$ (described by $p(\theta \mid y))$ and a loss function, we compute an optimal decision.

### Bayes' rule

- conditional prob: $\text{Pr}\{y,\theta\}=\text{Pr}\{y|\theta\}\text{Pr}\{\theta\}$
- Law of total prob: $\text{Pr}\{y\}=\sum\limits_{\theta}\text{Pr}\{y,\theta\}$ (discrete variables), $p(y)=\int_{\theta}p(y,\theta)d\theta$(continuous variables)
- Bayes' rule: $p(y|\theta)p(\theta)=p(\theta|y)p(y)$ $\to\ p(\theta|y)=\frac{p(y|\theta)p(\theta)}{p(y)}$
- ![image-20240320191921011](/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240320191921011.png)
- ![image-20240320191934352](/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240320191934352.png)

![image-20240320192246975](/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240320192246975.png)

Two types of sensors:

$$p(\theta|y_1,y_2)\ p(\theta)p(y_1,y_2|\theta)$$ 

$$p(y_1,y_2|\theta)=p(y_1|\theta)p(y_2|\theta)$$ conditional independent





### Bayesian Decision Theory

#### Principle

- Basic: 
  - Minimize expected loss or equivalently
    - $C(\theta,a)$
    - $\hat{\theta}=\arg\min\limits_{a}\mathbb{E}\{C(\theta,a)|y\}$
    - where $\mathbb{E}\{C(\theta,a)|y\}=\int_\Theta C(\theta,a)p(\theta|y)d\theta$
  - Maximize expected utility
- ![image-20240320194923998](/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240320194923998.png)****

#### MMSE

- parameter estimation: $\theta\in\Theta=\mathbb{R}^n$

- $C(\theta,a)=||\theta-a||_2^2=(\theta-a)^T(\theta-a)$

- Let $\bar{\theta}=\mathbb{E}\{\theta|y\}, P=\text{Cov}\{\theta|y\}=\mathbb{E}\{(\theta-\bar{\theta})(\theta-\bar{\theta})^T|y\}$ <img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240320201240193.png" alt="image-20240320201240193" style="zoom:33%;" />

#### MAP  

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240320201402470.png" alt="image-20240320201402470" style="zoom:33%;" />

##	Filtering\Smoothing\Prediction

### filtering

- $x_k$: parameter of interest

- $y_k$: measurements at time $k$

- compute $p(x_k|y_{1:k})$, where $y_{1:k}\triangleq[y_1,y_2,...,y_k]$(using all the information at and before $t=k$ to estimate $x_k$)

#### example

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325091120843.png" alt="image-20240325091120843" style="zoom:33%;" />

### smoothing and prediction

- Smoothing (n>0): compute $p(x_k|y_{1:k+n})$ using past\current\future
- Prediction(n>0): compute $p(x_k|y_{1:k-n})$ using past

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325092252480.png" alt="image-20240325092252480" style="zoom:33%;" />

## State space models

#### Discrete-time state space models

- $x_k=\text{f}_{k-1}(x_{k-1},q_{k-1})$

- $y_k=h_k(x_k,r_k)$
- $x_0\sim p(x_0)$
- $q_{k-1}$: motion noise./$r_k$: measurement noise

#### Process/motion model

- $x_k=\text{f}_{k-1}(x_{k-1},q_{k-1})$ describe the state evolution $p(x_k|x_{k-1})$, the distribution of $x_k$ given $x_{k-1}$
- How much changes we allowed are modeled by the motion model.

#### measurement model/sensor model

- $y_k=h_k(x_k,r_k)$ describes the distribution of $y_k$ given $x_k$, $p(y_k|x_k)$, also likelihood function.
- relating data(x_k) to the state vector(y_k) and helping us to use data to learn about the states.
- <img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325100833470.png" alt="image-20240325100833470" style="zoom:33%;" />

#### Conditional independencies in state space models

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325102439711.png" alt="image-20240325102439711" style="zoom:33%;" />

#### Bayesian networks

probabilistic graphical model

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325103438310.png" alt="image-20240325103438310" style="zoom:33%;" />

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325104405331.png" alt="image-20240325104405331" style="zoom:12%;" />

### Optimal filtering

- objective in filtering: compute $p(x_k|y_{1:k})$ for k=1,2,3,...
- <img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325105612354.png" alt="image-20240325105612354" style="zoom:33%;" />

- <img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325105838659.png" alt="image-20240325105838659" style="zoom:33%;" />
  - Pred.-motion model
  - Update- measurement model
- <img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325111515113.png" alt="image-20240325111515113" style="zoom:33%;" />

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325111841824.png" alt="image-20240325111841824" style="zoom:33%;" />

<img src="/Users/hangjenchan/Library/Application Support/typora-user-images/image-20240325112407718.png" alt="image-20240325112407718" style="zoom:33%;" />
