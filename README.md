# 3.1 — Producto interno y normas vectoriales
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 3)

---
## Definición algebraica

Dados dos vectores en $\mathbb{R}^n$:

$$\mathbf{u} = \begin{pmatrix} a \\ b \\ \vdots \end{pmatrix}, \quad \mathbf{v} = \begin{pmatrix} c \\ d \\ \vdots \end{pmatrix}$$

El producto interno se define como:

$$\mathbf{u} \cdot \mathbf{v} = ac + bd + \cdots = \sum_{i=1}^{n} u_i v_i$$

**Resultado:** siempre un escalar real — no un vector.

---

## Definición geométrica

$$\mathbf{u} \cdot \mathbf{v} = \|\mathbf{u}\| \|\mathbf{v}\| \cos\theta$$

donde $\theta$ es el ángulo entre los dos vectores.

De aquí se puede despejar el ángulo:

$$\theta = \cos^{-1}\left(\frac{\mathbf{u} \cdot \mathbf{v}}{\|\mathbf{u}\| \|\mathbf{v}\|}\right)$$

---
