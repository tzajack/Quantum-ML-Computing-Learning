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

However, quantumly we need only $1$ query.

## 3.Process of Deutsch-Jozsa Algorithm

1. Prepare the system in Fourier state $|e_0\rangle = \frac{|0\rangle + |1\rangle + ... + |M-1\rangle}{\sqrt{M}}$
2. Apply the reduced oracle $V_f$
3. Measure on the Fourier basis $\\{ e_m \\}^{M-1}_{m=0} $
