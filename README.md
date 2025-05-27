# Mapas de Karnaugh y transformación de la función en mintérminos y maxtérminos

[![DOI](https://zenodo.org/badge/991594273.svg)](https://doi.org/10.5281/zenodo.15530853)

Se presenta un programa para simplificar expresiones de álgebra booleana mediante mapas de Karnaugh. +Info en [Mapa de Karnaugh (Wikipedia)](https://en.wikipedia.org/wiki/Karnaugh_map).

## Introducción

Básicamente, el archivo `Kmap.py` contiene una función que puede simplificar expresiones de álgebra booleana según la tabla de verdad. Sin embargo, introducir la tabla de verdad completa es innecesario y puede resultar engorroso, especialmente cuando hay muchas combinaciones. Por eso la función `simplify` toma únicamente los mintérminos y los términos “don't care” como entrada.

## Algoritmo

Hay tres variables principales para esta función:

- `minterms`: utilizado para almacenar términos como `'1001'` y `'10**'`.  
- `source`: utilizado para llevar un registro de dónde proviene cada término. Por ejemplo, el término `'1001'` proviene de sí mismo, por lo que su “origen” es únicamente su índice en `minterms` (`[1]`). En cambio, para `'10**'`, se genera a partir de los términos `['1000', '1001', '1010', '1011']`, de modo que su origen es `[1, 2, 3, 4]`.  
- `flag`: utilizado para comprobar si un término ya ha sido usado para generar uno nuevo.

La función se divide en dos etapas:

1. **Simplificación**: se comprimen todos los términos hasta que ya no se pueda simplificar ninguno más. La salida de ejemplo en este paso es:
   ```python
   ['10**', '1*0*', '1**0', '*110']
   ```
   que equivale a la expresión booleana `AB' + AC' + AD' + BCD'`.

2. **Selección final**: se revisa el `source` de cada término. Si el origen de un término no incluye al menos una fuente única, o bien todas sus fuentes corresponden a términos “don't care”, ese término se considera innecesario y se elimina. El resultado que queda tras este filtrado es la forma mínima definitiva.

## Ejemplo

En la página de la wiki (enlazada más arriba) aparece una tabla de verdad que puede representarse como:

- `f(A,B,C,D) = Σ(6,8,9,10,11,12,13,14)`  
- `f(A,B,C,D) = A'BCD' + AB'C'D' + AB'C'D + AB'CD' + AB'CD + ABC'D' + ABC'D + ABCD'`  
  (donde A' significa ¬A)

Para reproducirlo en el código, asigna:

```python
minterms = ['0110', '1000', '1001', '1010', '1011', '1100', '1101', '1110']
```

Luego ejecuta en tu terminal:

```bash
python3 Kmap.py
```

Verás la salida:

```python
['10**', '1*0*', '*110']
```

(el asterisco `*` indica que la variable en esa posición ha sido simplificada). Esta salida equivale a `AB' + AC' + BCD'`, que coincide con el resultado de la wiki.

Para incluir condiciones “don't care”, basta con añadir esos términos en la lista `not_care` y ejecutar de nuevo el código.


### Autor

Salvador Canas Moreno
