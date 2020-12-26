本文章翻译于Caltech教授John Preskill的Quantum Computation课程。
课程网址：http://www.theory.caltech.edu/people/preskill/ph229/

## Chapter 2. Foundations I: States and Ensembles
#### 2.1 Axioms of quantum mechanics
本章节讨论**量子开放系统**(open quantum systems)。开放表示它并非被完全隔绝，可以和未知外界交换能量和信息。研究开放系统的动机是，大部分真实系统就是开放的。

我们先考虑量子封闭系统，即完美孤立的系统。为了理解开放系统S的行为，我们可以把S和环境E组成的整体当成孤立体系(“整个宇宙”)，然后研究在无法观测环境E但能够观测S的情况下S的性质。

量子理论是描述物理世界的数学模型。描述**孤立系统**需要五条公理：态，可观测量，测量，动力学，以及如何合并两个系统成为一个整体（态和Hilbert空间的直积）。一个有趣的特性是，薛定谔方程是线性的，而经典动力学方程一般是非线性的。另一个重要区别是，幺正演化是确定的（给定初值和哈密顿，演化就确定了），但测量是随机的：量子理论没有给出对测量结果的预测，只给出了各种可能结果的概率。这很奇怪，因为测量过程不应该受到不同的物理定律支配。“演化的确定性”和“测量的内禀随机性”的区别被称为量子理论的“测量问题”(measurement problem)。

#### 2.2 The Qubit
量子信息的基本单元是qubit，描述最简单的量子系统的态。量子态用Hilbert空间中的射线(ray)表示，而最小的非平凡Hilbert空间是二维的，用二维空间正交归一基$\{|0\rangle,|1\rangle\}$张成。归一化的qubit具有一般形式$a|0\rangle+b|1\rangle$，其中$a,b$是复数且$|a|^2+|b|^2=1$。对量子态的测量会干扰这个态，使它塌缩到某个本征态（本来就是本征态的特例除外）。如果qubit的初态未知，那么仅有单次测量是无法确定$a,b$值的。

对于经典比特来说，我们可以不干扰地测量它的全部信息（即测量不改变它的状态）。如果有一个特定取值（0或1）但我们不知道是哪个值，只能说有$p_0$概率是0，$p_1$概率是1，且$p_0+p_1=1$。测量它后，我们就能100%得到完整信息。

那么，**一个量子比特与一个随机的经典比特究竟有什么区别？** 总的来说，qubit有许多理解方式，但bit只有一种。
##### 2.2.1 Spin-1/2
首先，$a$和$b$包含的信息不止有测量得到某本征态的概率信息，还有具有物理意义的相对相位的信息。

对于二态系统$a|0\rangle+b|1\rangle$，可以用自旋1/2（电子）来解释。$|0\rangle$和$|1\rangle$态可以分别当成自旋沿z轴向上和向下态，用Bloch sphere表示。

**对称性**指作用在某一个态上的、保持系统所有可观测量不变的那种**变换**。在量子力学中，“可观测量”指的是幺正算符的测量值。如果用$\bold{A}$测量态$|\psi\rangle$，那么投影到这个算符本征态$|a\rangle$的概率是$|\langle a|\psi\rangle|^2$。对称性应当保证，当我们同时旋转系统和仪器的时候，这些概率值不变。相应的，在数学上，**对称性**指的是Hilbert空间向量保持内积的模不变的**映射**：$|\psi\rangle\rightarrow|\psi'\rangle$，使得对任意$|\varphi\rangle$和$|\psi\rangle$,有$|\langle\varphi|\psi\rangle|=|\langle\varphi'|\psi'\rangle|$。

**Wigner定理**说复空间里保内积模的变换总能写成**幺正**或**反幺正**的映射（通过选择合适的相位）。于是对称变换可写成$|\psi'\rangle=U|\psi\rangle$。反幺正只在离散对称性出现，在连续对称性不会出现。

对**连续的对称操作**$R$有对应的幺正算符$U(R)$。这些连续对称操作构成**群**：对称变换有逆变换，两个对称变换的乘积也是对称变换。每个对称操作$R$对应一个幺正变换$U(R)$，且乘法必须服从群乘法的规定：$R_1 ◦ R_2$表示先作用$R_2$再作用$R_1$。$U(R_1)U(R_2) = Phase(R_1, R_2) · U(R_1 ◦ R_2)$。出现相位项是因为，$U(R_1 ◦ R_2)$作用在希尔伯特空间的ray（量子态）上，而不是vector上，因此有个不定相位项。我们称$U(R)$是对称群的一种**幺正表示**（a unitary representation, up to a phase）。

**对称性**和**动力学**是两回事。但通常我们要求对称性要服从系统的动力学演化。这意味着“先对称变换再演化”与“先演化再对称变换”是等价的，即时间演化算符$e^{-itH}$与对称变换算符$U(R)$对易：$U(R)e^{-itH}=e^{-itH}U(R)$。对时间小量$t$展开到一阶得到$U(R)\cdot H=H\cdot U(R)$。

<img src="figures/symm_dynam.png"   style="width:500px"/>

假设一个**连续变换**接近$I$：$R=I+\varepsilon T$，那么对应的**幺正矩阵**也接近$I$：$U=I-i\varepsilon Q+O(\varepsilon^2)$，其中$Q=Q(T)$是$T$的函数。由于$U$幺正，$Q$也在$\varepsilon$的一阶近似下幺正，因此是个可观测量，且有$Q=Q^\dagger$。于是有可观测量$Q$与哈密顿对易：$$[Q,H]=0,$$这是个守恒律，即算符$Q$的本征态在薛定谔方程演化下不变（除相位外）。反之，如果已知有个物理量$Q$守恒，即$[Q,H]=0$，那么就可以构造对称变换，将有限大小的变换分解成无限小微元的连乘$U(R)=(I+i\frac{\theta}{N}Q)^N\underset{N\rightarrow\infty}{\rightarrow} e^{i\theta Q}$。$Q$叫作对称变换**生成元**。

举例：**空间旋转**和**角动量**。

