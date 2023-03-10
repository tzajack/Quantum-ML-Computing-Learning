# Deutsch-Jozsa Algorithm

## 1.Description of Deutsch-Jozsa game

The referee of the game picks a function $f: \\{ 0,...,M-1 \\} \rightarrow  \\{ 0,1 \\}$, where $M$ is even.

There are only two types of function $f$:
1. Constant: $f(x)=a$ for some constant $a$
2. Balanced: $N_0=N_1$, where $N_0 = | \\{ x|f(x)=0 \\}|$ and $N_0 = | \\{ x|f(x)=1 \\} |$.
That is, the number of functions with value $1$ is equal to the number of functions with value $0$.
  
The player can select an arbitary $t \in \\{ 0,...,M-1 \\}$ and ask the referee the value of $f(t)$.

The player's goal is to find out whether the function picked is **constant** or **balanced**.

## 2.Query complexity

Classically, the worst case, we need to ask the referee $\frac{M}{2}+1$ times.

However, quantumly we need only $1$ quantum query.

## 3.Process of Deutsch-Jozsa Algorithm

1. Prepare the system in Fourier state $|e_0\rangle = \frac{|0\rangle + |1\rangle + ... + |M-1\rangle}{\sqrt{M}}$
2. Apply the reduced oracle $V_f$
3. Measure on the Fourier basis $\\{ e_m \\}^{M-1}_{m=0} $ 

   If the outcome is $0$, the function is **constant**.
   If the outcome is not $0$, the function is **Balanced**.
   
## 4.Simulation on Quleaf
Let take $M=4$ as an example.

We need $2$ qubits to demostrate the algorithm.

The initial state of Quleaf on each qubit is always $|0 \rangle$, so apply two $H$ gate will prepare the superposition of all possible input states.

![](https://github.com/tzajack/QuantumLearning/blob/main/Deutsch-Jozsa%20Algorithm/1.PNG)

The state after reduced oracle is:

$$
V_f|e_0 \rangle = \frac{\Sigma^{M-1}_{x=0} (-1)^{f(x)} |x \rangle  }{\sqrt(M) } 
$$

We rewrite this equation with $M=4$ case: 

$$
V_f|e_0 \rangle = \frac{(-1)^{f(0)}|00\rangle + (-1)^{f(1)}|01\rangle + (-1)^{f(2)}|10\rangle + (-1)^{f(3)}|11\rangle}{\sqrt{M}}
$$

Here, we rewrite the states with binary number with:

$$
|00\rangle = 
\begin{pmatrix}
1 \\ 0 \\ 0 \\ 0
\end{pmatrix} ^T
$$

$$
|01\rangle = 
\begin{pmatrix}
0 \\ 1 \\ 0 \\ 0
\end{pmatrix} ^T
$$

$$
|10\rangle = 
\begin{pmatrix}
0 \\ 0 \\ 1 \\ 0
\end{pmatrix} ^T
$$

$$
|11\rangle = 
\begin{pmatrix}
0 \\ 0 \\ 0 \\ 1
\end{pmatrix} ^T
$$

### 4.1 Balanced Case
If the function is **balanced**, then $2$ of the functions value is $1$, the other $2$ functions' value is $0$.

WLOG. we can set $V_f|e_0 \rangle$ with:
```math

 \frac{1}{\sqrt{M}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix} 
```

This state can be prepared by adding a $Z$ gate on the first qubit:

![](https://github.com/tzajack/QuantumLearning/blob/main/Deutsch-Jozsa%20Algorithm/2.PNG)

This is because the corresponding matrix is :
```math
Z\otimes I = \begin{pmatrix} 1 & 0  \\ 0 & -1  \end{pmatrix} \otimes \begin{pmatrix} 1 & 0  \\ 0 & 1  \end{pmatrix} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & -1 & 0 \\ 0 & 0 & 0 & -1 \end{pmatrix} 
```

We then add two $H$ gate and an observation:

![](https://github.com/tzajack/QuantumLearning/blob/main/Deutsch-Jozsa%20Algorithm/3.PNG)

Recall that outcome of this circuit should be always $1$(not $0$) as we previously defined. Let's run the circuit on Quleaf.

![](https://github.com/tzajack/QuantumLearning/blob/main/Deutsch-Jozsa%20Algorithm/4.PNG)

We can see that for $1000$ simulation, the result is always $1$.

Code for QComposer can be found at 'Quleaf_Code_balanced'.
### 4.2 Constant Case
If the function is **constant**, $V_f|0 \rangle$ becomes:
```math

 \frac{\pm 1}{\sqrt{M}} \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} 
```

Since the 'up to same state' property, the result is just the identity. Hence, we just replace $Z\otimes I$ with $I \otimes I$.

![](https://github.com/tzajack/QuantumLearning/blob/main/Deutsch-Jozsa%20Algorithm/5.PNG)

Recall that we should always get result $0$.

![](https://github.com/tzajack/QuantumLearning/blob/main/Deutsch-Jozsa%20Algorithm/6.PNG)

We can see that the simulation result agrees with our theory.

Code for QComposer can be found at 'Quleaf_Code_constant'.


