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

## Regla de la mano derecha

Para determinar el sentido positivo de rotación alrededor de un eje: apuntar el pulgar derecho en la dirección positiva del eje — los dedos indican el sentido positivo de rotación.

Ejemplo: $R_x(90°)$ sobre $\mathbf{v} = (0,1,0)$: el pulgar apunta en $+X$, los dedos van de $Y$ hacia $Z$, entonces el vector termina en $(0, 0, 1)$.

---

## Resumen de propiedades

| Propiedad | Expresión |
|-----------|-----------|
| Inversa = transpuesta | $R^{-1} = R^T$ |
| Determinante | $\det(R) = +1$ |
| Columnas ortonormales | cada columna es unitaria y ortogonal a las demás |
| Conserva longitudes | $\|R\mathbf{v}\| = \|\mathbf{v}\|$ |

---
# Módulo 3.3 — Reglas de rotación compuesta
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 3)

---

## Principio fundamental

La multiplicación de matrices de rotación **no es conmutativa**:

$$R_z \cdot R_x \neq R_x \cdot R_z$$

El orden en que se aplican las rotaciones define completamente la postura final. Este es uno de los conceptos más críticos de la cinemática de robots.

---

## Composición de rotaciones

La rotación total de $n$ rotaciones aplicadas en secuencia es el producto matricial en orden de aplicación — **de derecha a izquierda**:

$$R_{total} = R_n \cdots R_2 \cdot R_1$$

$R_1$ se aplica primero, $R_n$ al final.

---

## Dos interpretaciones según el marco de referencia

| Interpretación | Marco | Orden de multiplicación |
|---|---|---|
| Ejes **fijos** (globales) | El marco no cambia | Pre-multiplicar: $R_{nuevo} = R_i \cdot R_{actual}$ |
| Ejes **locales** (del cuerpo) | El marco gira con el cuerpo | Post-multiplicar: $R_{nuevo} = R_{actual} \cdot R_i$ |

---
## Cadena cinemática

Para un robot con articulaciones $R_1, R_2, R_3$ sobre **ejes locales**:

$$R_{total} = R_1 \cdot R_2 \cdot R_3$$

Lectura: $R_1$ se aplica primero. El eje de $R_2$ ya no es el eje global — es el eje que quedó después de que $R_1$ transformó el sistema. Cada articulación hereda el marco de la anterior.

> En la convención D-H siempre se trabaja con ejes locales.

---

## Por qué el orden importa — intuición

Rota un libro 90° sobre Z (lo giras en la mesa) y luego 90° sobre X (lo inclinas hacia ti). Invierte el orden: primero 90° sobre X, luego 90° sobre Z. El resultado final es diferente — la orientación del libro no es la misma en ambos casos.


# Módulos 3.4 y 3.5 — Traslación y transformaciones homogéneas
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 3)

---
## 3.4 — El problema de la traslación

Una matriz de rotación $R$ de $3\times3$ solo puede rotar. Para describir la posición completa de un eslabón respecto a otro se necesita también trasladar:

$$\mathbf{p}_1 = R \cdot \mathbf{p}_2 + \mathbf{d}$$

donde $\mathbf{d} = (p_x, p_y, p_z)^T$ es el vector de traslación entre orígenes.

**Problema:** esta operación mezcla multiplicación matricial con suma vectorial. No se pueden encadenar varias transformaciones como un producto simple — se rompe la posibilidad de tratar cada eslabón como un solo bloque matemático.


---

## 3.5 — Transformación homogénea

### El truco algebraico

Se extiende el espacio de 3D a 4D agregando una coordenada artificial igual a 1:

$$\mathbf{p} = \begin{pmatrix} x \\ y \\ z \end{pmatrix} \longrightarrow \tilde{\mathbf{p}} = \begin{pmatrix} x \\ y \\ z \\ 1 \end{pmatrix}$$

Con esto, la operación $R\mathbf{p} + \mathbf{d}$ se convierte en una **sola multiplicación matricial**:

$$\begin{pmatrix} \mathbf{p}_1 \\ 1 \end{pmatrix} = \underbrace{\begin{pmatrix} R & \mathbf{d} \\ \mathbf{0}^T & 1 \end{pmatrix}}_{T \ (4\times4)} \begin{pmatrix} \mathbf{p}_2 \\ 1 \end{pmatrix}$$

### Estructura de la matriz $T$

$$T = \begin{pmatrix} r_{11} & r_{12} & r_{13} & d_x \\ r_{21} & r_{22} & r_{23} & d_y \\ r_{31} & r_{32} & r_{33} & d_z \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

| Bloque | Dimensión | Contenido |
|---|---|---|
| $R$ | $3\times3$ superior izquierda | Rotación pura |
| $\mathbf{d}$ | $3\times1$ superior derecha | Traslación |
| $\mathbf{0}^T$ | $1\times3$ inferior izquierda | Siempre ceros |
| $1$ | escalar inferior derecha | Siempre 1 |

### Por qué funciona para encadenar

La fila $(\mathbf{0}^T \quad 1)$ garantiza que el producto de dos matrices homogéneas produce otra matriz homogénea con la misma estructura. La cadena se cierra sobre sí misma:

$$T_{02} = T_{01} \cdot T_{12}$$

Generalizado para una cadena de $n$ eslabones:

$$T_{0n} = T_{01} \cdot T_{12} \cdots T_{n-1,n}$$

Esta es la expresión central de la **cinemática directa**.

### Inversa de una transformación homogénea

$$T^{-1} = \begin{pmatrix} R^T & -R^T\mathbf{d} \\ \mathbf{0}^T & 1 \end{pmatrix}$$

Se aprovecha que $R^{-1} = R^T$ — no se necesita invertir la matriz completa.

