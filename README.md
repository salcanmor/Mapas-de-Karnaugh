# Mapas de Karnaugh y transformación de la función en mintérminos y maxtérminos

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

### Autor

Salvador Canas Moreno
