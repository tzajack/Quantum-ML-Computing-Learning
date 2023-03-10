# Quantum ML&Computing Learning
Python code for quantum machine learning and Quleaf quantum circuit demostration for quantum computing algorithms


## Quantum Classifier
Apply the quantum classifier to kaggle titanic dataset. 

Original document site:[https://qml.baidu.com/tutorials/machine-learning/quantum-classifier.html](https://qml.baidu.com/tutorials/machine-learning/quantum-classifier.html)

Structure of quantum circuit is similar to [VSQL: Variational Shadow Quantum Learning for Classification](https://doi.org/10.1609/aaai.v35i9.17016)



## Single Qubit QNN
A method to fit function using single qubit circuit.

Original document site:[https://qml.baidu.com/tutorials/machine-learning/quantum-neural-network-approximating-functions.html](https://qml.baidu.com/tutorials/machine-learning/quantum-neural-network-approximating-functions.html)

Differences from the document: add a constant coefficient and a bias to the final output in order to fit functions in wider range


## Deutsch-Joza Algorithm
A demostration of Deutsch-Joza algorithm on Baidu Quleaf

The md file is the explanation of some theory and how to demostrate the algorithm on Quleaf.

Code for build the ciruit in QComposer on Quleaf can be found at Quleaf_Code_balanced and Quleaf_Code_constant


## No Overfit in QNN
A implementation of the overfit-preventing property metioned in the QCL Paper

Original paper:[https://doi.org/10.48550/arXiv.1803.00745](https://doi.org/10.48550/arXiv.1803.00745).(*Relevent content in the last paragraph of part C.Ability to approximate a function*)

Here give a more detailed explanation than the one in the paper:

Let $\\{ P_k \\} = \\{ I,X,Y,Z \\}^{\otimes N}$, a set of Pauli operators.

The input density operator, $\rho_{in}$, can be expand as some combination of $P_k$, i.e. $\rho_{in} = \Sigma_k a_k(x) P_k$ for some coefficient $a_k(x)$ depends on input $x$.

Similarly, the output density operator after $U(\theta)$ can be written in another set of coefficent $b_k(x,\theta)$ combine with $P_k$, $\rho_{out} = \Sigma_k b_k(x,\theta) P_k$.

The Pauli observation taken, $O \in \\{ I,X,Y,Z \\}^{\otimes N}$, has the expectation:

$\langle O \rangle = tr(\rho_{out}O) = tr((\Sigma_k b_k(x,\theta) P_k)O) = tr((b_1 P_1 + b_2 P_2 + ... + b_n P_n)O)$ 

Since $P_1,P_2,...,P_n,B \in \\{ I,X,Y,Z \\}^{\otimes N}$, the product will remain the diagonal elements, hence $\langle O \rangle$ is just the value of $b_m(x,\theta)$

One can find a matrix of element $u_{ij}(\theta)$, such that $b_m(x,\theta) = \Sigma_k u_{m,k}(\theta)a_k(x)$. Hence, the output is linear combination of input coefficient functions $a_k(x)$ with the unitarity constraints of $u_{ij}(\theta)$

In normal regularization, $L = \Sigma_i ||f(x_i)-w*\phi(x_i)||^2 + ||w||^2$, but in this case, $w$  is the row vector $u_i$ and $\phi$ is the coefficient $a_k$. 

**Due to the unitarity of $u_i$, the norm of $u_i$ is a constant. That is, the regularization term is a constant, the model do not have to trade off bewteen regularization term and the loss.**



# Variation Shadow Quantum Learning 

A mixed method of classical fully connected network and quantum networks.

Original paper: [https://doi.org/10.1609/aaai.v35i9.17016](https://doi.org/10.1609/aaai.v35i9.17016)

The code follows the paper mainly so the differences compare to the tutorial of paddle_quantum are:
1. Use the titanic dataset again to avoid long training time(originally done by MINST dataset)
2. Use MSE Loss instead of cross-entropy loss 
3. Use a classical FCNN with output dimenson of $1$ and use sigmoid instead of softmax 