---

## Conexión con lo anterior

| Módulo | Aporte a $T$ |
|---|---|
| 3.1 Producto interno | Define ortogonalidad — propiedad de las columnas de $R$ |
| 3.2 Matrices de rotación | El bloque $R$ de $3\times3$ |
| 3.3 Rotación compuesta | El orden del producto $T_{01} \cdot T_{12} \cdots$ |
| 3.4 Traslación | El vector $\mathbf{d}$ y la motivación de la matriz $4\times4$ |
| **3.5 Homogénea** | **Unifica todo en una sola operación matricial** |

---
# Módulos 4.1 y 4.2 — Clasificación de robots y convención Denavit-Hartenberg
> **Fuente:** MATLAB Aplicado a Robótica y Mecatrónica — Fernando Reyes Cortés (Cap. 4)

---

## 4.1 — Clasificación de robots industriales

### Tipos de articulaciones

| Símbolo | Tipo | Movimiento | Variable |
|---|---|---|---|
| R | Rotacional | Giro alrededor de un eje | $\theta_i$ |
| P | Prismática | Traslación a lo largo de un eje | $d_i$ |

### Grados de libertad (GDL)
Número de articulaciones = número de variables independientes = dimensión del espacio de juntas.

### Configuraciones canónicas

| Configuración | Notación | Espacio de trabajo |
|---|---|---|
| Cartesiana | PPP | Cúbico |
| Cilíndrica | RPP | Cilíndrico |
| Esférica | RRP | Esférico |
| SCARA | RRP | Cilíndrico acotado |
| Antropomórfica | RRR | Irregular (mayor alcance) |

---

## 4.2 — Convención Denavit-Hartenberg (D-H)

### El problema que resuelve
Dado un robot con $n$ articulaciones, D-H define un método sistemático para asignar marcos de referencia y construir cada matriz $T_{i-1,i}$ con exactamente **4 parámetros**.

### Los 4 parámetros D-H

| Parámetro | Símbolo | Qué describe |
|---|---|---|
| Longitud del eslabón | $a_i$ | Distancia entre ejes $z_{i-1}$ y $z_i$ a lo largo de $x_i$ |
| Desplazamiento | $d_i$ | Distancia a lo largo de $z_{i-1}$ hasta el origen del marco $i$ |
| Ángulo de torsión | $\alpha_i$ | Ángulo entre $z_{i-1}$ y $z_i$ alrededor de $x_i$ |
| Ángulo de articulación | $\theta_i$ | Ángulo de rotación alrededor de $z_{i-1}$ |

**Regla clave:**
- Articulación **R** → $\theta_i$ es la variable, $d_i$ constante
- Articulación **P** → $d_i$ es la variable, $\theta_i$ constante

### Matriz D-H general

$$T_{i-1,i} = \begin{pmatrix} \cos\theta_i & -\sin\theta_i\cos\alpha_i & \sin\theta_i\sin\alpha_i & a_i\cos\theta_i \\ \sin\theta_i & \cos\theta_i\cos\alpha_i & -\cos\theta_i\sin\alpha_i & a_i\sin\theta_i \\ 0 & \sin\alpha_i & \cos\alpha_i & d_i \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

- Bloque $3\times3$ superior izquierdo → rotación compuesta ($\theta_i$ y $\alpha_i$)
- Columna superior derecha → traslación ($a_i$ y $d_i$)

---

## Aplicación al robot esférico (RRP)

### Tabla D-H

| Eslabón | $a_i$ | $d_i$ | $\alpha_i$ | $\theta_i$ | Variable |
|---|---|---|---|---|---|
| 1 (R) | $0$ | $d_1$ | $90°$ | $\theta_1$ | $\theta_1$ |
| 2 (R) | $0$ | $0$ | $-90°$ | $\theta_2$ | $\theta_2$ |
| 3 (P) | $0$ | $d_3$ | $0°$ | $0$ | $d_3$ |

### Por qué $a_i = 0$ en todos los eslabones
Los ejes de las tres articulaciones se **intersectan en un punto común** — por eso no hay distancia entre ejes. Esta es la condición geométrica que genera el espacio de trabajo esférico.

### Por qué $\alpha_1 = 90°$
Sin la torsión de 90°, J1 y J2 girarían alrededor del mismo eje — se desperdiciaría un grado de libertad. El $\alpha_1 = 90°$ hace que J2 controle la elevación del brazo mientras J1 controla el giro horizontal.


### Matrices individuales

$$T_{01} = \begin{pmatrix} \cos\theta_1 & 0 & \sin\theta_1 & 0 \\ \sin\theta_1 & 0 & -\cos\theta_1 & 0 \\ 0 & 1 & 0 & d_1 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

$$T_{12} = \begin{pmatrix} \cos\theta_2 & 0 & -\sin\theta_2 & 0 \\ \sin\theta_2 & 0 & \cos\theta_2 & 0 \\ 0 & -1 & 0 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

$$T_{23} = \begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & d_3 \\ 0 & 0 & 0 & 1 \end{pmatrix}$$

$T_{23}$ tiene el bloque de rotación igual a la identidad — la articulación prismática no rota, solo traslada a lo largo de $z_2$.

### Cinemática directa
$$T_{03} = T_{01}(\theta_1) \cdot T_{12}(\theta_2) \cdot T_{23}(d_3)$$

---
## Objetivo

Obtener una sola matriz $T_{03}$ que exprese la posición y orientación del efector en función de las tres variables articulares $\theta_1$, $\theta_2$ y $d_3$.

$$T_{03} = T_{01}(\theta_1) \cdot T_{12}(\theta_2) \cdot T_{23}(d_3)$$










