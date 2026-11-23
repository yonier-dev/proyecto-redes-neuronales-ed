# Manual de Usuario — Simulador de Red Neuronal

Bienvenido al **Simulador de Red Neuronal**. Esta aplicacion de escritorio
(Tkinter) demuestra como una red neuronal pequena aprende, por descenso de
gradiente, a reproducir distintas funciones matematicas. Tu eliges la funcion y
los coeficientes objetivo; la red empieza con pesos aleatorios, entrena durante
un numero de iteraciones y muestra en una grafica los datos reales frente a su
prediccion, ademas de un registro detallado del entrenamiento.

---

## 🧭 Estructura General de la Interfaz

La ventana (900 x 600 px) se organiza en tres zonas:

1. **Grafica (izquierda):** muestra los datos reales y la prediccion de la red.
2. **Controles (arriba a la derecha):** seleccion de funcion, epochs y coeficientes.
3. **Salida (abajo a la derecha):** registro textual del entrenamiento.

---

## 1. Zona de la Grafica

### 📈 Grafica de la funcion

Muestra dos series:
- **Linea/ puntos azules:** los **datos reales**, es decir, la funcion objetivo
  generada con los coeficientes `W`, `B` y `W2` que ingresaste.
- **Linea roja:** la **prediccion de la red neuronal** despues de entrenar.

El titulo de la grafica indica la funcion seleccionada (por ejemplo
`Red Neuronal F.Cuadrática y=...`). Al pulsar **Entrenar Red Neuronal** la
grafica se actualiza con la prediccion final de la red.

Interpretacion:
- Si la linea roja se superpone a los datos azules, la red aprendio bien.
- Si no se superpone, prueba con mas epochs o revisa los coeficientes.

---

## 2. Zona de Controles

### 🎛️ Controles y parametros

- **Selecciona Tipo de Funcion a Entrenar (ComboBox):** elige la funcion que la
  red debe aprender. Las opciones son:
  `FuncionLineal`, `FuncionCuadratica`, `FuncionCubica`, `FuncionLogaritmica`,
  `FuncionExponencial`, `FuncionTrigonometrica`, `FuncionCircunferencia`,
  `FuncionRadical`, `FuncionValorAbsoluto`.
- **Veces que Quiero Entrenar La redNeuronal (campo de texto):** numero de
  iteraciones (epochs) del entrenamiento. A mas epochs, mejor ajuste
  (hasta cierto punto).
- **Ingresa valor W / B / W2:** coeficientes objetivo de la funcion.
  - Al seleccionar una funcion se habilitan solo las casillas que esa funcion
    necesita (por ejemplo, `W2` solo para cuadratica, cubica, exponencial,
    trigonometrica y circunferencia).
- **Entrenar Red Neuronal (boton):** inicia el entrenamiento con los valores
  ingresados y actualiza la grafica y el registro.

### Coeficientes por funcion

| Funcion | W | B | W2 |
|---------|---|---|----|
| Lineal | pendiente | intercepto | — |
| Cuadratica | coef. de x^2 | intercepto | coef. de x |
| Cubica | coef. de x^3 | (se usa como coef. de x^2 en la red) | coef. de x^2 objetivo |
| Logaritmica | coef. de ln(x) | intercepto | — |
| Exponencial | amplitud | intercepto | coef. del exponente |
| Trigonometrica | amplitud | desplazamiento vertical | frecuencia |
| Circunferencia | radio | centro en Y | centro en X |
| Radical | coef. de sqrt(x) | intercepto | — |
| Valor Absoluto | coef. de \|x\| | intercepto | — |

Nota: la red usa internamente los parametros `w`, `b` y, cuando aplica, `z`
para ajustar la funcion. Los valores `W`, `B`, `W2` definen la curva objetivo.

---

## 3. Zona de Salida (registro)

### 📋 Registro de entrenamiento

El panel **Salida** muestra, epoch por epoch, el progreso del aprendizaje:

```
Epoch 0: loss=1.2345, w=0.12, b=-0.34
Epoch 1: loss=0.9876, w=0.25, b=-0.20
...
```

- **loss:** error cuadratico medio (MSE) entre la prediccion y los datos reales.
  Debe tender a cero a medida que la red aprende.
- **w, b, z:** valores de los parametros de la red en esa iteracion.

Si dejas el campo de epochs vacio, la aplicacion usa valores por defecto
(30 epochs, W=1, B=0, W2=1) y muestra el registro con esos valores.

---

## 💡 Consejos de uso

1. **Mas epochs = mejor ajuste** (hasta cierto punto). Prueba con 30, 50 o 100.
2. **Funciones con W2:** recuerda habilitar e ingresar `W2` en cuadratica,
   cubica, exponencial, trigonometrica y circunferencia.
3. **Circunferencia:** ingresa radio en `W`, centro Y en `B` y centro X en `W2`.
4. **Logaritmica y radical:** los datos se generan solo para `x` validos
   (x > 0), por lo que la grafica se ve en ese rango.
5. **Resultados variables:** los pesos iniciales son aleatorios, por lo que
   cada entrenamiento puede variar ligeramente.

## ⚠️ Solucion de problemas

- Si la aplicacion no inicia, verifica que `numpy` y `matplotlib` esten
  instalados: `pip install numpy matplotlib`.
- Si aparece un error al entrenar, asegurate de ingresar **numeros enteros**
  en los campos (la aplicacion usa `int()`).
- Si seleccionas una funcion y las casillas no se habilitan, vuelve a
  seleccionarla en el ComboBox.