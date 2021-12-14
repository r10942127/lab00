# **LCMV Beanforming**
The weight vector for the linearly constrained minimum variance beamformer is thesolution to the following optimization problem.
$$
\begin{split}
{\bf w}_{\rm LCMV} = &\mathop{\arg\min}\limits_{\bf w} \mathbb{E}[|y(t)|^2]\\&{\rm subject\ to}&{\bf C}^{H}{\bf w} = {\bf g},
\\&{\rm where} &y(t) = {\bf w}^H{\bf x}(t),
\\&&{\bf C} = [{\bf a}(\omega_i,\theta_j) \ {\bf a}(\omega_k,\theta_l)...].
\end{split}
$$
### **Wideband Beamforming using ULA&TDL structure**
${\scriptsize Hint: x_0(t)\ here\ represents\ the\ signal\ received\ by\ the\ uppermost\ sensor,\ \theta >0\ if\ signal\ is\ from\ upside.}$
![](https://i.imgur.com/WkZpGkm.png =30%x)
$\qquad \qquad$figure(1)

$x_m(t)=x_0(t)e^{-j\omega m\tau_1(\theta)},\ \tau_1(\theta)=\dfrac{dsin(\theta)}{\lambda}$

$$
\begin{split}
{\bf a}(\omega_i,\theta_j) = 
[&e^{-j\omega_i\tau_0(\theta_j)},e^{-j\omega_i\tau_1(\theta_j)},...,e^{-j\omega_i\tau_{M-1}(\theta_j)},
\\&e^{-j\omega_i(\tau_0(\theta_j)+Ts)},e^{-j\omega_i(\tau_1(\theta_j)+Ts)},...,e^{-j\omega_i(\tau_{M-1}(\theta_j)+Ts)},
\\&...,e^{-j\omega_i(\tau_0(\theta_j)+(J-1)Ts)},e^{-j\omega_i(\tau_1(\theta_j)+(J-1)Ts)},...,e^{-j\omega_i(\tau_{M-1}(\theta_j)+(J-1)Ts)}]^{T}
\end{split}
\\
\begin{split}
Ts\le\dfrac{T_{min}}{2}\ or\ Ts\le\dfrac{1}{2f_{max}},f_{max}\ {\rm represent\ the\ highest\ frequency\ of\ received\ signal}  
\end{split}
$$
![](https://i.imgur.com/C52P8We.png =80%x)
$\qquad \qquad \qquad \qquad \qquad \qquad$figure(2)
### **Example: MVDR**
**Target: make the response of desired DOA constant.**

In this book, author suggests the DOA of desired signal all from the broadside, i.e. $\theta$=0 in figure(1).
#### **Pre-steering**
If the DOA is not from broadside, author suggests imposing appropriate time delays for each sensor output.

After pre-steering, the signals entering the array are all from broadside,i.e.$x_0[n]=x_1[n]=...=x_{M-1}[n]$. Then, the conventional wideband TDL structure, shown in figure(2), would turn into figure(3). 

![](https://i.imgur.com/wAHJxxl.png =80%x)
$\qquad \qquad \qquad \qquad \qquad \qquad$figure(3)
$$
f[l]= \displaystyle\sum_{k=0}^{M-1} w_{k,l}
$$Then, take $f[0]$ for example :
$\qquad\begin{split}
f[0]=&1\times {\rm w}_{0,0}+1\times {\rm w}_{1,0}+...+1\times {\rm w}_{M-1,0}+
\\&0\times {\rm w}_{0,1}+0\times {\rm w}_{1,1}+...+0\times {\rm w}_{M-1,1}+
\\&0\times ...+0\times {\rm w}_{M-1,J-1}
\\=&{\bf (C[0:MJ-1][0])}^H{\bf w}
\end{split}$
$\qquad$In this case, ${\bf C[0:M-1][0]}=1,\ {\bf C[M:MJ-1][0]}=0,\ {\bf g}[0] = f[0]$
We could form the entire ${\bf C}$ in the end,
$${\bf C} = 
\begin{bmatrix}
{\bf c_0}\qquad {\bf 0}
\\
\ddots
\\
{\bf 0}\qquad {\bf c_0}
\end{bmatrix}\in{\bf C}^{MJ\times J}
\\{\bf c_0}=[1...1]^T\in{\bf C}^{M\times 1}
$$
If we let $f[0]=f[1]=...=f[J-1]=1$, it equals to ${\bf g}[0]={\bf g}[1]=...={\bf g}[J-1]=1$, which means **the desired gain from broadside at all frequency equals to 1**.
### **Optimum Solution to the LCMV Problem**
we can change $\mathbb{E}[|y(t)|^2]$ into ${\bf w}^H{\bf R_{xx}w}$.
By the method of Lagrange multipliers, the Lagrangian is 
$$
\begin{split}
L=&{\bf w}^H{\bf R_{xx}w}+Re\{\lambda^H({\bf C}^{H}{\bf w-g})\}
\\
=&{\bf w}^H{\bf R_{xx}w}+\frac{{\lambda}^H}{2}\{{\bf C}^{H}{\bf w-g}\}+\frac{{\lambda}^T}{2}\{{\bf C}^{T}{\bf w^*-g^*}\}
\end{split}
$$
Then,
$$
\frac{\partial L}{\partial {\bf w^*}}={\bf R_{xx}w}+{\bf C\frac{{\lambda}^T}{2}}=0
$$
Therefore, $${\bf w_{opt}}={-\bf R_{xx}^{-1}C\frac{\lambda}{2}}$$
Next, since
$$
{\bf C}^{H}{\bf w_{opt}} = {\bf g},
\\
{\bf -C}^{H}{\bf R_{xx}^{-1}C\frac{\lambda}{2}} = {\bf g}
$$Finally, we replace the ${\lambda}$ in the derivation of ${\bf w_{opt}}$, and get 
$$
{\bf w_{opt}}={\bf R_{xx}^{-1}C(C^HR_{xx}^{-1}C)^{-1}g}
$$





