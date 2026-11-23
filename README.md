# Simulador de Red Neuronal

Aplicacion de escritorio (Tkinter) que muestra como una red neuronal pequena
**aprende por descenso de gradiente** a ajustar distintas funciones matematicas.
El usuario elige el tipo de funcion y los coeficientes objetivo; la red comienza
con pesos aleatorios, entrena durante un numero de iteraciones (epochs) y grafica
los datos reales frente a la prediccion de la red, junto con el error (loss) y
los parametros aprendidos en cada iteracion.

## Caracteristicas

- 9 tipos de funcion a aprender:
  Lineal, Cuadratica, Cubica, Logaritmica, Exponencial, Trigonometrica (seno),
  Circunferencia, Radical (raiz cuadrada) y Valor Absoluto.
- Interfaz grafica con Tkinter: grafica, controles y registro de entrenamiento.
- Coeficientes objetivo configurables (`W`, `B` y `W2` segun la funcion).
- Numero de iteraciones (epochs) configurable.
- Descenso de gradiente con gradientes analiticos y funcion de perdida MSE.
- Grafica con datos reales (puntos/linea azul) y prediccion de la red (linea roja).
- Registro por epoch del error y de los pesos aprendidos.

## Requisitos

- Python 3.8+
- `numpy`
- `matplotlib`
- `tkinter` (incluido con Python en la mayoria de instalaciones)
- En Linux, si la ventana no abre por falta de fuentes, instala un paquete de
  fuentes (por ejemplo `ttf-dejavu` en Arch o `fonts-dejavu` en Debian/Ubuntu).

## Instalacion

```bash
git clone https://github.com/yonier-dev/proyecto-redes-neuronales-ed.git
cd proyecto-redes-neuronales-ed/project
pip install numpy matplotlib
```

## Uso

```bash
# Ejecutar la aplicacion (desde la carpeta project/)
python main.py
```

En Linux/macOS puede ser necesario usar `python3`:

```bash
python3 main.py
```

## Como usar la aplicacion

1. Ejecuta `python main.py`.
2. En **Selecciona Tipo de Funcion a Entrenar** elige la funcion que quieres que la red aprenda.
3. Escribe en **Veces que Quiero Entrenar La redNeuronal** el numero de iteraciones (epochs).
4. Ingresa los coeficientes objetivo en **W**, **B** y, si la funcion lo requiere, **W2**.
   (Al seleccionar una funcion se habilitan/deshabilitan las casillas correspondientes.)
5. Pulsa **Entrenar Red Neuronal**.
6. Observa la grafica (datos reales vs prediccion) y el panel **Salida** con el
   detalle epoch por epoch.

Si dejas el campo de epochs vacio, la aplicacion usa valores por defecto
(30 epochs, W=1, B=0, W2=1).

## Funciones disponibles

| Funcion (combo) | Datos reales (objetivo) | Parametros de la red |
|-----------------|--------------------------|----------------------|
| FuncionLineal | `y = W*x + B` | `w, b` |
| FuncionCuadratica | `y = W*x^2 + W2*x + B` | `w, b, z` |
| FuncionCubica | `y = W*x^3 + W2*x^2 + B*x` | `w, b, z` |
| FuncionLogaritmica | `y = W*ln(x) + B` | `w, b` |
| FuncionExponencial | `y = W*e^(W2*x) + B` | `w, b, z` |
| FuncionTrigonometrica | `y = W*sin(W2*x) + B` | `w, b, z` |
| FuncionCircunferencia | `(x-W2)^2 + (y-B)^2 = W^2` | `cx=z, cy=b, r=w` |
| FuncionRadical | `y = W*sqrt(x) + B` | `w, b` |
| FuncionValorAbsoluto | `y = W*abs(x) + B` | `w, b` |

Notas por funcion:
- **FuncionCircunferencia**: `W` es el radio, `B` el centro en Y y `W2` el centro en X.
- **FuncionLogaritmica**: los datos se generan con `x` en `[0.1, 2]`.
- **FuncionRadical**: los datos se generan con `x >= 0`.

## Estructura del proyecto

```
project/
  main.py                      Punto de entrada de la aplicacion
  guiGraphic/
    interfaz.py                Interfaz Tkinter (ventana, controles, eventos)
    graphics.py                Creacion y actualizacion de la grafica
  logic/
    LinealEquation.py          Red para funcion lineal
    SquareEquation.py          Red para funcion cuadratica
    CubicEquation.py           Red para funcion cubica
    LogarithmicEquation.py     Red para funcion logaritmica
    ExponentialEquation.py     Red para funcion exponencial
    TrigonometricEquation.py   Red para funcion trigonometrica (seno)
    CircleEquation.py          Red para circunferencia
    RadicalEquation.py         Red para funcion radical
    AbsoluteEquation.py        Red para valor absoluto
    main.py                    Demo por consola de la red cuadratica
```

Cada clase en `logic/` implementa el mismo esquema:
- `forward()`: prediccion de la red.
- `loss()`: error cuadratico medio (MSE).
- `backward()`: gradientes analiticos.
- `actualizar()`: actualizacion de pesos por descenso de gradiente.
- `prueba(n_epoch)`: bucle de entrenamiento y registro de detalles.
- `getTextDetails()`: texto con el historial de entrenamiento.

## Detalles tecnicos

- La red es un modelo pequeno con parametros `w`, `b` (y `z` cuando aplica),
  inicializados de forma aleatoria con `numpy.random.randn()`.
- El entrenamiento minimiza el MSE entre la prediccion y los datos objetivo.
- Tasa de aprendizaje (learning rate): `0.1` en la mayoria de funciones,
  `0.05` en exponencial y trigonometrica, `0.01` en circunferencia.
- La interfaz no requiere conexion a internet ni servicios externos.

## Autores

Proyecto de Ecuaciones Diferenciales - Universidad