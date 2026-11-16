# Regresión Lineal por Mínimos Cuadrados en Java

Implementación del método de **Regresión Lineal Simple** mediante **Mínimos Cuadrados**, incluyendo el **coeficiente de correlación de Pearson (r)** y el **coeficiente de determinación (r²)**. Con los datos de entrada se obtiene el modelo `Y = β0 + β1·X` y se pueden hacer predicciones de Y a partir de un valor de X.

**Autor:** Marco Antonio Pavia Flores.
**Materia:** SCC-1017 Métodos Numéricos — Unidad 5
**Docente:** Víctor Hugo Vásquez Herrera
**Institución:** Instituto Tecnológico Superior de Xalapa

## Lenguaje de programación

**Java** (JDK 8 o superior; se recomienda JDK 17 o superior).

## Estructura del proyecto

```text
RegresionLineal/
├── src/
│   └── RegresionLineal.java
├── .gitattributes
└── README.md
```

| Archivo | Descripción |
|---|---|
| `RegresionLineal.java` | Contiene `calcularMinimosCuadrados` (β0, β1, r, r²), `predecir` y el método `main` con los datos de prueba. |

El código declara el paquete `Ajuste_de_Funciones` (`package Ajuste_de_Funciones;`), por lo que la clase completa se ejecuta como `Ajuste_de_Funciones.RegresionLineal`.

## Fundamento matemático

Con `n` datos y las sumatorias ΣX, ΣY, ΣX², ΣY² y ΣXY:

```text
β1 = (n·ΣXY − ΣX·ΣY) / (n·ΣX² − (ΣX)²)
β0 = (ΣY − β1·ΣX) / n
r  = (n·ΣXY − ΣX·ΣY) / √[ (n·ΣX² − (ΣX)²) · (n·ΣY² − (ΣY)²) ]
r² = r · r
```

Las líneas implementadas en `RegresionLineal.java` son las que calculan Pearson y el coeficiente de determinación:

```java
double numerador = n * sumXY - sumX * sumY;
double denominador = Math.sqrt((n * sumX2 - sumX * sumX) * (n * sumY2 - sumY * sumY));
double pearsonR = numerador / denominador;
double r2 = pearsonR * pearsonR;
```

## Validaciones

`calcularMinimosCuadrados()` muestra un mensaje de error y devuelve `{0, 0, 0, 0}` si:

- Los arreglos `x` y `y` tienen distinto tamaño.
- Los arreglos están vacíos.
- Todos los valores de `X` son iguales (el denominador de β1 sería cero).

Si `Y` es constante, el denominador de Pearson es cero y el programa asigna `r = 0` para evitar una división entre cero.

## Datos de prueba

Definidos directamente en el método `main`:

```java
double[] x = {1, 2, 3, 4, 5};
double[] y = {2, 4, 5, 4, 5};
```

| X | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| Y | 2 | 4 | 5 | 4 | 5 |

- Valor a predecir: **X = 6** (`nuevoX` en `main`)

## Cómo clonar, compilar y ejecutar

### Desde la terminal

1. Clona el repositorio y entra a la carpeta:
   ```bash
   git clone https://github.com/Marco-Pavia/RegresionLineal-PorMinimosCuadrados.git
   cd RegresionLineal-PorMinimosCuadrados
   ```
2. Compila desde la carpeta raíz:
   ```bash
   javac -d out src/RegresionLineal.java
   ```

### Desde IntelliJ IDEA

1. Abre la carpeta del proyecto con *File → Open*.
2. Verifica que `RegresionLineal.java` esté dentro de la carpeta `src`.
3. Abre el archivo y presiona el botón verde ▶ junto al método `main`.

## Ejemplo de ejecución

```text
--- RESULTADOS DE MINIMOS CUADRADOS Y CORRELACION ---
Sumatorias: n= 5, X= 15.0, Y= 20.0, X2= 55.0, Y2= 86.0, XY= 66.0
Pendiente (beta1): 0.6000
Ordenada al origen (beta0): 2.2000
Modelo obtenido: Y = 2.2000 + 0.6000X
Coeficiente de Pearson (r): 0.7746
Coeficiente de Determinacion (r2): 0.6000

--- PREDICCION ---
Valor de X: 6.00
Valor estimado de Y: 5.8000
```

## Resultados esperados

| Indicador | Valor |
|---|---|
| Pendiente (β1) | 0.6000 |
| Ordenada al origen (β0) | 2.2000 |
| Modelo | Y = 2.2000 + 0.6000X |
| Pearson (r) | 0.7746 |
| Determinación (r²) | 0.6000 |
| Predicción para X = 6 | 5.8000 |