【例1：空间旋转】
绕$\hat{n}$轴无限小逆时针转动为$R(\hat{n}, d\theta) = I − id\theta\hat{n}\cdot \vec{J}$，其中$\vec{J}$为角动量。有限大转动为$R(\hat{n}, \theta)=\exp(−i\theta\hat{n}\cdot \vec{J})$。转动群的表示显然可以是三维的矩阵，但是最简单的非平凡不可约表示用的basis是二维Pauli矩阵：$J_k=\frac{1}{2}\sigma_k$，$\sigma_k$为Pauli矩阵，称之为“自旋1/2”表象。Pauli矩阵的反对易算子为$\{\sigma_a, \sigma_b\} = 2 \delta_{a b}\,I$。因此$(\hat{n}\cdot\vec{\sigma})^2=n_kn_l\sigma_k\sigma_l=n_kn_kI=I.$ 有限大小转动可以表示为（证明参见[wiki](https://en.wikipedia.org/wiki/Pauli_matrices#Exponential_of_a_Pauli_vector)）$$U(\hat{n}, \theta)=e^{-i\frac{\theta}{2}({\hat {n}}\cdot {\vec {\sigma }})}=I\cos {\frac{\theta}{2}}-i({\hat {n}}\cdot {\vec {\sigma }})\sin {\frac{\theta}{2}}.$$注意到任意$2\times2$行列式为1的幺正矩阵都可以表示成这个形式。至此，我们可以**将1/2自旋作为一个qubit，把幺正变换当做1/2自旋在复空间的旋转**（不用管可能伴随的物理上不相关的整体相位旋转）。此表象的一个特殊性质是它是双值函数，即绕任意轴转$2\pi$得到$U(\hat{n}, θ = 2\pi) = −I$。因此，这个旋转群的表象会有一个符号的不确定性：$$U(R_1)U(R_2) = \pm U(R_1◦R_2).$$这是合理的，因为群乘法只作用在ray上而不是vector上，因此会有多余的相位项。这个“双值(double-valued)”的表象叫作**spinor representations**。（spinor的存在源于群的拓扑性质——not simply connected.）【存疑？】

将自旋1/2旋转$2\pi$角度不会有可观测的效果（因为只有相位反相），但不要以为自旋1/2的这个性质就观测不到了。举例，假设有个机器可以操作一对自旋，若第一个自旋向上，不操作；若第一个向下，则将第二个旋转$2\pi$。现将第一个自旋变成叠加态：$\frac{1}{\sqrt{2}}(|\uparrow\rangle_1+|\downarrow\rangle_1)|\uparrow\rangle_2\mapsto\frac{1}{\sqrt{2}}(|\uparrow\rangle_1-|\downarrow\rangle_1)|\uparrow\rangle_2$，虽然第二个自旋无可观测变化，但第一个变成原先的正交态，这是可以观测到的。

【例2：角动量】
现在构造$\hat{n}=(\sin\theta\cos\varphi, \sin\theta\sin\varphi, \cos\theta)$方向上的**自旋角动量**本征值。在自旋1/2表象下，通过将$J_3$本征值$\begin{pmatrix} 1\\0\end{pmatrix}$沿向量$\hat{n}'=(−\sin\varphi,\cos\varphi, 0)$逆时针旋转$\theta$，即对$\begin{pmatrix} 1\\0\end{pmatrix}$施加旋转操作（注意此时用的基矢是Pauli matrices）：
$$
\begin{align}
\exp(-i\frac{\theta}{2}{\hat {n}'}\cdot {\vec {\sigma }})&=\exp\left[\frac{\theta}{2}\begin{pmatrix} 0&-e^{-i\varphi}\\e^{i\varphi}&0\end{pmatrix}\right]
=\sum_{k=0}^\infty\frac{\left(\frac{\theta}{2}\right)^k\begin{pmatrix} 0&-e^{-i\varphi}\\e^{i\varphi}&0\end{pmatrix}^k}{k!}
\\&=\sum_{p=0}^\infty\frac{\left(\frac{\theta}{2}\right)^{2p}(-1)^pI}{(2p)!}+\sum_{p=0}^\infty\frac{\left(\frac{\theta}{2}\right)^{2p+1}(-1)^p\begin{pmatrix} 0&-e^{-i\varphi}\\e^{i\varphi}&0\end{pmatrix}}{(2p+1)!}
\\&=I\cos\frac{\theta}{2}+\begin{pmatrix} 0&-e^{-i\varphi}\\e^{i\varphi}&0\end{pmatrix}\sin\frac{\theta}{2}
\\&=\begin{pmatrix} \cos\frac{\theta}{2}&-e^{-i\varphi}\sin{\frac{\theta}{2}}\\e^{i\varphi}\sin{\frac{\theta}{2}}&\cos\frac{\theta}{2}\end{pmatrix},
\end{align}
$$
得到的就是$\hat{n}$方向的本征态$|\psi(\theta,\varphi)\rangle=\exp(-i\frac{\theta}{2}{\hat {n}'}\cdot {\vec {\sigma }})\begin{pmatrix} 1\\0\end{pmatrix}=\begin{pmatrix} e^{-i\varphi/2}\cos{\frac{\theta}{2}}\\e^{i\varphi/2}\sin{\frac{\theta}{2}}\end{pmatrix}$（不管整体相位）。可以证明它确实是矩阵$$\hat{n}\cdot\vec{\sigma}=\begin{pmatrix} \cos\theta&e^{-i\varphi}\sin\theta\\e^{i\varphi}\sin\theta&-\cos\theta\end{pmatrix}$$本征值为1的本征态，即沿着$(\theta,\varphi)$方向的自旋向上本征态。因此，qubit的两个系数$a=e^{-i\varphi}\cos{\frac{\theta}{2}}$ 和 $b=e^{i\varphi}\sin{\frac{\theta}{2}}$可以解释为指向$(\theta,\varphi)$的自旋。

有了铺垫，下面就可以讨论**随机经典比特和量子比特的区别**了。取特殊方向$(\theta,\varphi)=(\pi/2,0)$（x轴），则量子态变为自旋x轴向上态$|\uparrow_x\rangle=\frac{1}{\sqrt{2}}(|\uparrow_z\rangle+|\downarrow_z\rangle)$，其正交态为自旋x轴向下态$|\downarrow_x\rangle=\frac{1}{\sqrt{2}}(|\uparrow_z\rangle-|\downarrow_z\rangle)$。对这两个态，如果测量z轴的自旋，各有1/2概率会得到$|\uparrow_z\rangle$或$|\downarrow_z\rangle$。现测量一个新的态$\frac{1}{\sqrt{2}}(|\uparrow_x\rangle+|\downarrow_x\rangle)$沿z轴的自旋。若为经典比特，各有1/2概率得到两个x轴方向的本征态，而它们各自又是1/2概率得到z轴方向的两个结果，因此最终是各有1/2概率得到z轴向上或向下自旋；若为量子比特，代入计算得到这个态就一定是z轴向上态，不可能是z轴向下态！量子世界里，概率并非简单相加！这种区别来源于**量子相干性**（quantum interference）。

小结一下qubit的几何解释：我们可以把1/2自旋当成qubit，它的量子态由三维空间中表示自旋方向的单位向量$\hat{n}$完全来表征。幺正变换旋转这个自旋，对自旋的测量只有两个结果，沿着某个（仪器给定的）轴向上或向下态。

着重强调一下，尽管形式上1/2自旋表述可以用于任何二能级系统，但不是所有二能级系统都具有spinor在空间旋转的奇特性质！【反例？】

##### 2.2.2 Photon polarizations
另一个重要的二态系统是光子，可以有两个极化方向。极化方向也会随着转动操作而变换，但它与1/2自旋的重要区别是：(1)光子无质量，(2)光子自旋为1（光子不是spinor）。

> **庞加莱群**（Poincare group）：是狭义相对论中闵可夫斯基时空的等距同构群，是有10（4+3+3）个生成元的非阿贝尔群、非紧致李群。庞加莱对称性：
> 1.**时空平移(translations)**（描述时空中的平移的4维阿贝尔李群，其生成元为$P$）；
> 2.**三维空间旋转(rotations)**（描述3维旋转的非阿贝尔李群，其生成元为$J$）；
> 3.**直线性洛伦兹变换(boosts)**（联系两个惯性坐标系的变换，其生成元为$K$）。
> 后两者（$J$和$K$）构成了一个子群——**洛伦兹群**（Lorentz group）。平移群$P$和洛伦兹群的半直积（semi-direct product）就构成了庞加莱群。后文说的**The little group**指的是，洛伦兹群中保持粒子动量不变的某个子群。

我们这里不讨论庞加莱群的幺正表示。在The little group这个保持动量不变的洛伦兹群的子群里，自旋可以用来区分粒子在这个小群下是如何变换的。

**对于有质量的粒子**，我们boost到粒子静止坐标系（保证粒子动量守恒），于是the little group简化变为三维空间旋转群。【为何旋转会保持动量不变？】

**对于无质量的粒子**，不存在静止坐标系。上述the little group的有限维幺正表示就变成了二维旋转群的表示——绕动量方向轴的二维转动。对于经典光子来说，就是垂直于传播方向的两个横向极化方向。

光子的两个极化方向，绕传播方向轴线旋转可表示为：
$$
|x\rangle→ \cos\theta|x\rangle + \sin\theta|y\rangle\\
|y\rangle→ −\sin\theta|x\rangle+ \cos\theta|y\rangle\label{polar}
$$
此二维表示是**可约的**：矩阵$\begin{pmatrix} \cos\theta&\sin\theta\\−\sin\theta&\cos\theta\end{pmatrix}$具有本征态$|R\rangle=\frac{1}{\sqrt{2}}\begin{pmatrix} 1\\i\end{pmatrix}$和$|L\rangle=\frac{1}{\sqrt{2}}\begin{pmatrix} i\\1\end{pmatrix}$，其本征值分别为$e^{i\theta}$和$e^{-i\theta}$，分别表示左右圆偏振。换句话说，这两个态是旋转生成元$J=\begin{pmatrix} 0&-i\\i&0\end{pmatrix}=\sigma_2$的本征态，本征值为$\pm1$。正是因为对应Pauli矩阵的本征态为$\pm1$（而不是$\pm\frac{1}{2}$），我们称**光子的自旋为1**。

假设光子依次通过x方向偏振片和y方向偏振片，并假设一半的光子可以通过x偏振片，显然这些光子不可能再通过y方向偏振片了。但是如果在中间加个45度偏振片，那么有1/8的光子可以完全穿过整个装置。这个过程中很难说一个光子携带了1bit关于极化的经典信息，因此qubit和概率化的经典bit有区别。

下面我们构造一个general的光子“极化方向+相对相位”调节器。可以用一个**装置A**来旋转光子极化方向，实现上述Eq.$(\ref{polar})$的旋转变换。它的原理是“调开”一个哈密顿量，要求圆偏振态$|L\rangle$和$|R\rangle$为其非简并能量本征态，在达到所要求的偏振方向后关闭哈密顿。当然这不是最一般的幺正变换。还可以用另一个**装置B**改变两个线偏振态的相对相位（调开另一个哈密顿量，要求线偏振态为其非简并能量本征态）：
$$
|x\rangle→ e^{-i\varphi/2}|x\rangle\\
|y\rangle→ e^{i\varphi/2}|y\rangle
$$
**装置A**（改变线偏振态方向）和**装置B**（调整线偏振态的相对相位）可以组合在一起，构造光子极化态的任意$2\times2$且模为1的幺正变换。

#### 2.3 The density operator
##### 2.3.1 The bipartite quantum system
现在从1 qubit变到2 qubits。

2.1节讨论的五条公理只适用于**封闭系统**。实际上封闭系统并不存在，我们观察到的系统可能只是一个更大系统的一部分。当我们研究**开放系统**，即大系统的一个局部时：

- **量子态**不再是rays（而是由密度矩阵描述）;
- **测量**不再是正交投影；
- **演化**不再是幺正的。

理解开放系统量子描述的第一步，可以从研究2-qubit系统中的某一个qubit做起。假设qubit A可以被我们观测或进行操作，但是qubit B远在天边无法探测。AB系统作为整体是个封闭系统，服从五条公理。我们现在想看看有没有合理的**单独描述qubit A**的方式。

考虑物体A和B在各自正交基下的2qubit量子态：
$$
|\psi\rangle_{AB} = a|0\rangle_A\otimes|0\rangle_B + b|1\rangle_A\otimes|1\rangle_B\label{2qubit}
$$
这个态里A和B存在关联。假设我们通过单独测量A把它投影到基$\{|0\rangle_A, |1\rangle_A\}$上，那么可以测得$|0\rangle_A$概率为$|a|^2$，制备了态$|0\rangle_A\otimes|0\rangle_B$，另一种情况同理。不管是哪种情况，得到了A的态，那么B的态也就确定了，对B用基$\{|0\rangle_B, |1\rangle_B\}$测量就能预测100%确定的结果。在这个意义下，我们说对于上述量子态$|\psi\rangle_{AB}$，用基$\{|0\rangle_A, |1\rangle_A\}$和$\{|0\rangle_B, |1\rangle_B\}$测量得到的结果之间存在完全关联(perfectly correlated)。

考虑作用在A系统上更一般的可观测量，我们想在不关心B测量结果情况下，只获取A的测量结果。假设$M_A$是作用在A系统上的幺正算符，$I_B$是B上的恒等算符，则可观测量$M_A\otimes I_B$在$|\psi\rangle_{AB}$下的均值为（推导用到了$|0\rangle_B$和$|1\rangle_B$的正交归一性）：
$$
\begin{aligned}\langle M_A\rangle&=\langle\psi| M_A\otimes I_B|\psi\rangle\\&=(a^*\langle 00|+b^*\langle 11|)(M_A\otimes I_B)(a|00\rangle+b|11\rangle)\\&=|a|^2\langle 0|M_A|0\rangle+|b|^2\langle 1|M_A|1\rangle\\&=\text{tr}(M_A\rho_A).\end{aligned}
$$
其中密度算符$\rho_A=|a|^2|0\rangle\langle0|+|b|^2|1\rangle\langle1|$，它自共轭，正定，trace为1（因为$|\psi\rangle$是归一态）。

最后一行的形式对于任意作用在qubit A上的算符$M_A$都成立，因此$\rho_A$**可以理解为an ensemble of possible quantum states, each occurring with a specified probability**。

对于**1个qubit**，其$|0\rangle$和$|1\rangle$的**相干叠加态**(coherent superposition)和它们组成的**系综态**(probabilistic ensemble)$\{p_0,|0\rangle; p_1,|1\rangle\}$是两个完全不同的概念。举例，对于自旋1/2粒子的相干叠加态$\frac{1}{\sqrt{2}}(|\uparrow_z\rangle+|\downarrow_z\rangle)$测量其$\sigma_1$，一定只会得到$|\uparrow_x\rangle$。但是对于$|\uparrow_z\rangle$和$|\downarrow_z\rangle$各有1/2概率出现的系综来说，要用密度矩阵表示$\rho=\frac{1}{2}(|\uparrow_z\rangle\langle\uparrow_z|+|\downarrow_z\rangle\langle\downarrow_z|)=\frac{1}{2}I$，将它投影到$|\uparrow_x\rangle$上得到期望值为1/2：$\text{tr}(|\uparrow_x\rangle\langle\uparrow_x|\rho)=\langle\uparrow_x|\rho|\uparrow_x\rangle=1/2$。同理，将这个系综态沿着任意$\{\theta,\varphi\}$方向测量，得到“自旋向上态”$|\psi(\theta,\varphi)\rangle$的概率为$\langle|\psi\rangle\langle\psi|\rangle=\text{tr}(|\psi\rangle\langle\psi|\rho)=\langle\psi|\frac{1}{2}I|\psi\rangle=1/2$，同理“自旋向下态”概率也是1/2。因此，在**A和B组成的2-qubit**世界中，如果总的态$|\psi\rangle_{AB}$是由$|00\rangle$和$|11\rangle$等概率构成的相干叠加态$|\psi\rangle_{AB} = \frac{1}{2}|0\rangle_A\otimes|0\rangle_B + \frac{1}{2}|1\rangle_A\otimes|1\rangle_B$，那么只测量A系统的话，A会表现得**不具有相干性**——沿着任意方向测量，都会等概率得到“自旋向上”或“自旋向下”。

上述讨论可以**推广到任意双系统体系**。双系统体系的Hilbert空间表示为$\mathcal{H}_A\otimes\mathcal{H}_B$。若$\{|i\rangle_A\}$是$\mathcal{H}_A$的一组正交基，$\{|\mu\rangle_B\}$是$\mathcal{H}_B$的一组正交基，那么$\{|i\rangle_A\otimes|\mu\rangle_B\}$是$\mathcal{H}_A\otimes\mathcal{H}_B$的一组正交基。总Hilbert空间$\mathcal{H}_A\otimes\mathcal{H}_B$的任意一个**纯态**表示为$|\psi\rangle_{AB}=\sum_{i,\mu}a_{i\mu}|i\rangle_A\otimes|\mu\rangle_B$，其中$\sum_{i,\mu}|a_{i\mu}|^2=1$。可观测量$M_A\otimes I_B$作用在子系统A上的均值为
$$
\begin{aligned}\left\langle\boldsymbol{M}_{A}\right\rangle &=_{A B}\left\langle\psi\left|\boldsymbol{M}_{A} \otimes \boldsymbol{I}_{B}\right| \psi\right\rangle_{A B} \\ &=\sum_{j, \nu} a_{j \nu}^{*}(_{A}\langle j|\otimes_{B}\langle\nu|)\left(\boldsymbol{M}_{A} \otimes \boldsymbol{I}_{B}\right) \sum_{i, \mu} a_{i \mu}\left(|i\rangle_{A} \otimes|\mu\rangle_{B}\right).\\ &=\sum_{i, j, \mu} a_{j \mu}^{*} a_{i \mu}\left\langle j\left|\boldsymbol{M}_{A}\right| i\right\rangle=\operatorname{tr}\left(\boldsymbol{M}_{A} \boldsymbol{\rho}_{A}\right) \end{aligned}
$$
其中
$$
\boldsymbol{\rho}_A\equiv\text{tr}_B(|\psi\rangle\langle\psi|)=\sum_{i,j,\mu}a_{i\mu}a_{j\mu}^*|i\rangle\langle j|\label{densityOperator}
$$
是作用在子系统A上的密度算符（一般情况下非对角）。这个仅作用在A系统上的密度矩阵$\boldsymbol{\rho}_A$是通过将总系统AB的密度矩阵（此处是**纯态**$|\psi\rangle_{AB}$的密度矩阵）对B系统求partial trace得到的。

此段讲述**partial trace的本质**。我们可以将dual vector (or bra) $_B\langle\mu|$看成**对ket的线性映射**（linear map），它将$\mathcal{H}_A\otimes\mathcal{H}_B$的ket向量映射到$\mathcal{H}_A$的ket向量，定义式为$_B\langle\mu|i\nu\rangle_{AB}=\delta_{\mu\nu}|i\rangle_A$。同理，ket $|\mu\rangle_B$将$\mathcal{H}_A\otimes\mathcal{H}_B$对偶空间的bra线性映射到$\mathcal{H}_A$的bra上，$_{AB}\langle i\nu|\mu\rangle_B=\delta_{\mu\nu}\ _A\langle i|$。由此，可以看出，**partial trace操作是一种对算符的线性映射**，它将$\mathcal{H}_A\otimes\mathcal{H}_B$空间的算符$M_{AB}$映射到$\mathcal{H}_A$空间的算符，定义式为$\text{tr}_BM_{AB}=\sum_{\mu}\ _B\langle\mu|M_{AB}|\mu\rangle_B$。将$M_{AB}$替换成$\mathcal{H}_A\otimes\mathcal{H}_B$空间的密度算符$|\psi\rangle_{AB}\ _{AB}\langle\psi|$，就是$\rho_A$的定义$\rho_A=\text{tr}_B(|\psi\rangle_{AB}\ _{AB}\langle\psi|)$，即把左边的$|\psi\rangle_{AB}$映射到$|i\rangle_A$（忽略系数），把右边的$_{AB}\langle\psi|$映射到$_A\langle j|$。

由Eq.$(\ref{densityOperator})$得到$\boldsymbol{\rho}_A$的性质：

- 厄米：$\boldsymbol{\rho}_A=\boldsymbol{\rho}_A^{\dagger}$.
- 正定：对任意$|\varphi\rangle_A$，有$\langle\varphi|\boldsymbol{\rho}_A|\varphi\rangle=\sum_\mu |\sum_ia_{i\mu}\langle\varphi|i\rangle|^2\geq0$.
- $\text{tr}(\boldsymbol{\rho}_A)=\sum_{i,\mu}|a_{i\mu}|^2=1$, since $|\psi\rangle_{AB}$ is normalized.

因此，$\boldsymbol{\rho}_A$可以被对角化，且对角元特征值均为非负实数，求和为1。

当我们观测大系统的一个子系统时，即使大系统的态是ray，子系统也不一定是ray，因此子系统一般要用密度矩阵表示。如果子系统的态也是ray，那么子系统就是一个**纯态**；否则是**混合态**。纯态$|\psi\rangle_A$对应的密度矩阵$\boldsymbol{\rho}_A=|\psi\rangle_{A}\ _{A}\langle\psi|$实际上是个投影到$|\psi\rangle_A$所张成的一维空间的投影算符【存疑】，因此$\rho_A^2=\rho_A$。

对一般态的密度矩阵，在对角化的正交归一基下表示为$\boldsymbol{\rho}_A=\sum_ap_a|a\rangle\langle a|$，且$\text{tr}\boldsymbol{\rho}_A^2=\sum p^2_a<\sum p_a=1$。我们称$\boldsymbol{\rho}_A$是本征态$\{|a\rangle\}$的**incoherent mixture**，此处“incoherent ”指的是不同本征态$|a\rangle's$之间的相对相位无法通过实验观测到。任意作用在子系统A上的算符$M_A$的期望值可表示为$\langle M_A\rangle=\text{tr}(M_A\boldsymbol{\rho}_A)=\sum_a p_a\langle a|M|a\rangle$，因此$\boldsymbol{\rho}_A$可理解为**an ensemble of pure quantum states**。

小结： A和B系统有相互作用，它们的态是纠缠的（有关联的），**纠缠破坏了A系统不同量子态之间的相干叠加性**，因此若我们仅观测A（把B求trace掉）就无法提取A的态之间相对相位的信息。从这个意义上说，A的量子态“塌缩”了，成为一堆可能的态（不一定是本征态）的集合（而不是相干叠加），而每个态会对应一个概率，所有态构成了一个系综。这样我们就理解了当A和B相互作用时，概率如何在量子力学里出现。

##### 2.3.2 Bloch sphere(球表面纯态的两种等价表示)
暂时回到单个qubit的情况。最一般的$2\times2$密度矩阵（厄米矩阵）有4个实参量，可以用基$\{I,\sigma_1,\sigma_2,\sigma_3\}$展开。因为$\sigma_i$的trace为0，所以$I$的系数一定为1/2，才能满足$\text{tr}\boldsymbol{\rho}=1$，因此展开式表示成$$\rho(\vec{P})=\frac{1}{2}(I+\vec{P}\cdot\vec{\sigma})=\frac{1}{2}\begin{pmatrix}1+P_3&P_1-iP_2\\P_1+iP_2&1-P_3\end{pmatrix}$$其中$P_i$均为实数。计算$\text{det}\rho=\frac{1}{4}(1-\vec{P}^2)$，因此$\rho$有两个非负本征值的**必要条件**是$\text{det}\rho\geq0$或$|\vec{P}|^2\leq1$。同时这也是**充分条件**，因为$\text{det}\rho\geq0$得出两个本征值同号，而$\text{tr}\rho=1$要求它们不可能同时为负。

>注：$\rho(\vec{P})=\frac{1}{2}\begin{pmatrix}1+P_3&P_1-iP_2\\P_1+iP_2&1-P_3\end{pmatrix}$的本征值为$\lambda_{\pm}=\frac{1}{2}\left(1\pm|\vec{P}|\right)$。当且仅当$\vec{P}=0$时密度算符有简并本征值$1/2$。

单个qubit的任意密度矩阵1-1对应于3维单位球上的点$\vec{P}$，这个单位球称为Bloch sphere（尽管它是个ball，并不是sphere）。球表面上的点($|\vec{P}|=1$球面)对应$\text{det}\rho=0$。因为$\text{tr}\rho=1$，所以特征值必为0和1，因此**球面的点表示纯态**。用单位向量$\hat{n}$表示球面上$|\vec{P}|=1$的点，利用$(\hat{n}\cdot\vec{\sigma})^2=I$，易证纯态密度矩阵$\rho(\hat{n})=\frac{1}{2}(I+\hat{n}\cdot\vec{\sigma})$满足性质$(\hat{n}\cdot\vec{\sigma})\rho(\hat{n})=\rho(\hat{n})(\hat{n}\cdot\vec{\sigma})=\rho(\hat{n})$，因此在这个纯态下算符$(\hat{n}\cdot\vec{\sigma})$的均值$\langle\hat{n}\cdot\vec{\sigma}\rangle=\text{Tr}((\hat{n}\cdot\vec{\sigma})\rho(\hat{n}))=\text{Tr}\rho(\hat{n})=1$，即此纯态为$\hat{n}$方向上自旋为1的本征态，所以纯态密度矩阵也可以表达为投影算符$\rho(\hat{n})=|\psi(\hat{n})\rangle\langle\psi(\hat{n})|$，$\hat{n}$是算符$\hat{n}\cdot\vec{\sigma}$的“自旋向上”态$|\psi(\hat{n})\rangle$指向的方向。或者直接用$|\psi(\theta,\varphi)\rangle=\begin{pmatrix} e^{-i\varphi/2}\cos{\frac{\theta}{2}}\\e^{i\varphi/2}\sin{\frac{\theta}{2}}\end{pmatrix}$写出来:
$$
\begin{align}\rho(\hat{n})&=|\psi(\hat{n})\rangle\langle\psi(\hat{n})|\nonumber\\&=\left(\begin{matrix}\cos^2(\theta/2)&\cos(\theta/2)\sin(\theta/2)e^{-i\varphi}\\\cos(\theta/2)\sin(\theta/2)e^{i\varphi}&\sin^2(\theta/2)\end{matrix}\right)\nonumber\\&=\frac{1}{2}I+\frac{1}{2}\left(\begin{matrix}\cos\theta&\sin(\theta)e^{-i\varphi}\\\sin(\theta)e^{i\varphi}&-\cos\theta\end{matrix}\right)\nonumber\\&=\frac{1}{2}(I+\hat{n}\cdot\vec{\sigma}).\label{equivalence}\end{align}
$$
用Bloch球的参数化密度矩阵表示**纯态**的好处是$|\psi(\theta,\varphi)\rangle$的物理上不重要的相位项不会出现在$\rho(\theta,\varphi)=|\psi(\hat{n})\rangle\langle\psi(\hat{n})|$中，$\rho$的每一个参数都是有物理意义的。

对于**一般的向量**$|\vec{P}|^2\leq1$，由$\sigma_i\sigma_j=I\delta_{ij}+i\epsilon_{ijk}\sigma_k$推出的性质$\frac{1}{2}\text{tr}(\sigma_i\sigma_j)=\delta_{ij}$，得到算符$\hat{n} \cdot \vec{\boldsymbol{\sigma}}$在混合态下的均值为
$$
\langle\hat{n} \cdot \vec{\boldsymbol{\sigma}}\rangle_{\vec{P}}=\operatorname{tr}(\hat{n} \cdot \vec{\boldsymbol{\sigma}} \rho(\vec{P}))=\operatorname{tr}\left(\frac{1}{2}\hat{n} \cdot \vec{\boldsymbol{\sigma}}+\frac{1}{2}(\hat{n} \cdot \vec{\boldsymbol{\sigma}})(\vec{P} \cdot \vec{\boldsymbol{\sigma}})\right)=\operatorname{tr}\left(\frac{1}{2}n_i\sigma_iP_j\sigma_j\right)=\hat{n} \cdot \vec{P}
$$
如果我们有一堆制备好的全同的混合态（用$\vec{P}$标记），那么就可以通过测量这个态在三个线性独立方向$\hat{n}_k$上可观测量$\hat{n}_k \cdot \vec{\boldsymbol{\sigma}}$的均值$\langle\hat{n}_k \cdot \vec{\boldsymbol{\sigma}}\rangle_{\vec{P}}$完全确定$\vec{P}$的三个分量。我们称向量$\vec{P}$标记了自旋的极化(polarization )。

#### 2.4 Schmidt decomposition

本节讨论双粒子的纯态(bipartite pure state)的Schmidt decomposition表示。

> 注：正交归一基不一定会让$\boldsymbol{\rho}_{A}$对角。
>
> 举例：混合态$\boldsymbol{\rho}_{A}=p_1|\uparrow_x\rangle\langle\uparrow_x|+p_2|\downarrow_x\rangle\langle\downarrow_x|$在基$\{|\uparrow_x\rangle,|\downarrow_x\rangle\}$下是对角的，其中$p_1\neq p_2$且$p_1+p_2=1$。若选择另一组正交归一基$\{|\uparrow_z\rangle,|\downarrow_z\rangle\}$，即做幺正变换$|\uparrow_x\rangle=\frac{1}{\sqrt{2}}(|\uparrow_z\rangle+|\downarrow_z\rangle)$和$|\downarrow_x\rangle=\frac{1}{\sqrt{2}}(|\uparrow_z\rangle-|\downarrow_z\rangle)$，则表示为
> $$
> \boldsymbol{\rho}_{A}=\frac{p_1+p_2}{2}|\uparrow_z\rangle\langle\uparrow_z|-\frac{p_1-p_2}{2}|\uparrow_z\rangle\langle\downarrow_z|-\frac{p_1-p_2}{2}|\downarrow_z\rangle\langle\uparrow_z|+\frac{p_1+p_2}{2}|\downarrow_z\rangle\langle\downarrow_z|
> $$
> 是非对角的形式！不过trace还是1。正交归一基$\{|\uparrow_x\rangle,|\downarrow_x\rangle\}$让$\boldsymbol{\rho}_{A}$成为对角形式，称为A系统的Schmidt bases。对这个混合态$\boldsymbol{\rho}_{A}$，若选用了基$\{|\uparrow_z\rangle,|\downarrow_z\rangle\}$，需要幺正变换到Schmidt bases$\{|\uparrow_x\rangle,|\downarrow_x\rangle\}$才能将$\boldsymbol{\rho}_{A}$化为对角形式。

$\mathcal{H}_A\otimes\mathcal{H}_B$中任意一个向量可表示为
$$
|\psi\rangle_{AB}=\sum_{i,\mu}a_{i\mu}|i\rangle_A\otimes|\mu\rangle_B\equiv\sum_i|i\rangle_A\otimes|\tilde{i}\rangle_B\label{generalVector}
$$
其中$\{|i\rangle_A\}$和$\{|\mu\rangle_B\}$分别是各自子空间的正交归一基（它们不一定是各自的Schmidt bases）。在最后一个等式中定义了$|\tilde{i}\rangle_B\equiv\sum_\mu a_{i\mu}|\mu\rangle_B$，注意此时这些$\{|\tilde{i}\rangle_B\}$'s 不一定能保证相互正交或归一。

> 这一步，我们把和$|i\rangle_A$态配对的所有B的态线性组合成一个态，系数为$a_{i\mu}$，标记为$|\tilde{i}\rangle_B$。

现在假设基$\{|i\rangle_A\}$已经使得$\boldsymbol{\rho}_{A}$对角（即$\{|i\rangle_A\}$为A的Schmidt bases，对更一般情况需要先将A的基幺正变换到Schmidt bases，见**文末附录**）：$\boldsymbol{\rho}_{A}=\sum_ip_i|i\rangle\langle i|$。另一方面，$\boldsymbol{\rho}_{A}$也可以通过对B求partial trace得到：
$$
\begin{aligned}\boldsymbol{\rho}_{A}&=\operatorname{tr}_{B}(|\psi\rangle\langle\psi|) \\ &=\operatorname{tr}_{B}\left(\sum_{i, j}|i\rangle\langle j|\otimes| \tilde{i}\rangle\langle\tilde{j}|\right)
\\&=\sum_{i, j}|i\rangle\langle j|\otimes\sum_\mu\langle \mu|\tilde{i}\rangle\langle\tilde{j}|\mu\rangle
\\&=\sum_{i, j}|i\rangle\langle j|\otimes\sum_\mu\langle\tilde{j}|\mu\rangle\langle \mu|\tilde{i}\rangle
\\&=\sum_{i, j}\langle\tilde{j}|\tilde{i}\rangle(|i\rangle\langle j|)\end{aligned}
$$
比较两者，得到$_B\langle\tilde{j}|\tilde{i}\rangle_B=p_i\delta_{ij}$，因此$\{|\tilde{i}\rangle_B\}$'s的确是正交的。把它们归一化$|i'\rangle_B=p_i^{-1/2}|\tilde{i}\rangle_B$。注意$p_i\neq0$，因为我们只归一化那些非零概率的对角元，即$\{|\tilde{i}\rangle_B\}$'s不一定张成完整的$\mathcal{H}_B$空间，或$\{|i\rangle_A\}$'s不一定张成完整的$\mathcal{H}_A$空间。因此Eq.$(\ref{generalVector})$可以改写为$\mathcal{H}_A$和$\mathcal{H}_B$各自正交归一基$\{|i\rangle_A\}$和$\{|i'\rangle_B\}$下的展开：
$$
|\psi\rangle_{AB}=\sum_i\sqrt{p_i}|i\rangle_A\otimes|i'\rangle_B\label{Schmidt}
$$
上式就是bipartite pure state的Schmidt decomposition，此时$\boldsymbol{\rho}_A$和$\boldsymbol{\rho}_B$**均为对角形式**，因为$\boldsymbol{\rho}_B=\text{tr}_A(|\psi\rangle\langle\psi|)=\sum_ip_i|i'\rangle\langle i'|$，此时它们的基称为各自的Schmidt bases。

> **总结上述Schmidt decomposition（$p_i$无简并）的步骤**：
>
> (1) 对于给定的一般态$|\psi\rangle_{AB}=\sum_{i,\mu}a_{i\mu}|i\rangle_A\otimes|\mu\rangle_B$，先对A的基矢做幺正变换到A的Schmidt bases使得$\boldsymbol{\rho}_{A}$对角（上文中假设$\{|i\rangle_A\}$已经是A的Schmidt bases了，但对一般情况我们应当讲清是如何变换的，见**文末附录**），得到一套对角元$\{p_i\}$；
>
> (2) 定义$|\tilde{i}\rangle_B\equiv\sum_\mu a_{i\mu}|\mu\rangle_B$，并用前面的$\{p_i\}$将它们归一化$|i'\rangle_B=p_i^{-1/2}|\tilde{i}\rangle_B$；
>
> (3) 在新的两个基下改写成$|\psi\rangle_{AB}=\sum_i\sqrt{p_i}|i\rangle_A\otimes|i'\rangle_B$即可。

所选用的基依赖于不同的bipartite pure state，因为不同的态系数$a_{i\mu}$不同。一般地我们不能同时将两个态$|\psi\rangle_{AB}$和$|\varphi\rangle_{AB}\in\mathcal{H}_A\otimes\mathcal{H}_B$用同一组$\mathcal{H}_A$和$\mathcal{H}_B$的正交归一基展开成Eq.$(\ref{Schmidt})$的形式，因为两个态的系数$a_{i\mu}$不同，即使$|i\rangle_A$用同一组基矢，$|i'\rangle_B$的定义也不一样。

> From the note "Introduction to Entanglement Entropy ":
>
> The number of terms in the sum of Eq.($\ref{Schmidt}$) is (at most) the dimension of the smaller Hilbert space $\mathcal{H}_A$ or $\mathcal{H}_B$. If A is small and B is big, this is intuitive. It says we can pick a basis for $|i\rangle_A$, and each of these states will be correlated with a particular state of system B. 

**下面讨论对一般双系统态（$p_i$无简并），如何找两个子系统各自的幺正变换变成Schmidt bases。**

比较Schmidt bases下的展开式Eq.$(\ref{Schmidt})$和一般正交归一基下的展开式（此时$\rho_A$和$\rho_B$均不一定是对角形式）
$$
|\psi\rangle_{AB}=\sum_{a,\mu}\psi_{a\mu}|a\rangle_A\otimes|\mu\rangle_B\label{moreGeneral}
$$
正交基$\{|a\rangle_A\}$和$\{|\mu\rangle_B\}$分别通过幺正变换$U_A,U_B$变成Schmidt bases$\{|i\rangle_A\}$和$\{|i'\rangle_B\}$，因此
$$
|i\rangle_{A}=\sum_{a}|a\rangle_{A}\left(U_{A}\right)_{a i}, \quad\left|i^{\prime}\right\rangle_{B}=\sum_{\mu}|\mu\rangle_{B}\left(U_{B}\right)_{\mu i^{\prime}}
$$
对比Eq.$(\ref{Schmidt})$和Eq.$(\ref{moreGeneral})$，有（注意B的$i'$指标和A的$i$指标是一一对应的，故下式下标统一用$i$）
$$
\psi_{a \mu}=\sum_{i}\left(U_{A}\right)_{a i} \sqrt{p_{i}}\left(U_{B}^{T}\right)_{i \mu}\label{SVD}
$$
因此，通过幺正变换，任何general的矩阵$\psi_{a \mu}$都能变换成对角且非负的（若Hilbert空间$\mathcal{H}_A$和$\mathcal{H}_B$的维数不同，则该“对角”矩阵为矩形）。Eq.$(\ref{SVD})$实际上是矩阵$\psi_{a \mu}$的**奇异值分解**(singular value decomposition, SVD)，对角元（即态的权重）$\{\sqrt{p_i}\}$在Schmidt decomposition中是矩阵$\psi_{a \mu}$的异值。

由Eq.$(\ref{Schmidt})$对子空间$\mathcal{H}_A$求trace得到$\boldsymbol{\rho}_{B}=\operatorname{tr}_{A}(|\psi\rangle\langle\psi|)=\sum_ip_i|i'\rangle\langle i'|$也是纯态，可见$\boldsymbol{\rho}_{A}$和$\boldsymbol{\rho}_{B}$具有相同的**非零本征值集合**，若$\mathcal{H}_A$和$\mathcal{H}_B$维数不同，则它们的**零本征值**数量会不同。$\blacksquare$

**若$p_i$有简并，如何构造Eq.$(\ref{Schmidt})$？**

如果$\boldsymbol{\rho}_{A}$（和$\boldsymbol{\rho}_{B}$）除了零本征值外**没有简并的非零本征值**，那么态$|\psi\rangle_{AB}$的Schmidt decomposition由$\boldsymbol{\rho}_{A}$和$\boldsymbol{\rho}_{B}$**唯一确定**。可以分别对角化$\boldsymbol{\rho}_{A}$和$\boldsymbol{\rho}_{B}$找到Schmidt bases$\{|i\rangle_A\}$和$\{|i'\rangle_B\}$，然后配对两者具有相同特征值$p_i$的本征态，就构造出了Eq.$(\ref{Schmidt})$。此处选择基矢的相位使得求和项里没有相位项；仅剩的自由度是同时将$\{|i\rangle_A\}$和$\{|i'\rangle_B\}$定义为它们的反相，但这并不改变Eq.$(\ref{Schmidt})$。构造过程上文已经有讨论。

如果$\boldsymbol{\rho}_{A}$（和$\boldsymbol{\rho}_{B}$）**有简并的非零本征值**，则需要由$\boldsymbol{\rho}_{A}$和$\boldsymbol{\rho}_{B}$提供更多信息来确定Schmidt decomposition，即知道哪个$|i'\rangle_B$匹配哪个$|i\rangle_A$。举例，若$\mathcal{H}_A$和$\mathcal{H}_B$均为d维，$U_{ij}$是任意$d\times d$幺正矩阵，则对下面这个构造的态求partial trace（注意$\{|i\rangle_A\}$和$\{|j'\rangle_B\}$分别$\mathcal{H}_A$和$\mathcal{H}_B$的正交归一基，不一定是Schmidt bases，但下面注释会证明实际上态能写成这个形式的话，$\{|j'\rangle_B\}$确实是B的Schmidt bases）：
$$
|\psi\rangle_{A B}=\frac{1}{\sqrt{d}} \sum_{i, j=1}^{d}|i\rangle_{A} U_{i j} \otimes\left|j^{\prime}\right\rangle_{B}
$$
得到$\boldsymbol{\rho}_{A}=\boldsymbol{\rho}_{B}=\frac{1}{d}I$，都是对角的，本征值为$1/d$，是d维简并的。

> 证明：
> $$
> \begin{align}
> \boldsymbol{\rho}_{A}&=\operatorname{tr}_{B}(|\psi\rangle\langle\psi|)=\sum_{j'}\ _B\langle j'|\left(\frac{1}{d}\sum_{i,j,p,q=1}^d U_{ij}U_{pq}^*|i\rangle_A\ _A\langle p|\otimes|j'\rangle_B\ _B\langle q'|\right)|j'\rangle_B\\
> &=\frac{1}{d}\sum_{i,j,p=1}^d U_{ij}U_{pj}^*|i\rangle_A\ _A\langle p|=\frac{1}{d}\sum_{i,p=1}^d \left(\sum_j U_{ij}U_{jp}^\dagger\right)|i\rangle_A\ _A\langle p|\\
> &=\frac{1}{d}\sum_{i,p=1}^d \delta_{ip}|i\rangle_A\ _A\langle p|=\frac{1}{d}I
> \end{align}
> $$
> $\boldsymbol{\rho}_{B}$同理可证。$\blacksquare$
>
> **注**：这个构造的态中，矩阵$U_{ij}$幺正的性质很重要。实际上，把$i$的求和放进去表示对A的正交归一基做幺正变换构造新的基$\{|j\rangle\}$，
> $$
> |\psi\rangle_{A B}=\frac{1}{\sqrt{d}} \sum_{j=1}^{d}\left(\sum_i^d|i\rangle_{A} U_{i j} \right)\otimes\left|j^{\prime}\right\rangle_{B}= \sum_{j=1}^{d}\frac{1}{\sqrt{d}}|j\rangle_{A}\otimes\left|j^{\prime}\right\rangle_{B}
> $$
> 这其实就是写成了Schmidt decomposition形式。可以看出$\{|j\rangle_A\}$和$\{|j'\rangle_B\}$都是Schmidt bases。

进一步，我们可以对这两个均已使用了Schmidt bases的子空间同时施加互为共轭的幺正变换
$$
|i\rangle_{A}=\sum_{a}|a\rangle_{A} V_{a i}, \quad\left|i^{\prime}\right\rangle_{B}=\sum_{b}\left|b^{\prime}\right\rangle_{B} V_{b i}^{*}
$$
其中$V$是幺正矩阵（实际上两个子空间的幺正变换可以无关，但这里我们选用互为共轭的变换）。
$$
\begin{aligned}|\psi\rangle_{A B}=\frac{1}{\sqrt{d}} \sum_{i}|i\rangle_{A} \otimes\left|i^{\prime}\right\rangle_{B} &=\frac{1}{\sqrt{d}} \sum_{i, a, b}|a\rangle_{A} V_{a i} \otimes\left|b^{\prime}\right\rangle_{B} V_{i b}^{\dagger} \\ &=\frac{1}{\sqrt{d}} \sum_{a}|a\rangle_{A} \otimes\left|a^{\prime}\right\rangle_{B} \end{aligned}
$$
同步共轭旋转两个子空间，保留了$|\psi\rangle_{A B}$的形式，也就是说，对A作用$V$且对B作用$V^*$保证了bipartite pure state $|\psi\rangle_{A B}$不变！。

这个例子说明，在$\boldsymbol{\rho}_{A}$（和$\boldsymbol{\rho}_{B}$）**有简并的非零本征值**的情况下，Schmidt form对基矢的选择有模糊性。当然，这个模糊性只生活在**简并的空间**，即只有在简并本征矢张成的空间里，基矢的选择才有模糊性！非简并空间部分没有模糊性，按照前面构造Schmidt decomposition的步骤即可！

##### 2.4.1 Entanglement

对$|\psi\rangle_{A B}$可以用一个正整数**Schmidt number**标记，表示$\boldsymbol{\rho}_{A}$（也即$\boldsymbol{\rho}_{B}$）非零本征值的个数，即Schmidt decomposition项数。这个数可以表征bipartite pure state是否是纠缠态：若Schmidt number大于1，则$|\psi\rangle_{A B}$是纠缠的（不可分的**nonseparable**）；否则不是纠缠的（可分的**separable**）。

一个 **separable** bipartite pure state（Schmidt number=1）是$\mathcal{H}_A$和$\mathcal{H}_B$纯态的直积：
$$
|\psi\rangle_{A B}=|\varphi\rangle_{A} \otimes|\chi\rangle_{B}
$$
于是reduced density matrices $\rho_A=|\varphi\rangle\langle\varphi|$和$\rho_B=|\chi\rangle\langle\chi|$是纯态。任何无法写成上述直积的态均为纠缠态，对应的$\boldsymbol{\rho}_{A}$和$\boldsymbol{\rho}_{B}$是混合态。

当$|\psi\rangle_{A B}$是纠缠态，我们称A和B有量子关联(quantum correlations)。但如果$|\psi\rangle_{A B}$是separable的，也不能说A和B没有关联，比如非纠缠态$|\uparrow\rangle_{A}|\uparrow\rangle_{B}$中A和B的确是关联的——指向同一方向。但是纠缠态中的关联与这种separable state的关联不一样！一大区别是，**纠缠不能局部产生**(entanglement cannot be created locally)。让A和B纠缠的唯一方式是让它们直接相互作用。

非纠缠态$|\uparrow\rangle_{A}|\uparrow\rangle_{B}$可以在A和B不接触的情况下制备，只要发送一个经典的信息给Alice和Bob让他们各自制备沿z轴自旋向上态即可。但是制备纠缠态$\frac{1}{\sqrt{2}}\left(|\uparrow\rangle_{A}|\uparrow\rangle_{B}+|\downarrow\rangle_{A}|\downarrow\rangle_{B}\right)$的唯一方法是对非纠缠态$|\uparrow\rangle_{A}|\uparrow\rangle_{B}$作用一个collective幺正变换。

> **注**：collective unitary transformation指的是，把双系统态作为整体进行演化，从初态$|\uparrow\rangle_{A}|\uparrow\rangle_{B}$演化成双系统态的叠加态，即两个子系统的纠缠态。

仅仅local的幺正变换，比如$U_A\otimes U_B$，和Alice与Bob的local测量，不可能增加这个2qubit态的Schmidt number（从1变成大于1，即无纠缠变成有纠缠），无论他们交流过多少信息。使A和B发生纠缠的唯一办法就是让它们相互靠近产生相互作用。

#### 2.5 Ambiguity of the ensemble interpretation

##### 2.5.1 Convexity(密度矩阵是幺正矩阵的凸子集)

（复习）一个作用在Hilbert空间$\mathcal{H}$的算符$\boldsymbol{\rho}$可以被称为密度算符，只要它满足下述三个条件：

(1) 厄米(self-adjoint/Hermitian)：$\rho=\rho^{\dagger}$.

(2) 非负（半正定positive semidefinite）

(3) $\text{tr}(\rho_A)=1$

> **Definition:**
>
> For a square symmetric matrix is **positive semi-definite** if $\boldsymbol{v}^TH\boldsymbol{v}\geq0,\ \forall\boldsymbol{v}\in\mathcal{R}^n$, and **positive definite** if the inequality holds with equality only for vectors $\boldsymbol{v}=0$. 
>
> For an square Hermitian matrix $M$:
>
> - M is **positive definite** if and only if all of its eigenvalues are **positive**.
> - M is **positive** **semi-definite** if and only if all of its eigenvalues are **non-negative**.

于是，任意给定两个密度矩阵$\boldsymbol{\rho}_1$和$\boldsymbol{\rho}_2$，可以构造另一个密度矩阵是它们的凸线性组合(convex linear combination)：
$$
\boldsymbol{\rho}(\lambda)=\lambda \boldsymbol{\rho}_{1}+(1-\lambda) \boldsymbol{\rho}_{2}
$$
对任意$0\leq\lambda\leq1$均成立。易证$\boldsymbol{\rho}(\lambda)$满足上述条件(1)和(3)，对条件(2)，$\boldsymbol{\rho}_1$和$\boldsymbol{\rho}_2$的正定性保证了
$$
\langle\psi|\boldsymbol{\rho}(\lambda)| \psi\rangle=\lambda\left\langle\psi\left|\boldsymbol{\rho}_{1}\right| \psi\right\rangle+(1-\lambda)\left\langle\psi\left|\boldsymbol{\rho}_{2}\right| \psi\right\rangle \geq 0
$$
于是我们证明了，在d维的Hilbert空间$\mathcal{H}$中，密度算符是$d\times d$厄米算符的一个凸子集(convex subset)。（向量空间的子集称为凸集，如果这个子集包含了连接任意两个元素的线元）

对于一般的密度算符，可以表示成其他密度算符的求和。但是**纯态并不能写成其他态的convex sum**。

> 证明：考虑纯态$\boldsymbol{\rho}=|\psi\rangle\langle\psi|$，定义$|\psi\rangle$的正交态为$|\psi_\perp\rangle$，假设$\boldsymbol{\rho}$可以表示成convex sum，则
> $$
> \begin{aligned}\left\langle\psi_{\perp}|\boldsymbol{\rho}| \psi_{\perp}\right\rangle= 0 &=\lambda\left\langle\psi_{\perp}\left|\boldsymbol{\rho}_{1}\right| \psi_{\perp}\right\rangle+(1-\lambda)\left\langle\psi_{\perp}\left|\boldsymbol{\rho}_{2}\right| \psi_{\perp}\right\rangle \end{aligned}
> $$
> 由于等号右边是两个非负数相加且和为零，只能是两项均为零。由假设$\lambda$不是0或1，则$\boldsymbol{\rho}_{1}$和$\boldsymbol{\rho}_{2}$均与$|\psi_\perp\rangle$正交$\left\langle\psi_{\perp}\left|\boldsymbol{\rho}_{1}\right| \psi_{\perp}\right\rangle=0=\left\langle\psi_{\perp}\left|\boldsymbol{\rho}_{2}\right| \psi_{\perp}\right\rangle$，由于$|\psi_\perp\rangle$是任意与$|\psi\rangle$正交的态，因此$\boldsymbol{\rho}_{1}=\boldsymbol{\rho}_{2}=\boldsymbol{\rho}$。$\blacksquare$

在凸集中的矢量，如果不能表示成凸集中其他矢量的线性组合，则称为该凸集的extremal points。因此“纯态密度矩阵”是“密度矩阵凸集”的extremal points。此外，**只有纯态是extremal points**，因为任意混合态都可写成对角化形式$\boldsymbol{\rho}=\sum_ip_i|i\rangle\langle i|$，因此混合态是纯态的凸线性组合。

在讨论Bloch sphere时我们已经接触了这个结构。在三维空间中，$2\times2$密度矩阵是所有$2\times2$厄米矩阵的一个3维凸子集，这个凸子集是个trace为1的3维单位球。这个子集是凸的，所有extremal points在球面上。类似的，$d\times d$密度算符是$d\times d$厄米矩阵的$(d^2-1)$维凸子集，这个凸子集trace为1，且所有extremal points都是纯态。

但是$2\times2$的情况不具代表性：**对于$d>2$，密度矩阵凸子集的边界不一定都是纯态**！凸子集边界上的态是所有具有至少一个零本征值的密度矩阵（因为邻域内有负本征值的矩阵）。

> **注**：边界上的点满足$\text{det}\boldsymbol{\rho}=0$【需要几何上的证明】，即至少有一个零本征值。

这个条件对于$d=2$对应的是纯态，但对于$d>2$就不一定是纯态，因为非零本征值的数量可以大于1个！

##### 2.5.2 Ensemble preparation

设想有人制备两个态**其中之一**：以概率$\lambda$制备$\boldsymbol{\rho}_{1}$，以概率$1-\lambda$制备$\boldsymbol{\rho}_{2}$（此处用到了随机数生成器）。要测量可观测量$M$的均值，我们同时取“制备的态的选择$\boldsymbol{\rho}_{1}$or$\boldsymbol{\rho}_{2}$”和“量子测量结果$\langle\cdot\rangle$”的平均：
$$
\begin{aligned}\langle\boldsymbol{M}\rangle &=\lambda\langle\boldsymbol{M}\rangle_{1}+(1-\lambda)\langle\boldsymbol{M}\rangle_{2} \\ &=\lambda \operatorname{tr}\left(\boldsymbol{M} \boldsymbol{\rho}_{1}\right)+(1-\lambda) \operatorname{tr}\left(\boldsymbol{M} \boldsymbol{\rho}_{2}\right) \\ &=\operatorname{tr}(\boldsymbol{M} \boldsymbol{\rho}(\lambda)) \end{aligned}
$$
任意可观测量$M$的期望值和一开始就制备混合态$\boldsymbol{\rho}(\lambda)$的测量结果没有区别！因此，这提供了操作上的方便，要制备混合态（纯态的凸线性组合），只需要按概率制备纯态即可。

- 实际上，对任意**混合态**$\boldsymbol{\rho}$，有无数种线性组合表达式，所以有无数种制备方式，但都能得到完全相同的可观测量的测量结果。

- 但是**纯态**就不一样，只有一种方式制备（这就是“纯”的含义）。每个纯态都是某些可观测量的本征值，比如，对于纯态$\boldsymbol{\rho}=|\psi\rangle\langle\psi|$，投影算符$\boldsymbol{E}=|\psi\rangle\langle\psi|$的测量结果为1，即单个qubit的纯态总是某个方向上的“自旋向上”态。因为$\boldsymbol{\rho}=|\psi\rangle\langle\psi|$是唯一测量$\boldsymbol{E}$能100%得到1的态，所以不可能有其他制备这个态的方式了。

综上，**纯态的制备是唯一的，但混合态的制备总是模糊(ambiguous)的**。有多模糊？取决于这个混合态有多少种写成纯态凸求和的方式，或更数学点，混合态矩阵有多少种写成extremal states 凸求和的方式？

举例：最大混合态$\boldsymbol{\rho}=\frac{1}{2}\boldsymbol{I}$（对应Bloch ball $\vec{P}=0$，本征值$1/2$二重简并）。它可写成$\boldsymbol{\rho}=\frac{1}{2}\left(|\uparrow_{z}\rangle\langle\uparrow_{z}|+|\downarrow_{z}\rangle\langle\downarrow_{z}|\right)$，所以只需等概率1/2制备$|\uparrow_{z}\rangle$或$|\downarrow_{z}\rangle$即可。此外还可写成$\boldsymbol{\rho}=\frac{1}{2}\left(|\uparrow_{x}\rangle\langle\uparrow_{x}|+|\downarrow_{x}\rangle\langle\downarrow_{x}|\right)$。这两种制备方式无疑是不同的，但只测量自旋无法分辨两者，因为自旋的期望值均为0。更一般地，Bloch ball中心点是任意两个中心对称点的求和，即只要等概率制备$|\uparrow_{\hat{n}}\rangle$或$|\downarrow_{\hat{n}}\rangle$就能得到$\boldsymbol{\rho}=\frac{1}{2}\boldsymbol{I}$。

只有当$\boldsymbol{\rho}$有两个或以上简并本征值时（三维情况是$\vec{P}=0$），才能从mutually orthogonal pure states系综中产生$\boldsymbol{\rho}$的不同制备方式，但没必要局限于mutually orthogonal pure states。【存疑，应该指的是上一段内容吧？】可以考虑Bloch ball内部的点（本征值不简并，即$|\vec{P}|$非零）
$$
\rho(\vec{P})=\frac{1}{2}(I+\vec{P} \cdot \vec{\sigma})
$$
其中$0<|\vec{P}|<1$。如果$\vec{P}$可以表示为连接球面两点$\hat{n}_{1}$和$\hat{n}_{2}$连线上的某个点$\vec{P}=\lambda \hat{n}_{1}+(1-\lambda) \hat{n}_{2}$，那么它也可以写成（参考Eq.$(\ref{equivalence})$）
$$
\begin{align}
\rho(\vec{P})&=\frac{\lambda}{2}(I+\hat{n}_1\cdot \vec{\sigma})+\frac{1-\lambda}{2}(I+\hat{n}_2\cdot \vec{\sigma})\nonumber\\&=\lambda \rho\left(\hat{n}_{1}\right)+(1-\lambda) \rho\left(\hat{n}_{2}\right)
\end{align}
$$
显然，任意穿过$\vec{P}$点的连接Bloch sphere球面两点的线段都对应一个$\rho(\vec{P})$的表达式。

这种highly ambiguous的混合态制备方式是量子信息**区别于经典概率分布**的一大特征。比如，考虑单个经典bit的概率分布，它的两种极端分布(extremal distributions)是0或1以100%概率出现，任意概率分布都是这两个极端点(extremal points)的convex sum。同样地，如果有d个可能的态，则有d种极端分布，任意概率分布都能唯一分解成极端点的线性组合（概率分布的凸集是一个单形体simplex，即d个顶点的convex hull）。

> **单形体simplex**：内部任意点p是其顶点的线性组合。在1维空间中，线段是单形体，在二维空间中，三角形是单形体，在三维空间中，四面体是单形体，以此类推。

如果出现0，1，2的概率分别是21%，33%，46%，那么只有唯一一种产生这个分布的制备方式。

##### 2.5.3 Faster than light?

通过“A与B纠缠导致A出现混合态”进一步讨论混合态制备的ambiguous性质。

若A处于混合态$\boldsymbol{\rho}_A=\frac{1}{2}I=\frac{1}{2}\left(|\uparrow_{z}\rangle\langle\uparrow_{z}|+|\downarrow_{z}\rangle\langle\downarrow_{z}|\right)$，它可以由下面的entangled bipartite pure state with the Schmidt decomposition对B求trace产生：
$$
|\psi\rangle_{A B}=\frac{1}{\sqrt{2}}\left(\left|\uparrow_{z}\right\rangle_{A}\left|\uparrow_{z}\right\rangle_{B}+\left|\downarrow_{z}\right\rangle_{A}\left|\downarrow_{z}\right\rangle_{B}\right)
$$
因此，$\boldsymbol{\rho}_A$的ensemble interpretation（各以概率1/2制备$|\uparrow_{z}\rangle_{A}$和$|\downarrow_{z}\rangle_{A}$）可以通过测量B实现。我们在基$\{|\uparrow_{z}\rangle_{B},|\downarrow_{z}\rangle_{B}\}$下测量B，如果得到$|\uparrow_{z}\rangle_{B}$，那么就制备了$|\uparrow_{z}\rangle_{A}$，反之亦然。

但是在这个例子中，因为$\boldsymbol{\rho}_A$有简并的非零本征值，所以Schmidt basis并不唯一。我们可以同步对A和B做共轭幺正变换而不改变bipartite pure state的形式$|\psi\rangle_{A B}$（注意对A施加$V$则必须对B施加$V^*$，见Chap2.4）。因此，对任意单位向量$\hat{n}$，$|\psi\rangle_{A B}$都有Schmidt decomposition形式：
$$
|\psi\rangle_{A B}=\frac{1}{\sqrt{2}}\left(\left|\uparrow_{\hat{n}}\right\rangle_{A}\left|\uparrow_{\hat{n}^{\prime}}\right\rangle_{B}+\left|\downarrow_{\hat{n}}\right\rangle_{A}\left|\downarrow_{\hat{n}^{\prime}}\right\rangle_{B}\right)
$$
由此可以看到，只要选择合适的基$\{|\uparrow_{\hat{n}^{\prime}}\rangle_{B},|\downarrow_{\hat{n}^{\prime}}\rangle_{B}\}$来测量B（$\hat{n}'$是对B的基施加幺正变换$V^*$得到的），我们就能把$\boldsymbol{\rho}_A$表示成any interpretation as an ensemble of two pure states。

这个性质揭示了**超光速通讯的可能**。假设制备了一堆$|\psi\rangle_{A B}$，Alice把所有A qubits带到另一个星系，Bob留下B qubits在地球上。当Bob想发射1bit信息给Alice，他选择用$\boldsymbol{\sigma}_1$或$\boldsymbol{\sigma}_3$测量他的所有自旋，于是Alice的自旋就变成了$\{|\uparrow_{x}\rangle_{A},|\downarrow_{x}\rangle_{A}\}$或$\{|\uparrow_{z}\rangle_{A},|\downarrow_{z}\rangle_{A}\}$的系综（此处$V$选择实矩阵$V=V^*$，于是$\hat{n}=\hat{n}'$）。为了得到信息，Alice立刻测量她的自旋，来看到底是哪个ensemble。但这个scheme有缺陷。尽管两种制备方式不同，但两个ensemble均由同一个密度矩阵$\boldsymbol{\rho}_A$描述，所以Alice不可能通过测量来分辨这两个ensemble，也就无法获取Bob的动作信息。换句话说，这个信息是unreadable。

但为什么我们仍说两种制备方式是不同的呢？因为我们能**通过某种经典的方式区分它们**。考虑Bob要么(1)沿着$\hat{z}$轴测量自旋，要么(2)沿着$\hat{x}$轴测量自旋，然后通过经典的星际电话呼叫Alice，但不告诉她做了(1)还是(2)，只是告诉她测量结果：“第一个自旋向上，第二个向下……”现在Alice对她的自旋做(1)或(2)的测量。如果两人沿着相同轴测量，Alice会发现每一个结果都与Bob符合；如果两人沿不同方向（正交方向）测量，Alice会发现她的结果与Bob没有关联，符合与不符合各占大约一半。如果Bob保证确实做了(1)或(2)，且没有任何制备和测量误差，那么只要Alice的测量结果与Bob不同，她就会知道两人的基选择不同（尽管Bob并没告诉过她基的信息）。如果所有结果都吻合，且对许多自旋重复测量都是这样，Alice就有足够统计上的自信确信她和Bob用的是同一个轴（尽管偶尔有测量误差，但只要出错率足够小，统计检测还是可靠的）。所以Alice还是有办法区分Bob的两种制备方式，但这就不是超光速了，因为Alice先得接到Bob的经典跨星系电话才能进行测试。

##### 2.5.4 Quantum erasure

我们说过$\boldsymbol{\rho}_A=\frac{1}{2}\boldsymbol{I}$描述了纯态$|\uparrow_{z}\rangle_{A}$和$|\downarrow_{z}\rangle_{A}$的非相干混合(incoherent mixture)，这个混合态需要与相干叠加态区别开：
$$
\left|\uparrow_{x}, \downarrow_{x}\right\rangle=\frac{1}{\sqrt{2}}\left(\left|\uparrow_{z}\right\rangle \pm\left|\downarrow_{z}\right\rangle\right)
$$
在相干叠加态，两个态的相对相位有可观测的结果——可以用来区分两个态。而在混合态里，相对相位完全无法观测到。当A与另一个我们无法接触到的B纠缠时，A系统两个态的叠加变得不再相干。

只有当我们不知道自旋处于哪个本征态时，这两个本征态才会相干，即相对相位可以被观测到。此外，干涉只有在**原理上不可能弄清**A的自旋沿z轴向上还是向下的情况下发生。而一旦A与B发生纠缠，A就会退相干，因为我们**原理上可以**通过测量B知道A沿着z轴的自旋状态。

“纠缠导致退相干”是在某种条件下才有意义的。假设Bob沿着**x轴**测量B的自旋，得到$|\uparrow_{x}\rangle_{B}$或$|\downarrow_{x}\rangle_{B}$，然后把结果发给Alice。现在Alice的自旋处于x方向的纯态，要么是$|\uparrow_{x}\rangle_{A}$，要么是$|\downarrow_{x}\rangle_{A}$，但这两个态各自又是z方向$|\uparrow_{z}\rangle_{A}$和$|\downarrow_{z}\rangle_{A}$的相干叠加。We have managed to recover the purity of Alice’s spin before the jaws of decoherence could close! 【存疑，此句不理解】

假设Bob让他的自旋经过一个沿**z轴**的Stern–Gerlach仪器，那么Alice的自旋不可能是$|\uparrow_{z}\rangle_{A}$和$|\downarrow_{z}\rangle_{A}$的相干叠加，而是变成z方向的某个纯态，即**沿z轴变得没有相干性**。Bob只需要观测他的自旋如何偏转确定z方向自旋，就能推测出Alice的自旋是沿z轴向上还是向下的纯态。但是！我们假设Bob不观测，而是不加记录地重新合并两束粒子束，然后让该粒子束再经过第二个沿**x轴**的Stern–Gerlach仪器，这次他观测x方向的自旋，并把$\boldsymbol{\sigma}_1$的测量结果告诉Alice，那么Alice就知道她是$|\uparrow_{x}\rangle_{A}$还是$|\downarrow_{x}\rangle_{A}$，而这两个态各自都是沿z轴的相干态，于是Alice的自旋**沿z轴的相干性就恢复了**！

这种情况叫**quantum eraser**。把A和B的自旋纠缠起来，会产生“measurement situation”，使得$|\uparrow_{z}\rangle_{A}$和$|\downarrow_{z}\rangle_{A}$的相干性丢失，因为我们原理上可以测量B沿z轴的自旋来知道A沿z轴的自旋。但是当我们**沿x轴**测量B的自旋，关于A**沿z轴**的自旋信息就被“擦除”了。无论结果是$|\uparrow_{x}\rangle_{B}$还是$|\downarrow_{x}\rangle_{B}$都不会告诉我们关于A沿z轴的自旋信息，因为Bob很小心地没有获取第一个（**沿z轴**的）Stern–Gerlach仪器的测量结果。因此，当Alice从Bob那听到他的$\boldsymbol{\sigma}_1$测量结果后，A的自旋还是可以变为$|\uparrow_{z}\rangle_{A}$和$|\downarrow_{z}\rangle_{A}$的相干叠加态。

**从系综角度最容易理解quantum eraser**。Alice从系综$\boldsymbol{\rho}_A=\frac{1}{2}\boldsymbol{I}$中获得了很多处于这个混合态的自旋，显然此时她无法观测到$|\uparrow_{z}\rangle_{A}$和$|\downarrow_{z}\rangle_{A}$的干涉。当Bob沿x轴进行测量（选定一组基），这个系综的制备方式就唯一确定了。但是，这对Alice能获得的信息没有影响——她的自旋仍旧由密度矩阵$\boldsymbol{\rho}_A=\frac{1}{2}\boldsymbol{I}$描述。但是当Alice接到Bob的电话告诉她哪几个编号的自旋的$\boldsymbol{\sigma}_1$测量结果为“向上”后，她可以选择所有这些自旋的编号，构成处于$|\uparrow_{x}\rangle_{A}$态的“子系综”。Bob发来的信息帮助Alice从maximally mixed state中丢弃purity，获得一堆相干态的子系综。

关于quantum eraser的另一个问题是**delayed choice**，即上述情形对于Alice和Bob是对称的，无论谁先测量都一样。因为，如果Alice和Bob的测量是空间上分隔的事件，我们就无法确知谁先发生，因为时间先后依赖于观察者的坐标系。对于$\boldsymbol{\rho}_A=\frac{1}{2}\boldsymbol{I}$，在Bob决定沿哪个轴测量他的自旋之前，Alice可以先沿x轴测量她的所有自旋并记录下来，过一周后，Bob也许才刚刚决定要用基$\{|\uparrow_{\hat{n}}\rangle_{A},|\downarrow_{\hat{n}}\rangle_{A}\}$来制备Alice的态（这就是“delayed choice”）。然后Bob打电话告诉Alice哪几个编号的自旋是$|\uparrow_{\hat{n}}\rangle_{A}$，Alice可以检查她的测量记录来验证下式是否满足：$\left\langle\sigma_{1}\right\rangle_{\hat{n}}=\hat{n} \cdot \hat{x}$，无论Bob在Alice测量前还是测量后再制备Alice的自旋，这个式子都成立。【存疑，不理解】

>把上段过程写出来：
>
>**case1**. Bob在Alice测量前制备Alice的自旋（上下顺序表示时间先后，下同）：
>$$
>B:\ |\uparrow_{\hat{n}}\rangle_{A}\ |\downarrow_{\hat{n}}\rangle_{A}\ |\uparrow_{\hat{n}}\rangle_{A}\cdots\\
>A:\ |\uparrow_{\hat{x}}\rangle_{A}\ |\downarrow_{\hat{x}}\rangle_{A}\ |\downarrow_{\hat{x}}\rangle_{A}\cdots
>$$
>Alice从Bob那得到所有$|\uparrow_{\hat{n}}\rangle_{A}$的自旋编号，相当于对态$|\uparrow_{\hat{n}}\rangle_{A}$求$\sigma_1$的均值，结果为$\hat{n} \cdot \hat{x}$。
>
>**case 2**. Bob在Alice测量后制备Alice的自旋：
>$$
>A:\ |\uparrow_{\hat{x}}\rangle_{A}\ |\uparrow_{\hat{x}}\rangle_{A}\ |\downarrow_{\hat{x}}\rangle_{A}\cdots\\
>B:\ |\uparrow_{\hat{n}}\rangle_{A}\ |\downarrow_{\hat{n}}\rangle_{A}\ |\uparrow_{\hat{n}}\rangle_{A}\cdots
>$$
>【存疑，这个case如何理解？】

我们宣称$\boldsymbol{\rho}_A$给出了关于子系统A的完整描述，因为它可以得出对A的任何测量的结果。有人或许会反驳说quantum eraser现象给出反例，因为Alice从Bob那获得信息后，可以从mixture state中复原pure state，我们怎么能说Alice对A的了解已经全部包含在$\boldsymbol{\rho}_A$里了呢？

作者的解释是：Quantum erasure illustrates the principle that “information is physical.” 实际上，“$\boldsymbol{\rho}_A$”与“$\boldsymbol{\rho}_A$+Alice从Bob得到的信息”不是一回事。这个信息（给子系综贴上了标签）改变了物理描述。我们应该把Alice的“state of knowledge”也考虑进Alice自旋系统的描述中来。一个“Alice不知道哪些自旋是向上”的系综，与“Alice知道哪些自旋是向上”的系综是不同的。这个“state of knowledge”不一定是人脑，它可以仅仅是对子系综的一系列label。

##### 2.5.5 The HJW theorem 

至此，我们只讨论了单个qubit的，由密度算符$\boldsymbol{\rho}_A=\frac{1}{2}\boldsymbol{I}$描述的quantum eraser。这个讨论可以大大延拓。

我们已知一个混合态可以有无数种表示成“纯态构成的系综”的形式。对一般的密度矩阵的某一个具体实现（对应之前例子中的$\frac{1}{2}I=\frac{1}{2}\left(|\uparrow_{z}\rangle\langle\uparrow_{z}|+|\downarrow_{z}\rangle\langle\downarrow_{z}|\right)$）：
$$
\boldsymbol{\rho}_{A}=\sum_{i} p_{i}\left|\varphi_{i}\right\rangle\left\langle\varphi_{i}\right|, \quad \sum p_{i}=1\label{ensemble}
$$
其中$\{|\varphi_{i}\rangle_A\}$是归一化的向量，但它们**不一定相互正交**。不管怎样，$\boldsymbol{\rho}_A$可以表示成一个系综，里面每个纯态$|\varphi_{i}\rangle\langle\varphi_{i}|$以概率$p_i$发生。

对任意一个$\boldsymbol{\rho}_{A}=\sum_{i} p_{i}\left|\varphi_{i}\right\rangle\left\langle\varphi_{i}\right|$，我们可以构造它的一个“purification”——purification指的是一个双粒子系统的**纯态**$|\Phi_1\rangle_{AB}$，对$\mathcal{H}_B$做partial trace就能得到$\boldsymbol{\rho}_{A}$。一个purification的例子是
$$
|\Phi_1\rangle_{AB}=\sum_i\sqrt{p_i}|\varphi_i\rangle_A\otimes|\alpha_i\rangle_B
$$
其中$|\alpha_i\rangle_B\in\mathcal{H}_B$是正交归一基：$_B\langle\alpha_i|\alpha_i\rangle_B=\delta_{ij}$。显然有$\text{tr}_B(|\Phi_1\rangle\langle\Phi|)=\boldsymbol{\rho}_{A}$。

我们可以用基$\{|\alpha_i\rangle_B\}$对B测量（$|\alpha_i\rangle_B$'s张成的Hilbert空间不一定是整个$\mathcal{H}_B$，但是对于态$|\Phi_1\rangle_{AB}$，测量B的结果不可能出现正交于所有给定的$|\alpha_i\rangle_B$'s的B的态）。在$|\Phi_1\rangle_{AB}$这个态下$|\alpha_i\rangle_B$出现的概率为$p_i$，此时制备了A的纯态$|\varphi_{i}\rangle\langle\varphi_{i}|$。所以，只要给定了$\boldsymbol{\rho}_{A}$的一个purification$|\Phi_1\rangle_{AB}$，我们可以对B做测量来实现$\boldsymbol{\rho}_{A}$的ensemble interpretation。当知道了B的测量结果后，我们就相当于从混合态$\boldsymbol{\rho}_{A}$中提取出了A的一个纯态$|\varphi_{i}\rangle_A$。上述内容是之前讨论的推广，之前我们讨论的是测量B沿z轴的自旋来制备A的态$|\uparrow_z\rangle_A$。

要推广quantum eraser的概念，我们要对B做不同的测量来构造$\boldsymbol{\rho}_{A}$的另一个ensemble interpretation。令由纯态构成的系综（对应之前例子中的$\frac{1}{2}I=\frac{1}{2}\left(|\uparrow_{x}\rangle\langle\uparrow_{x}|+|\downarrow_{x}\rangle\langle\downarrow_{x}|\right)$）：
$$
\boldsymbol{\rho}_{A}=\sum_{\mu} q_{\mu}\left|\psi_{\mu}\right\rangle\left\langle\psi_{\mu}\right|
$$
是上述同一个$\boldsymbol{\rho}_{A}$的不同实现形式。对这个系综，也有其对应的purification
$$
\left|\Phi_{2}\right\rangle_{A B}=\sum_{\mu} \sqrt{q_{\mu}}\left|\psi_{\mu}\right\rangle_{A} \otimes\left|\beta_{\mu}\right\rangle_{B}
$$
其中$\{|\beta_{\mu}\rangle_B\}'s\in\mathcal{H}_B$是正交归一基，对这个态$\left|\Phi_{2}\right\rangle_{A B}$，我们可以对B做测量把它投影到基$\{|\beta_{\mu}\rangle_B\}$上，实现A的ensemble。

现在问题来了，$|\Phi_1\rangle_{AB}$和$\left|\Phi_{2}\right\rangle_{A B}$有何联系？容易证明两者相差一个仅作用于$\mathcal{H}_B$空间的幺正变换：

> 【存疑，咋证明？】我觉得是，先把A以$|\psi\rangle$为基的态对角化，再变换成$|\varphi\rangle$基的表示形式，然后系数全部并到B空间。但我怀疑他这里写错了。

$$
\left|\Phi_{1}\right\rangle_{A B}=\left(\boldsymbol{I}_{A} \otimes \boldsymbol{U}_{B}\right)\left|\Phi_{2}\right\rangle_{A B}\label{connection}
$$
或写成
$$
\left|\Phi_{1}\right\rangle_{A B}=\sum_{\mu}\sqrt{q_{\mu}}\left|\psi_{\mu}\right\rangle_{A} \otimes\left|\gamma_{\mu}\right\rangle_{B}
$$
其中$\left|\gamma_{\mu}\right\rangle_{B}=\boldsymbol{U}_{B}\left|\beta_{\mu}\right\rangle_{B}$是$\mathcal{H}_B$空间的另一组正交基。于是，$\boldsymbol{\rho}_{A}$的purification$|\Phi_1\rangle_{AB}$是唯一的【存疑，原句是there is a single purification】，通过选择测量B系统合适的可观测量，就能实现$\{|\varphi_{i}\rangle_A\}$ensemble或$\{|\psi_{\mu}\rangle_A\}$ensemble。

同样地，还可以考虑$\boldsymbol{\rho}_{A}$的其他ensemble实现，每一个ensemble中纯态的数量均不超过d。然后选择d维Hilbert空间$\mathcal{H}_B$，和纯态$|\Phi\rangle_{A B} \in \mathcal{H}_{A} \otimes \mathcal{H}_{B}$，使得每一个ensemble都可以通过对B进行合适的测量来实现。这叫**HJW theorem** (for Hughston, Jozsa, and Wootters), it expresses the quantum eraser phenomenon in its most general form. 

实际上HJW theorem是Schmidt decomposition的引理。$|\Phi_1\rangle_{AB}$和$\left|\Phi_{2}\right\rangle_{A B}$都有各自的Schmidt decomposition，由于两者对B求partial trace都能得到同样的$\boldsymbol{\rho}_{A}$，他们的Schmidt decomposition一定具有形式
$$
\begin{aligned}\left|\Phi_{1}\right\rangle_{A B} &=\sum_{k} \sqrt{\lambda_{k}}|k\rangle_{A} \otimes\left|k_{1}^{\prime}\right\rangle_{B} \\\left|\Phi_{2}\right\rangle_{A B} &=\sum_{k} \sqrt{\lambda_{k}}|k\rangle_{A} \otimes\left|k_{2}^{\prime}\right\rangle_{B} \end{aligned}
$$
其中$\lambda_k$'s是$\boldsymbol{\rho}_{A}$的本征值，$|k\rangle_{A}$'s是相应的本征矢。但因为$\{|k_{1}^{\prime}\rangle_{B} \}$和$\{|k_{2}^{\prime}\rangle_{B} \}$都是$\mathcal{H}_{B}$的正交归一基，一定有幺正变换使得
$$
\left|k_{1}^{\prime}\right\rangle_{B}=\boldsymbol{U}_{B}\left|k_{2}^{\prime}\right\rangle_{B}
$$
这就推出了Eq.$(\ref{connection})$。【存疑，A的基矢在Eq.$(\ref{connection})$两个态里并不一样啊】

在纯态系综Eq.$(\ref{ensemble})$里，我们可以说，纯态$|\varphi_{i}\rangle_A$进行了非相干的混合(mixed incoherently)——在A系统中的观察者无法探测到这些态的相对相位。它们无法干涉的原因是，原理上可以通过对B进行投影到正交归一基$\{|\alpha_i\rangle_B\}$的测量而知道which representative of the ensemble is actually realized。然而，如果投影到B的另一组正交基$\{|\gamma_\mu\rangle_B\}$，并把测量结果告诉A，就能从A的ensemble提取出纯态$|\psi_\mu\rangle_A$，即使它是$|\varphi_i\rangle_A$'s的相干叠加态。实际上，用基$\{|\gamma_\mu\rangle_B\}$测量B，“擦除”了“which way” information——A处于$|\varphi_i\rangle_A$还是$|\varphi_j\rangle_A$态。在这个意义下，HJW theorem表征了最一般的quantum eraser。背后的物理正是“information is physical”——测量B的信息一旦传输给了A，就会改变A状态的physical description。【存疑，不理解】

#### 2.6 How far apart are two quantum states?

##### 2.6.1 Fidelity and Uhlmann’s theorem 

两个纯态$|\psi\rangle$和$|\phi\rangle$的远离程度由$|\langle\psi|\phi\rangle|^2$和1的距离来量化，称为fidelity。

两个密度算符$\boldsymbol{\rho}$和$\boldsymbol{\sigma}$的fidelity定义为（也有人把这个量的开根号称为fidelity）
$$
F(\boldsymbol{\rho}, \boldsymbol{\sigma}) \equiv(\operatorname{tr} \sqrt{\boldsymbol{\rho}^{\frac{1}{2}} \boldsymbol{\sigma} \boldsymbol{\rho}^{\frac{1}{2}}})^{2}
$$
其中，对一个positive semidefinite matrix $M$，$\sqrt{M}$表示它的唯一的positive square root。

> A **positive semidefinite matrix** is a Hermitian matrix all of whose eigenvalues are nonnegative.
>
> (from [wiki](**https://en.wikipedia.org/wiki/Square_root_of_a_matrix**)) In general, a matrix can have several square roots. But a **positive-semidefinite** matrix has precisely **one** positive-semidefinite square root, which can be called its principal square root. More generally, an $n×n$ matrix with $n$ distinct nonzero eigenvalues has $2^n$ square roots, but precisely **one** positive-semidefinite square root.
>
> **Proof**: Such a matrix, *A*, has a decomposition $VDV^{-1}$ where $V$ is the matrix whose columns are eigenvectors of *A* and *D* is the diagonal matrix whose diagonal elements are the corresponding *n* eigenvalues $\lambda_i$. Thus the square roots of $A$ are given by $VD^{1/2} V^{−1}$, where $D^{1/2}$ is any square root matrix of $D$, which, for distinct eigenvalues, must be diagonal with diagonal elements equal to square roots of the diagonal elements of $D$; since there are two possible choices for a square root of each diagonal element of $D$, there are $2^n$ choices for the matrix $D^{1/2}$. This also leads to a proof of the above observation, that a positive-definite matrix has precisely one positive-definite square root.

fidelity非负，当$\boldsymbol{\rho}$和$\boldsymbol{\sigma}$have support on mutually orthogonal subspaces时为零，当且仅当两个态相同时达到最大值1。

- 若$\boldsymbol{\rho}$是纯态$\boldsymbol{\rho}=|\psi\rangle\langle\psi|$，即满足$\boldsymbol{\rho}^2=\boldsymbol{\rho}$或$\boldsymbol{\rho}=\boldsymbol{\rho}^{1/2}$，则有

$$
F(\rho, \sigma)=\left(\operatorname{tr}\sqrt{\left|\psi_{\rho}\right\rangle\left\langle\psi_{\rho}|\sigma| \psi_{\rho}\right\rangle\left\langle\psi_{\rho}\right|}\right)^{2}=\left\langle\psi_{\rho}|\sigma| \psi_{\rho}\right\rangle \left(\operatorname{Tr}\sqrt{\left|\psi_{\rho}\right\rangle\left\langle\psi_{\rho}\right|}\right)^{2}=\left\langle\psi_{\rho}|\sigma| \psi_{\rho}\right\rangle
$$

- 若$\boldsymbol{\rho}$和$\boldsymbol{\sigma}$都是纯态，$\boldsymbol{\rho}=|\psi_\rho\rangle\langle\psi_\rho|$和$\boldsymbol{\sigma}=|\psi_\sigma\rangle\langle\psi_\sigma|$，则$F(\rho, \sigma)=|\langle\psi_\rho|\psi_\sigma\rangle|^2$，退化到简单的距离定义。

假设我们对$\boldsymbol{\rho}=|\psi\rangle\langle\psi|$进行orthogonal measurement——只有两种测量结果：若为$|\psi\rangle$输出"Yes"，若为与$|\psi\rangle$正交的态则输出"No"。于是fidelity的含义为得到"Yes"的概率。

>**我注**：将$\boldsymbol{\sigma}$分解成$\boldsymbol{\sigma}=p|\psi\rangle\langle\psi|+(1-p)|\psi_\perp\rangle\langle\psi_\perp|$，则$F(\rho, \sigma)=\left\langle\psi_{\rho}|\sigma| \psi_{\rho}\right\rangle=p$。

**fidelity**也可以用$L^1$ norm（也叫作trace norm）定义：
$$
F(\boldsymbol{\rho}, \boldsymbol{\sigma})=\left\|\boldsymbol{\sigma}^{\frac{1}{2}} \boldsymbol{\rho}^{\frac{1}{2}}\right\|_{1}^{2}
$$
其中$L^1$ norm定义为：
$$
\|\boldsymbol{A}\|_{1}=\operatorname{tr} \sqrt{\boldsymbol{A}^{\dagger} \boldsymbol{A}}
$$
若$\boldsymbol{A}$是厄米的，那么$\|\boldsymbol{A}\|_{1}$就是其特征值取绝对值后再求和。

$F(\boldsymbol{\rho}, \boldsymbol{\sigma})$**关于两个自变量是对称的**。证明：对任意厄米算符$\boldsymbol{A}$和$\boldsymbol{B}$，$L^1$ norm满足$\|\boldsymbol{AB}\|_1=\|\boldsymbol{BA}\|_1$。这是因为$\boldsymbol{BAAB}$和$\boldsymbol{ABBA}$有相同的本征值集合——若$|\psi\rangle$是$\boldsymbol{ABBA}$本征值为$\lambda$的本征态，那么$\boldsymbol{BA}|\psi\rangle$是$\boldsymbol{BAAB}$本征值为$\lambda$的本征态。所以$\text{tr}\sqrt{\boldsymbol{BAAB}}=\text{tr}\sqrt{\boldsymbol{ABBA}}$。【存疑】

下面讨论两个密度算符的“fidelity”和“它们各自purifications的overlap”之间的关系。$\boldsymbol{\rho}_A$的purification $|\Phi\rangle_{AB}$满足$\boldsymbol{\rho}_A=\text{tr}_B(|\Phi\rangle\langle\Phi|)$。若A的密度矩阵能写成纯态形式$\boldsymbol{\rho}_A=\sum_i|i\rangle\langle i|)$，其中$\{|i\rangle_A\}$是A的正交归一基，则某个特定的purification可写成
$$
|\Phi_\boldsymbol{\rho}\rangle=\sum_i\sqrt{p_i}|i\rangle_A\otimes|i\rangle_B
$$
其中$\{|i\rangle_B\}$是B的正交归一基。根据HJW定理，一般的purification具有形式
$$
|\Phi_\boldsymbol{\rho}(V)\rangle=I\otimes V|\Psi_\boldsymbol{\rho}\rangle
$$






#### 附录

**我们详细描述对一般的双系统态$|\psi\rangle_{AB}=\sum_{i,\mu}a_{i\mu}|i\rangle_A\otimes|\mu\rangle_B$，先变换到A的Schmidt bases使得$\boldsymbol{\rho}_{A}$对角的过程。**

假设我们需要从A的正交基$\{|i\rangle_A\}$幺正变换到Schmidt bases$\{|j\rangle_A\}$，使得$\boldsymbol{\rho}_{A}$对角。对原先非对角的$\boldsymbol{\rho}_{A}$：我们对其做Schmidt对角化，得到对角化后的本征矢$\{|j\rangle_A\}$和相应的幺正变换$U$。幺正变换可写为
$$
|j\rangle=\sum_i U_{ji}|i\rangle\text{ or }|i\rangle=\sum_j U^\dagger_{ij}|j\rangle
$$
于是双系统态变成了
$$
|\psi\rangle_{AB}=\sum_{i,j,\mu}a_{i\mu}U^\dagger_{ij}|j\rangle_A\otimes|\mu\rangle_B
$$

- 在一般正交归一基$\{|i\rangle_A\}$下有非对角形式
  $$
  \begin{align}
  \boldsymbol{\rho}_{A}=\text{tr}_B(|\psi\rangle\langle\psi|)=\sum_{i,i'}\left(\sum_\mu a_{i\mu}a^*_{i'\mu}\right)|i\rangle_A\ _A\langle i'|
  \end{align}
  $$
  因此$\text{tr}_A\boldsymbol{\rho}_{A}=\sum_{i\mu}a_{i\mu}a^*_{i\mu}=1$。

- 在Schmidt bases$\{|j\rangle_A\}$下有对角形式
  $$
  \begin{align}
  \boldsymbol{\rho}_{A}&=\text{tr}_B(|\psi\rangle\langle\psi|)=\text{tr}_B\left(\sum_{i,j,\mu}a_{i\mu}U^\dagger_{ij}|j\rangle_A\otimes|\mu\rangle_B\right)\left(\sum_{i',j',\nu}a_{i'\nu}U_{i'j'}\langle j'|_A\otimes\langle\mu|_B\right)\\
  &=\sum_{iji'j'\mu}a_{i\mu}a^*_{i'\mu}U^\dagger_{ij}U_{i'j'}|j\rangle_A\ _A\langle j'|\\
  &=\sum_{iji'\mu}a_{i\mu}a^*_{i'\mu}U^\dagger_{ij}U_{i'j}|j\rangle_A\ _A\langle j|\text{ (由假设是对角)}\\
  &=\sum_j \left[\sum_{i,i'}\sum_\mu\left(a_{i\mu}a^*_{i'\mu}\right)U^\dagger_{ij}U_{i'j}\right]|j\rangle_A\ _A\langle j|\\
  &\equiv\sum_j p_j|j\rangle_A\ _A\langle j|
  \end{align}
  $$
  因此$\text{tr}_A\boldsymbol{\rho}_{A}=\sum_jp_j=\sum_{i,i'}\sum_\mu\left(a_{i\mu}a^*_{i'\mu}\right)\delta_{i,i'}=\sum_{i\mu}a_{i\mu}a^*_{i\mu}=1$，对A的基变换后$\boldsymbol{\rho}_{A}$的trace不变，还是1。

  Chap 2.4中Schmidt decomposition的第一步已经假设我们完成了上述将A对角化的过程，即A的基矢已经是其Schmidt bases$\{|j\rangle_A\}$。$\blacksquare$