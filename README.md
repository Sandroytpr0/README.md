# SistemaRutaCampus

## Curso
Algoritmo y Estructura de Datos Basados en Inteligencia Artificial

## Docente
Wilder Julio Espinoza Bravo

## Integrantes del equipo
- Sandro Callañaupa Portal
- [Nombre 2]
- [Nombre 3]
- [Nombre 4]
  
## Descripción del problema

SistemaRutaCampus es una solución integradora que gestiona lugares, rutas y niveles
de aforo dentro de un campus universitario, con el fin de apoyar la toma de decisiones
sobre ocupación, conectividad y recomendación de rutas.

El sistema combina estructuras de datos lineales estáticas y dinámicas, estructuras
LIFO/FIFO, recursividad, grafos y un árbol de decisión para resolver el problema de
forma articulada.

## Estructuras de datos utilizadas

| Estructura | Dónde se usa | Justificación |
|---|---|---|
| Vector (`Lugar[]`) | Gestión de lugares y su aforo actual | Cantidad fija de lugares conocida de antemano; acceso directo por índice |
| Matriz (`int[][]`) | Matriz de adyacencia de distancias entre lugares | Representa relaciones fijas entre todos los pares de lugares |
| Lista enlazada | [completar con el módulo de tu compañero] | [completar] |
| Pila | [completar] | [completar] |
| Cola | [completar] | [completar] |
| Recursividad | Búsqueda recursiva de lugares + Merge Sort | Permite recorrer y ordenar sin ciclos tradicionales |
| Grafo | [completar] | [completar] |
| Árbol / decisión | [completar] | [completar] |

## Detalle técnico: Estructuras lineales estáticas (Vector y Matriz)

### Vector de lugares — `procesarVectorLugares`

Se utiliza un vector `Lugar[]` para almacenar los espacios del campus (biblioteca,
cafetería, auditorio, laboratorio, etc.) junto con su aforo actual.

- **Algoritmo aplicado:** Ordenamiento por Selección (Selection Sort), complejidad O(n²).
- **Proceso:** ordena los lugares de menor a mayor aforo, y luego recorre el vector
  contando cuántos lugares superan el límite de alerta (100 personas), generando un
  consolidado de zonas con aforo crítico.

### Matriz de conectividad — `analizarMatrizConectividad`

Se utiliza una matriz de adyacencia `int[][]` de 4x4, donde cada celda representa
la distancia en metros entre dos lugares del campus.

- **Proceso:** recorre la matriz completa con un doble ciclo `for`, cuenta el total
  de conexiones directas (celdas mayores a 0) y calcula la distancia promedio entre
  los tramos del campus.

## Detalle técnico: Recursividad

### Búsqueda recursiva de lugares

Permite encontrar un lugar específico comparando su nombre con cada elemento del
arreglo, mediante llamadas sucesivas al mismo método en lugar de un ciclo tradicional.

- **Caso base:** (1) el nombre buscado coincide con un lugar del arreglo, o
  (2) se llega al final del arreglo sin encontrar coincidencias.
- **Llamada recursiva:** ocurre cuando el lugar actual no coincide con el buscado;
  el método se llama de nuevo avanzando a la siguiente posición.

### Merge Sort (ordenamiento recursivo)

Organiza los lugares del campus según su distancia, de menor a mayor.

- **Funcionamiento:** divide el arreglo en dos mitades, ordena cada mitad de forma
  recursiva y luego combina ambas partes ya ordenadas.
- **Caso base:** cuando la parte del arreglo tiene un solo elemento o está vacía.
- **Llamada recursiva:** cuando el algoritmo divide el arreglo en dos y vuelve a
  ejecutar Merge Sort sobre cada mitad.

## Estructura del repositorio














