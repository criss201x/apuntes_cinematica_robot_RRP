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

## Interpretación del signo

| Resultado | Ángulo | Significado geométrico |
|-----------|--------|------------------------|
| $\mathbf{u} \cdot \mathbf{v} = 0$ | $\theta = 90°$ | Vectores **ortogonales** (perpendiculares) |
| $\mathbf{u} \cdot \mathbf{v} > 0$ | $\theta < 90°$ | Ángulo agudo — apuntan en dirección similar |
| $\mathbf{u} \cdot \mathbf{v} < 0$ | $\theta > 90°$ | Ángulo obtuso — apuntan en direcciones opuestas |

---

## Norma vectorial

La norma es la "longitud" de un vector — Pitágoras generalizado a $n$ dimensiones:

$$\|\mathbf{u}\| = \sqrt{a^2 + b^2 + c^2}$$

Para los ejes cartesianos unitarios $\hat{x} = (1,0,0)$, $\hat{y} = (0,1,0)$, $\hat{z} = (0,0,1)$:

$$\|\hat{x}\| = \|\hat{y}\| = \|\hat{z}\| = 1 \quad \text{(vectores unitarios)}$$
