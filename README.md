# Quantum-Kernels

```markdown
# 🌌 Quantum Kernels: QSVM, Feature Maps & Quantum Kernel Alignment (QKA)

Este repositório contém a formulação teórica, implementação prática e experimentos numéricos demonstrando como circuitos quânticos podem ser utilizados como funções de núcleo (**kernels**) para impulsionar algoritmos de Machine Learning Clássico através de **Quantum Support Vector Machines (QSVM)**.

Desenvolvido com o ecossistema **Qiskit 1.0+** e **Qiskit Machine Learning**, o projeto aborda desde a codificação de dados clássicos na Esfera de Bloch até a otimização de parâmetros de circuitos quânticos via alinhamento de kernel com os rótulos de dados (QKA).

---

## 📚 Sumário Teórico

### 1. O Kernel Quântico de Fidelidade
A transição do espaço clássico para o espaço de Hilbert quântico de dimensão exponencial $2^n$ é feita mapeando um dado de entrada $x$ em um estado quântico:

$$
|\phi(x)\rangle = U_\phi(x)|0\rangle^{\otimes n}
$$

A similaridade entre duas amostras $x$ e $x'$ no espaço de estados é calculada pela **Fidelidade Quântica**, que define o nosso Kernel Quântico:

$$
K_q(x, x') = |\langle\phi(x)|\phi(x')\rangle|^2
$$

### 2. O Papel do Emaranhamento ($CNOT$)
A inclusão de portas de emaranhamento como a $CNOT$ correlaciona os qubits de forma não-local. Enquanto um mapeamento local produz um estado produto puramente independente:

$$
|\phi_{\text{local}}(x)\rangle = R_Y(x_0)|0\rangle \otimes R_Z(x_1)|0\rangle
$$

A introdução da porta $CNOT$ mapeia correlações cruzadas não-lineares diretamente na amplitude geométrica de sobreposição:

$$
|\phi_{\text{entangled}}(x)\rangle = \text{CNOT} \left( R_Y(x_0)|0\rangle \otimes R_Z(x_1)|0\rangle \right)
$$

---

## 🔬 Estrutura dos Experimentos Computacionais

### 🧪 Experimento 1: Mapeamento Geométrico na Esfera de Bloch
* **Objetivo:** Visualização do mapeamento de dados em um espaço de estados quânticos de um único qubit.
* **Visualização:** Mapeamento em 3D utilizando rotações $R_Y(\theta)$ na superfície da Esfera de Bloch para analisar a distribuição geométrica das similaridades quânticas.

### 🧪 Experimento 2: QSVM vs. SVM Clássica (RBF)
* **Dataset:** Dados ad-hoc de Havlíček com 2 características.
* **Feature Map:** Codificação $ZZ$ parametrizada de 2 qubits com duas repetições (`reps=2`).
* **Resultados Obtidos:**
  * **QSVM (Kernel Quântico):** **90%** de acurácia no teste.
  * **SVM Clássico (RBF):** **70%** de acurácia no teste.

### 🧪 Experimento 3: Quantum Kernel Alignment (QKA)
* **Conceito:** Otimização dos parâmetros variacionais $\theta$ de um circuito quântico para maximizar a compatibilidade com a matriz de rótulos dos dados clássicos $T = y y^\top$.
* **Métrica (Alinhamento de Frobenius):**
  $$
  A(K_\theta, T) = \frac{\langle K_\theta, T\rangle_F}{\|K_\theta\|_F \|T\|_F}
  $$
* **Otimização:** Uso do método de otimização clássica Nelder-Mead (`scipy.optimize.minimize`) para ajustar de forma eficiente os parâmetros internos do `TrainableFidelityQuantumKernel`.

### 🧪 Exercício Prático: O impacto do Emaranhamento
* Comparação lado a lado de matrizes de kernel geradas utilizando um circuito local (sem $CNOT$) e um circuito emaranhado (com $CNOT$):

| Sem Emaranhamento (Local) | Com Emaranhamento (CNOT) |
| :---: | :---: |
| ![Local Kernel](https://github.com/user-attachments/assets/placeholder-local) | ![Entangled Kernel](https://github.com/user-attachments/assets/placeholder-entangled) |



## 🛠️ Requisitos e Configuração

Certifique-se de instalar as dependências corretas compatíveis com o **Qiskit v1.0+**:

```bash
pip install "qiskit>=1.0,<2.0" \
            "qiskit-machine-learning>=0.8,<0.9" \
            "scikit-learn>=1.4" \
            matplotlib seaborn scipy
---
## 📝 Referências

* **Qiskit Machine Learning Community**
* Havlíček, V., Córcoles, A.D., Temme, K. et al. *Supervised learning with quantum-enhanced feature spaces*. Nature 567, 209–212 (2019).
```
