## Pure state

**Pure state** of a many-body wavefunction
$$
|\Psi\rangle=\sum_{\mathbf{s}} \Psi^{s_{1} s_{2} s_{3} \cdots s_{N}}\left|s_{1} s_{2} s_{3} \cdots s_{N}\right\rangle
$$
where the amplitude is a N-order tensor. 

> For a simple two-body pure state $|\psi\rangle_{AB}=\Psi^{s_1s_2}|s_1s_2\rangle= a|0\rangle_A\otimes|0\rangle_B + b|1\rangle_A\otimes|1\rangle_B$, the second-order tensor is
> $$
> \Psi^{s_1s_2}=\left(\begin{matrix}a&0\\0&b\end{matrix}\right)
> $$
> The reduced density matrix of system A is
> $$
> \begin{align}
> \rho^{s_1'}_{s_1}&\equiv\text{Tr}_B\left(|\psi\rangle_{AB}\ _{AB}\langle\psi|\right)=\sum_{s_2}\Psi^{s_1's_2}\Psi_{s_1s_2}=\Psi\Psi^\dagger\\&=\left(\begin{matrix}|a|^2&0\\0&|b|^2\end{matrix}\right)=|a|^2|0\rangle_A\ _A\langle0|+|b|^2|1\rangle_A\ _A\langle1|
> \end{align}
> $$
> <img src="figures/SecondOrderTensor.png"   style="width:100px"/>

For a more general case, we can define Many-Body Entanglement by dividing sites into region "A" and "B":

<img src="figures/ManyBodyTN.png"   style="width:300px"/>

Trace over region B to get reduced density matrix of A:

<img src="figures/ManyBodyTN2.png"   style="width:300px"/>

Diagonalize $\rho_A$ to get eigenvalues

<img src="figures/ManyBodyTN3.png"   style="width:300px"/>

where 
$$
P=\left(\begin{matrix}p_1&&\\&p_2&\\&&\ddots\end{matrix}\right)
$$
Then use $S_{\mathrm{vN}}=-\sum_{n} p_{n} \ln \left(p_{n}\right)$ to compute the von Neumann entanglement entropy.

A **many-body pure state** can be divided into two categories: **Product state** and **Entangled state**.

#### Product state

states with no entanglement:

1. Simple example

$$
|\Psi\rangle=|\uparrow \uparrow\rangle=|\uparrow\rangle|\uparrow\rangle
$$

with $\rho_A=\left(\begin{matrix}1&0\\0&0\end{matrix}\right)$, von Neumann entanglement entropy $S_{vN}=0$.

2. Another product state (not obvious in $z$ basis though):

$$
\begin{aligned}|\Psi\rangle &=|\uparrow\rangle|\rightarrow\rangle \\ &=|\uparrow\rangle\left(\frac{1}{\sqrt{2}}|\uparrow\rangle+\frac{1}{\sqrt{2}}|\downarrow\rangle\right) \\ &=\frac{1}{\sqrt{2}}|\uparrow\rangle|\uparrow\rangle+\frac{1}{\sqrt{2}}|\uparrow\rangle|\downarrow\rangle \end{aligned}
$$

with $\rho_A=\left(\begin{matrix}1&0\\0&0\end{matrix}\right)$, von Neumann entanglement entropy $S_{vN}=0$.

3. The state
   $$
   |\Psi\rangle=\frac{1}{2}\left(|\uparrow\rangle|\uparrow\rangle+|\uparrow\rangle|\downarrow\rangle+|\downarrow\rangle|\uparrow\rangle+|\downarrow\rangle|\downarrow\rangle\right)=\frac{1}{2}|\uparrow+\downarrow\rangle_A|\uparrow+\downarrow\rangle_B
   $$
   with $\rho_A=\left(\begin{matrix}1/2&1/2\\1/2&1/2\end{matrix}\right)$, must be diagonalized to get eigenvalues:
   $$
   \rho_{1}=\left[\begin{array}{cc}{1 / 2} & {1 / 2} \\ {1 / 2} & {1 / 2}\end{array}\right]=\frac{1}{\sqrt{2}}\left[\begin{array}{cc}{1} & {-1} \\ {1} & {1}\end{array}\right]\left[\begin{array}{ll}{\mathbb{1}} & {0} \\ {0} & {0}\end{array}\right]\left[\begin{array}{cc}{1} & {1} \\ {-1} & {1}\end{array}\right] \frac{1}{\sqrt{2}}
   $$
   von Neumann entanglement entropy $S_{vN}=0$.

