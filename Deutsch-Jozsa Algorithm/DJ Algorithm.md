# Deutsch-Jozsa Algorithm

## 1.Description of Deutsch-Jozsa game

The referee of the game picks a function $f:\{0,...,M-1\} \rightarrow \{0,1\}$, where $M$ is even.

There are only two types of function $f$:
1. Constant: $f(x)=a$ for some constant $a$
2. Balenced: $N_0=N_1$, where $N_0 = |\{x|f(x)=0\}|$ and $N_0 = |\{x|f(x)=1\}|$.
That is, the number of functions with value $1$ is equal to the number of functions with value $0$.
  
