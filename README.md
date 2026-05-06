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