#### Entangled state

States that cannot be written as a product state in any basis transformation of individual sites:

1. Singlet state :

$$
|\Psi\rangle=\frac{1}{\sqrt{2}}|\uparrow\rangle|\downarrow\rangle-\frac{1}{\sqrt{2}}|\downarrow\rangle|\uparrow\rangle
$$

with $\rho_A=\left(\begin{matrix}1/2&0\\0&1/2\end{matrix}\right)$, von Neumann entanglement entropy $S_{vN}=1$bit.

2. The state
   $$
   |\psi\rangle_{AB}=a|0\rangle_A\otimes|0\rangle_B + b|1\rangle_A\otimes|1\rangle_B
   $$
   with $\rho_A=\left(\begin{matrix}|a|^2&0\\0&|b|^2\end{matrix}\right)$, von Neumann entanglement entropy $S_{vN}=-|a|^2\log|a|^2-|b|^2\log|b|^2$bit.

## [Pauli Matrix basis v.s. Bloch vector representation](https://arxiv.org/pdf/1602.01548.pdf)

Probabilistic mixtures of single qubit quantum states can be represented by a density matrix[^Neumann1927]. The density matrix may be written in the **Pauli Matrix basis**, with the coefficients making up the **Bloch vector**[^Bloch1946]. The latter has the simple geometry of a vector inside a unit Bloch sphere, whose magnitude indicates the state’s purity, and whose rotations are unitary transformations.

For two-level systems, we study the extended Pauli matrices; with the identity matrix added,
$$
\begin{aligned} 
\sigma_{0} &=\left(\begin{array}{cc}{1} & {0} \\ {0} & {1}\end{array}\right)=I, & 
\sigma_{1}=\left(\begin{array}{cc}{0} & {1} \\ {1} & {0}\end{array}\right) \\ \sigma_{2} &=\left(\begin{array}{cc}{0} & {-i} \\ {i} & {0}\end{array}\right), & \sigma_{3}=\left(\begin{array}{cc}{0} & {1} \\ {1} & {0}\end{array}\right) \end{aligned}
$$
The Pauli matrices form a set of generators for the group of 2×2 special unitary matrices SU(2). Along with the identity, they constitute **a complete basis** of the space of 2×2 Hermitian matrices over the real numbers.

