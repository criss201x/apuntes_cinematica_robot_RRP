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


---

## Ejemplo resuelto

$$\mathbf{u} = \begin{pmatrix} 1 \\ 1 \\ 0 \end{pmatrix}, \quad \mathbf{v} = \begin{pmatrix} 1 \\ 0 \\ 0 \end{pmatrix}$$

**Paso 1 — Producto interno:**
$$\mathbf{u} \cdot \mathbf{v} = (1)(1) + (1)(0) + (0)(0) = 1$$

**Paso 2 — Normas:**
$$\|\mathbf{u}\| = \sqrt{1^2 + 1^2 + 0^2} = \sqrt{2} \approx 1.41$$
$$\|\mathbf{v}\| = \sqrt{1^2 + 0^2 + 0^2} = 1$$

**Paso 3 — Ángulo:**
$$\theta = \cos^{-1}\left(\frac{1}{1.41 \times 1}\right) = \cos^{-1}(0.70) \approx 45°$$

*Interpretación:* $\mathbf{v}$ apunta sobre el eje X puro; $\mathbf{u}$ apunta en diagonal entre X e Y — exactamente 45°.


---

## Caso especial: ortogonalidad de los ejes cartesianos

$$\hat{x} \cdot \hat{y} = (1)(0) + (0)(1) + (0)(0) = 0 \implies \text{ortogonales}$$

Los ejes X, Y, Z de cualquier sistema de coordenadas cartesiano son mutuamente ortogonales — su producto interno es siempre cero.

---

## Implementación en Python

```python
import numpy as np

u = np.array([1, 1, 0])
v = np.array([1, 0, 0])

producto_interno = np.dot(u, v)                        # → 1
norma_u          = np.linalg.norm(u)                   # → 1.4142
norma_v          = np.linalg.norm(v)                   # → 1
theta_grados     = np.degrees(np.arccos(np.dot(u,v) / (np.linalg.norm(u)*np.linalg.norm(v)))) # → 45°
```

> `np.degrees()` convierte radianes a **grados**. `np.arccos()` devuelve el ángulo en radianes.

---

## Relevancia en robótica

- Calcular el ángulo entre dos eslabones de un robot
- Verificar si dos ejes articulares son perpendiculares
- Proyectar fuerzas o velocidades sobre una dirección específica
- Base para la construcción de matrices de rotación (módulo 3.2)

---
# Matrices de rotación
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 3)

---

## Idea constructiva

Las columnas de una matriz de rotación son los **destinos de cada eje coordenado** después de la rotación. Si rotas 90° alrededor de Z:

- Eje X → $(0, 1, 0)$
- Eje Y → $(-1, 0, 0)$
- Eje Z → $(0, 0, 1)$ — no se mueve, es el eje de rotación

$$R_z(90°) = \begin{pmatrix} 0 & -1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

---

## Idea constructiva

Las columnas de una matriz de rotación son los **destinos de cada eje coordenado** después de la rotación. Si rotas 90° alrededor de Z:

- Eje X → $(0, 1, 0)$
- Eje Y → $(-1, 0, 0)$
- Eje Z → $(0, 0, 1)$ — no se mueve, es el eje de rotación

$$R_z(90°) = \begin{pmatrix} 0 & -1 & 0 \\ 1 & 0 & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

---

## Matrices de rotación generales

$$R_x(\theta) = \begin{pmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta & \cos\theta \end{pmatrix}$$

$$R_y(\theta) = \begin{pmatrix} \cos\theta & 0 & \sin\theta \\ 0 & 1 & 0 \\ -\sin\theta & 0 & \cos\theta \end{pmatrix}$$

$$R_z(\theta) = \begin{pmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{pmatrix}$$

**Patrón:** la fila y columna del eje de rotación tienen 1 en la diagonal y 0 en el resto.

---

## Por qué $R_y$ tiene el signo invertido

El orden cíclico dextrógiro es $X \to Y \to Z \to X$:

- $R_z$: plano $X \to Y$ — orden natural
- $R_x$: plano $Y \to Z$ — orden natural
- $R_y$: plano $Z \to X$ — orden **invertido** respecto a $X \to Z$

Mantener la regla de la mano derecha consistente obliga a voltear el signo negativo en $R_y$.

---

## Propiedades fundamentales — grupo $SO(3)$

Las matrices de rotación pertenecen al grupo especial ortogonal $SO(3)$, definido por:

### 1. Ortogonalidad

$$R \cdot R^T = I \implies R^{-1} = R^T$$

Invertir una rotación es simplemente **transponerla** — geométricamente es el viaje de regreso. Computacionalmente muy eficiente.

### 2. Determinante unitario

$$\det(R) = +1$$

Derivación: de $R \cdot R^T = I$ se sigue $\det(R)^2 = 1$, por tanto $\det(R) = \pm 1$. El $+1$ distingue rotaciones puras de reflexiones — en robótica siempre $+1$.

---