Pauli matrices satisfy the following well-known product, commutation, and anticommutation relations
$$
\begin{align} \sigma_{i} \sigma_{j} &=\delta_{i j} I+i \varepsilon_{i j k} \sigma_{k} \\\left[\sigma_{i}, \sigma_{j}\right] &=2 i \varepsilon_{i j k} \sigma_{k} \\\left\{\sigma_{i}, \sigma_{j}\right\} &=2 \delta_{i j} I \end{align}
$$
To generalize to higher dimensions, we wish to extend them to include $\sigma_0$. One can verify by trial that the four matrices satisfy the following product identity
$$
\sigma_{\alpha} \sigma_{\beta}=\left(\theta_{\alpha \beta \gamma}+i \varepsilon_{\alpha \beta \gamma}\right) \sigma_{\gamma}\label{productIdentity}
$$
where the third order tensors
$$
\theta_{\alpha \beta \gamma} \equiv\left\{\begin{array}{ll}{1} & {\text { one index is } 0, \text { the other two equal }} \\ {0} & {\text { otherwise }}\end{array}\right.
$$
and
$$
\varepsilon_{\alpha \beta \gamma} \equiv\left\{\begin{array}{cl}{1} & {\alpha \beta \gamma \in\{123,231,312\}} \\ {-1} & {\alpha \beta \gamma \in\{321,213,132\}} \\ {0} & {\text { repeated indices, or any index is } 0}\end{array}\right.
$$
Take the trace of Eq.($\ref{productIdentity}$) we derive the **orthogonality relation of Pauli matrices**（**Pauli矩阵作为basis的正交性含义**）:
$$
\begin{array}{}\operatorname{Tr}\left(\sigma_{\alpha} \sigma_{\beta}\right) &=\left(\theta_{\alpha \beta \gamma}+i \varepsilon_{\alpha \beta \gamma}\right) 2 \operatorname{Tr}(\sigma_{\gamma}) \\ &=\left(\theta_{\alpha \beta \gamma}+i \varepsilon_{\alpha \beta \gamma}\right) 2 \delta_{\gamma 0} \\ &=2\left(\theta_{\alpha \beta 0}+i \varepsilon_{\alpha \beta 0}\right) \\ &=2 \delta_{\alpha \beta} \label{orthogonality}\end{array}
$$

### Single system: Single qubit

For a **single qubit**, we can express the 2×2 density matrix **in the Pauli matrix basis**,
$$
\rho=\frac{1}{2}\left(I+r_{i} \sigma_{i}\right)=\frac{1}{2} r_{\mu} \sigma_{\mu}
$$
where the scalar $r_0$ is always unity to ensure $\text{Tr}\rho=1$, and scalars $r_1$, $r_2$, and $r_3$ are the components of the Bloch vector[^Bloch1946], denoted $\vec{r}= (r_1, r_2, r_3)$. Since $\rho$ is Hermitian, $r_i$ are always real.  Because of the orthogonality relation of the four Pauli matrices in Eq.($\ref{orthogonality}$), the Bloch vector is given by
$$
r_\mu=\text{Tr}(\rho\sigma_\mu)
$$
As an alternative representation of the quantum state, the Bloch vector has some advantages over the density matrix.  The purity of the density matrix  is at most unity
$$
1 \geq \operatorname{Tr} \rho^{2}=r_{\mu} r_{\nu} \operatorname{Tr}\left(\sigma_{\mu} \sigma_{\nu}\right) / 4=\left(1+\|\vec{r}\|^{2}\right) / 2
$$
implying $\|\vec{r}\|^{2}\leq1$. . Hence, the Bloch vector lies inside a sphere of unit radius, known as the **Bloch sphere**. Unitary transformations on the density matrix are interpreted as rotations in the Bloch vector picture. Any unitary operator $U$ in two dimensions can be written
$$
U_{\hat{a},\alpha}=\cos\frac{\alpha}{2}I-i\sin\frac{\alpha}{2}a_i\sigma_i
$$

> **Proof**: In the Pauli matrix basis, any finite rotation of magnitude $\alpha$ along axis $\hat{a}=(\sin\theta\cos\varphi,\sin\theta\sin\varphi,\cos\theta)$ is
> $$
> \begin{aligned}
> R(\hat{a}, \theta)&=\exp(−i\theta\hat{a}\cdot \vec{J})=\exp(−i\frac{\theta}{2}\hat{a}\cdot \vec{\sigma})\\
> &=\exp\left[-i\frac{\theta}{2}\begin{pmatrix} \cos\theta&\sin\theta e^{-i\varphi}\\\sin\theta e^{i\varphi}&-\cos\theta\end{pmatrix}\right]
> =\sum_{k=0}^\infty\frac{\left(-i\frac{\theta}{2}\right)^k\begin{pmatrix} \cos\theta&\sin\theta e^{-i\varphi}\\\sin\theta e^{i\varphi}&-\cos\theta\end{pmatrix}^k}{k!}
> \\&=\sum_{p=0}^\infty\frac{\left(\frac{\theta}{2}\right)^{2p}(-1)^pI}{(2p)!}-i\sum_{p=0}^\infty\frac{\left(\frac{\theta}{2}\right)^{2p+1}(-1)^p\hat{a}\cdot \vec{\sigma}}{(2p+1)!}
> \\&=\cos\frac{\theta}{2}I-i\sin\frac{\theta}{2}\hat{a}\cdot \vec{\sigma}\ \blacksquare
> \end{aligned}
> $$

A unitary transformation on the density matrix leaves $I$ unchanged, but modifies the Bloch vector term $r_i\sigma_i$. Writing $c=\cos\frac{\alpha}{2},\ s=\sin\frac{\alpha}{2}$, we find the new Bloch vector $\vec{r'}$ after applying a unitary transformation on the Bloch vector is
$$
\begin{array}{l}r'_{j} \sigma_{j}\equiv U r_{j} \sigma_{j} U^{\dagger}&=\left(c I-i s a_{i} \sigma_{i}\right)\left(r_{j} \sigma_{j}\right)\left(c I+i s a_{k} \sigma_{k}\right) / 2 \\ &=r_{j}\left(c^{2} \sigma_{j}-i \operatorname{csa}_{i}\left[\sigma_{i}, \sigma_{j}\right]+s^{2} a_{i} a_{k} \sigma_{i} \sigma_{j} \sigma_{k}\right) \\ &=r_{j}\left(c^{2} \sigma_{j}+2 c s \varepsilon_{i j k} a_{i} \sigma_{k}+2 s^{2} a_{j} a_{i} \sigma_{i}-s^{2} \sigma_{j}\right) \\ &=r_{j}\left(\cos \alpha \sigma_{j}+(1-\cos \alpha) a_{j} a_{i} \sigma_{i}+\sin \alpha \varepsilon_{i j k} a_{i} \sigma_{k}\right) \\ &=\left(\cos \alpha \delta_{i j}+(1-\cos \alpha) a_{i} a_{j}+\sin \alpha \varepsilon_{k j i} a_{k}\right) r_{j} \sigma_{i}\end{array}
$$
where in the third line, we used the identity $\sigma_{i} \sigma_{j} \sigma_{k} \equiv \delta_{i j} \sigma_{k}-\delta_{i k} \sigma_{j}+\delta_{j k} \sigma_{i}+i \varepsilon_{i j k} I$. We see that $r'_i$ is equal to the terms that multiply $\sigma_i$ in the last line. In vector notation
$$
\begin{aligned} \vec{r}^{\prime} &=\left(\cos \alpha I+(1-\cos \alpha) \hat{a} \hat{a}^{\dagger}+\sin \alpha\lfloor\hat{a}\rfloor_{\times}\right) \vec{r} \\ &=Q(\hat{a}, \alpha) \vec{r} \end{aligned}
$$
where $\hat{a} \hat{a}^{\dagger}$ is an outer product, and $\lfloor\hat{a}\rfloor_{\times}=\begin{pmatrix} 0&-a_3&a_2\\a_3&0&-a_1\\-a_2&a_1&0\end{pmatrix}$ is the cross product matrix of $\hat{a}$ (i.e. $\lfloor\hat{a}\rfloor_{\times}\vec{b}=\hat{a}\times\vec{b},\ \forall\vec{b}$). b). We identified the bracketed terms as the rotation matrix $Q(\hat{a}, \alpha)$, which rotates vectors by the angle $\alpha$ around $\hat{a}$. The rotation is more evident if we rewrite it as
$$
\vec{r}^{\prime}=(\vec{r} \cdot \hat{a}) \hat{a}+\cos \alpha(\vec{r}-(\vec{r} \cdot \hat{a}) \hat{a})+\sin \alpha \hat{a} \times \vec{r}
$$
The first term is the projection of $\vec{r}$ onto $\hat{a}$, left unchanged by the rotation. The two other terms are of equal magnitude, perpendicular to each other and to the first. They constitute the rotated component of $\vec{r}$.

A final interesting property of the Bloch vector is that expectation values become inner products. ducts. A generic qubit observable can be written $O=sI+\vec{c}\cdot\vec{\sigma}$, for some scalar $s$ and vector $\vec{c}$. 
$$
\langle O\rangle=\operatorname{Tr}[\rho O]=\frac{1}{2}\left(2 s+r_{i} c_{j} \operatorname{Tr}\left[\sigma_{i} \sigma_{j}\right]\right)=s+\vec{r} \cdot \vec{c}
$$

>**Example**: 
>
>An example is from Preskill's "Physics 219Computer Science 219" lecture notes (Chapter 2), the expectation value of operator $(\hat{n} \cdot \vec{\boldsymbol{\sigma}})$  under a generic state $\rho$ is
>$$
>\langle\hat{n} \cdot \vec{\boldsymbol{\sigma}}\rangle_{\rho}=\operatorname{tr}[(\hat{n} \cdot \vec{\boldsymbol{\sigma}} )\rho]=\operatorname{tr}\left(\frac{1}{2}\hat{n} \cdot \vec{\boldsymbol{\sigma}}+\frac{1}{2}(\hat{n} \cdot \vec{\boldsymbol{\sigma}})(\vec{r} \cdot \vec{\boldsymbol{\sigma}})\right)=\operatorname{tr}\left(\frac{1}{2}n_i\sigma_ir_j\sigma_j\right)=\hat{r} \cdot \vec{n}
>$$
>This means, if there are many identically prepared systems of state $\rho$, we can determine $\vec{r}$ (and hence the complete density matrix $\rho(\vec{r})$) by measuring $\langle\hat{n}_k\cdot\vec{\sigma}\rangle$ along each of three linearly independent axes $\hat{n}_k$. $\blacksquare$

### Single system: Single qutrit

Given the usefulness of the Bloch vector representation, some authors have generalized it to a qutrit system. They write the 3×3 density matrix $\rho$ as
$$
\rho=\frac{1}{3}\left(I+\sum_{m=1}^{8} r_{m} G_{m}\right)
$$
where $G_m$ are the Gell-Mann matrices. The $G_m$ are Hermitian, traceless, and satisfy the orthogonality relation $\text{Tr}[G_mG_n]=2\delta_{mn}$. However they are not unitary like the Pauli matrices, and the equivalence between unitary transformations and rotations does not hold. 【We do not discuss too much here.】

### Two-qubit system

For a single four-level system, or more commonly, a pair of coupled two-level systems (two qubits), we can use either **16 Gell-Mann-like matrices**, or **16 Dirac matrices** denoted $D_{\mu\nu}=\sigma_\mu\otimes\sigma_\nu$, as our basis.

- **16 Gell-Mann-like matrices**: the basis in these papers[^Jakóbczyk2001] is a generalization of the Gell-Mann matrices with complicated structure constants, resulting in a 15-dimensional space of allowable Bloch vectors with little useful symmetry. It's convenient to take as a basis in n-dimensional Hilbert space the matrices: $I_n, \lambda_1,\lambda_2,\cdots,\lambda_{n^2-1}$ where $\lambda_k$ are the generators of $SU(n)$ satisfying
  $$
  \text{Tr}\lambda_k=0,\ \text{Tr}(\lambda_k\lambda_l)=2\delta_{kl}
  $$
  Since every unitary operator with unit trace can be written as $\rho=\frac{1}{n}I+\frac{1}{2}\sum_{k=1}^{n^2-1}\alpha_k\lambda_k$, the Bloch vector $\vec{r}$ is a **15-dimensional vector**.

- **16 Dirac matrices**: they form a 16-element basis for the space of 4×4 Hermitian matrices. Excluding the identity $D_{00}$, the remaining 15 matrices constitute a set of generators for the group of special unitary 4×4 matrices, SU(4).

  <img src="figures/DiracMatrices.png"   style="width:500px"/>

The Dirac matrices satisfy the orthogonality relation（**双粒子体系Dirac matrix basis正交性含义**）
$$
\text{Tr}(D_{\alpha\beta}D_{\gamma\delta})=4\delta_{\alpha\gamma}\delta_{\beta\delta}
$$
The product, the commutator, and the anticommutator are also given in the paper. 

Writing the density matrix in the **Dirac basis**
$$
\rho=\frac{1}{4}r_{\mu\nu}D_{\mu\nu}
$$
where the scalar coefficients $r_{\mu\nu}$ constitute the 16 entries of the Bloch matrix $\vec{\vec{r}}$. Note here $\vec{\vec{r}}$ is a **second-order 4×4 tensor** instead of **15-dimensional vectors**! 

The orthogonality relation implies the Bloch matrix entries are accessible as the expectation values of tensor products of local observables, as per
$$
r_{\mu \nu}=\operatorname{Tr}\left(\rho D_{\mu \nu}\right)=\left\langle\sigma_{\mu} \otimes \sigma_{\nu}\right\rangle
$$
For $\rho$ to be a density matrix, it is necessary and sufficient that it be Hermitian, of unit trace, and positive semidefinite. The first two conditions imply $\vec{\vec{r}}$ is real and $r_{00}=1$.

**Examples**:

- The maximally mixed state, $\rho=I/4$, has a Bloch matrix where all the entries except $r_{00}$ are zero.
- Product state, $\rho = \rho_1\otimes\rho_2$, has no classical

## How to quantify entanglement?

A **pure state of a pair of quantum systems** is entangled if it is unfactorizable, e.g., the singlet state of two spin-1/2 particles, $\frac{1}{\sqrt{2}}(|\uparrow\downarrow\rangle-|\downarrow\uparrow\rangle)$.

A **mixed state of a pair of quantum systems** is entangled if it cannot be represented as a mixture of factorizable pure states. 

#### [Entropy of entanglement](](https://www.quantiki.org/wiki/entropy-entanglement-0))

The **entropy of entanglement** is an entanglement measure for a **bipartite pure states**. It is defined as the von Neumann entropy of one of the reduced states. That is, for a pure state $\rho_{AB}=∣\Psi\rangle\langle\Psi|_{AB}$, it is given by: 
$$
E(\rho) ≡ S(\rho_A) = S(\rho_B)
$$
where $\rho_A=\text{Tr}_B(∣\Psi\rangle\langle\Psi∣)$ and similar for $ρ_B$.

Many entanglement measures reduce to the **entropy of entanglement** when evaluated on pure states. Among those are:

- Distillable entanglement
- Entanglement cost
- Entanglement of formation
- Relative entropy of entanglement
- Squashed entanglement

Some entanglement measures that do not reduce to the entropy of entanglement are

- Negativity
- Logarithmic negativity
- Robustness of entanglement

#### Entanglement of formation[^William1997]

The **entanglement of formation** is also an entanglement measure for a **generic bipartite state**. Given a density matrix $\rho$ of a pair of quantum systems A and B, consider all possible pure-state decompositions of $\rho$, that is, all ensembles of pure states $|\psi_i\rangle$ with probabilities $p_i$, such that
$$
\rho=\sum_ip_i|\psi_i\rangle\langle\psi_i|
$$
For each bipartite pure state $|\psi_i\rangle$, the entanglement $E$ is defined as the von Neumann entropy of either of the two subsystems A and B
$$
E(|\psi_i\rangle)=-\operatorname{Tr}\left(\rho_{A} \log _{2} \rho_{A}\right)=-\operatorname{Tr}\left(\rho_{B} \log _{2} \rho_{B}\right)
$$
Here $\rho_A=\text{Tr}_B(|\psi_i\rangle\langle\psi_i|)$, and $\rho_B$ has a similar meaning.

The **entanglement of formation** of the mixed state $\rho$ is then defined as the average entanglement of the pure states of the decomposition, minimized over all decompositions of $\rho$:
$$
E(\rho) = \min_{\forall\ decomposition}p_iE(|\Psi_i\rangle)\label{entanglement of formation}
$$
The **entanglement of formation** is intended to **quantify the resources needed to create a given entangled state**. The paper[^William1997] claims that for a pair of qubits, the minimum value specified in Eq. ($\ref{entanglement of formation}$) can be expressed as an explicit function of $\rho$.











[^Neumann1927]: J. von Neumann, Göttinger Nachrichten 1927, 24
[^Bloch1946]: F. Bloch, Phys. Rev. 70, 460 (1946)
[^Jakóbczyk2001]: L. Jakóbczyk and M. Siennicki, Phys. Lett. 286, 383 (2001); T. Tilma, M. S. Byrd, and E. C. G. Sudarshan, J. Phys. A. Math. Gen. 35, 10445 (2002); R. A. Bertlmann and P. Krammer, J. Phys. A. Math. Theor. 41, 235303 (2008).

[^William1997]: William K. Wootters, PRL (1997), Entanglement of Formation of an Arbitrary State of Two Qubits