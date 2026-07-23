 SistemaRutaCampus

 Curso
Algoritmo y Estructura de Datos Basados en Inteligencia Artificial

 Docente
Wilder Julio Espinoza Bravo


 Integrantes del equipo
- Sandro Callañaupa Portal
- Favian Andre Hurtado Carlos
- Claudio Saldaña Isaac Arturo
- Alvaro Daniel Pino Chavez
  
 Descripción del problema

SistemaRutaCampus es una solución integradora que gestiona lugares, rutas y niveles
de aforo dentro de un campus universitario, con el fin de apoyar la toma de decisiones
sobre ocupación, conectividad y recomendación de rutas.

El sistema combina estructuras de datos lineales estáticas y dinámicas, estructuras
LIFO/FIFO, recursividad, grafos y un árbol de decisión para resolver el problema de
forma articulada.

 Estructuras de datos utilizadas

| Estructura | Dónde se usa | Justificación |
|---|---|---|
| Vector (`Lugar[]`) | Gestión de lugares y su aforo actual | Cantidad fija de lugares conocida de antemano; acceso directo por índice |
| Matriz (`int[][]`) | Matriz de adyacencia de distancias entre lugares | Representa relaciones fijas entre todos los pares de lugares |
| Lista enlazada | Módulo de Reporte de Incidencias en tiempo real (caminos bloqueados) | El flujo de alertas por mantenimiento o eventos es totalmente dinámico e impredecible; permite inserciones y eliminaciones eficientes en $O(1)$ |
| Pila | Historial de navegación y rastreo del usuario (*Botón Atrás*) | Sigue una política LIFO (*Last In, First Out*), ideal para almacenar los IDs de los nodos visitados y regresar al paso anterior |
| Cola | Sistema de tickets y atención en ventanillas de la Biblioteca | Sigue una política FIFO (*First In, First Out*), garantizando atender a los estudiantes estrictamente en su orden de llegada |
| Recursividad | Búsqueda recursiva de lugares + Merge Sort | Permite recorrer y ordenar sin ciclos tradicionales |
| Grafo | Mapeo vial del campus y cálculo de rutas óptimas (BFS / Dijkstra) | Es la estructura no lineal natural para modelar redes de transporte, donde los vértices son los lugares físicos y las aristas son las calles interconectadas |
| Árbol / decisión | Motor de IA básica para la recomendación de rutas y transporte | Estructura jerárquica basada en reglas lógicas condicionales que evalúa variables (clima, aforo, distancia) para emitir la mejor decisión de movilidad |

 Detalle técnico: Estructuras lineales estáticas (Vector y Matriz)

 Vector de lugares — `procesarVectorLugares`

Se utiliza un vector `Lugar[]` para almacenar los espacios del campus (biblioteca,
cafetería, auditorio, laboratorio, etc.) junto con su aforo actual.

- Algoritmo aplicado: Ordenamiento por Selección (Selection Sort), complejidad O(n²).
- Proceso: ordena los lugares de menor a mayor aforo, y luego recorre el vector
  contando cuántos lugares superan el límite de alerta (100 personas), generando un
  consolidado de zonas con aforo crítico.

 Matriz de conectividad — `analizarMatrizConectividad`

Se utiliza una matriz de adyacencia `int[][]` de 4x4, donde cada celda representa
la distancia en metros entre dos lugares del campus.

- **Proceso:** recorre la matriz completa con un doble ciclo `for`, cuenta el total
  de conexiones directas (celdas mayores a 0) y calcula la distancia promedio entre
  los tramos del campus.

Detalle Técnico - Implementación de Estructuras de Datos

## Actividad 3 - Lista Enlazada Simple

### Objetivo

Gestionar dinámicamente los reportes de aforo enviados por los usuarios del sistema, permitiendo agregar, buscar, eliminar y recorrer los reportes sin necesidad de definir un tamaño fijo de almacenamiento.

---

## Estructura implementada

Se implementó una **Lista Enlazada Simple**, compuesta por dos clases principales:

- **Reporte:** almacena la información del reporte.
- **Nodo:** almacena un objeto `Reporte` y una referencia al siguiente nodo.

### Diagrama

```text
                 ListaReportes
                      │
                      ▼
                 ┌─────────┐
                 │ inicio  │
                 └────┬────┘
                      │
                      ▼
        ┌────────────────────────────┐
        │ Reporte: Biblioteca - Alta │
        │ siguiente -----------------┼──────────┐
        └────────────────────────────┘          │
                                                ▼
                             ┌──────────────────────────────┐
                             │ Reporte: Laboratorio - Media │
                             │ siguiente -------------------┼─────────┐
                             └──────────────────────────────┘         │
                                                                      ▼
                                              ┌────────────────────────────┐
                                              │ Reporte: Cafetería - Baja  │
                                              │ siguiente = null           │
                                              └────────────────────────────┘
```

---

## Clases implementadas

### Reporte

Representa un reporte de aforo enviado por un usuario.

#### Atributos

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| lugar | String | Nombre del lugar reportado |
| aforo | String | Estado del aforo |

---

### Nodo

Representa un nodo de la lista enlazada.

#### Atributos

| Atributo | Tipo |
|----------|------|
| reporte | Reporte |
| siguiente | Nodo |

Cada nodo mantiene una referencia únicamente al siguiente nodo de la lista.

---

### ListaReportes

Administra toda la lista enlazada.

#### Atributo

| Atributo | Tipo |
|----------|------|
| inicio | Nodo |

El atributo **inicio** apunta al primer nodo de la lista.

---

# Operaciones implementadas

## Inserción

### Método

```java
insertar(Reporte reporte)
```

### Funcionamiento

1. Se crea un nuevo nodo.
2. Si la lista está vacía, el nodo pasa a ser el inicio.
3. Si existen elementos, se recorre la lista hasta el último nodo.
4. El nuevo nodo se enlaza al final.

### Complejidad

```
O(n)
```

---

## Búsqueda

### Método

```java
buscar(String lugar)
```

### Funcionamiento

1. Se inicia desde el nodo inicial.
2. Se compara el nombre del lugar.
3. Si coincide, retorna el reporte.
4. Si llega a `null`, significa que no existe.

### Complejidad

```
O(n)
```

---

## Eliminación

### Método

```java
eliminar(String lugar)
```

### Funcionamiento

1. Se verifica si el nodo a eliminar es el primero.
2. Si no lo es, se recorre la lista.
3. Se modifica la referencia del nodo anterior para omitir el nodo eliminado.

### Complejidad

```
O(n)
```

---

## Recorrido

### Método

```java
mostrar()
```

### Funcionamiento

Recorre todos los nodos desde el inicio hasta llegar a `null`, mostrando la información almacenada.

### Complejidad

```
O(n)
```

---

# Justificación técnica

Se eligió una **Lista Enlazada Simple** debido a que:

- La cantidad de reportes no puede determinarse previamente.
- Permite almacenar información de manera dinámica.
- No requiere redimensionar memoria como ocurre con los arreglos.
- Cada nodo mantiene únicamente una referencia al siguiente nodo, reduciendo el consumo de memoria frente a una lista doble cuando no se necesita recorrer hacia atrás.

---

# Actividad 4 - Pila (Stack)

## Objetivo

Registrar el historial de rutas consultadas por el usuario.

---

## Implementación

Se utilizó la clase:

```java
Stack<String>
```

---

## Funcionamiento

Cada vez que el usuario consulta una nueva ruta, esta se almacena en la pila.

```text
Top
│
├── Cafetería
├── Laboratorio
└── Biblioteca
```

Cuando el usuario selecciona la opción **Volver**, el sistema elimina y devuelve el elemento ubicado en la cima.

---

## Operaciones utilizadas

### Push

```java
push(ruta)
```

Inserta una nueva ruta en la cima de la pila.

Complejidad

```
O(1)
```

---

### Pop

```java
pop()
```

Elimina y retorna la última ruta registrada.

Complejidad

```
O(1)
```

---

## Justificación técnica

Se eligió una pila porque implementa el comportamiento **LIFO (Last In, First Out)**.

Esto coincide con la funcionalidad del historial, donde la última ruta consultada debe ser la primera en recuperarse.

---

# Actividad 4 - Cola (Queue)

## Objetivo

Procesar los reportes de aforo respetando el orden en que fueron enviados por los usuarios.

---

## Implementación

Se utilizó la interfaz

```java
Queue<String>
```

con la implementación

```java
LinkedList<String>
```

---

## Funcionamiento

Cada reporte recibido ingresa al final de la cola.

```text
Entrada

Biblioteca llena
        │
        ▼
Laboratorio libre
        │
        ▼
Cafetería media

Salida
```

El sistema procesa siempre el reporte ubicado al inicio.

---

## Operaciones utilizadas

### Offer

```java
offer(reporte)
```

Inserta un nuevo reporte al final de la cola.

Complejidad

```
O(1)
```

---

### Poll

```java
poll()
```

Obtiene y elimina el primer reporte de la cola.

Complejidad

```
O(1)
```

---

# Justificación técnica

Se eligió una cola porque implementa el comportamiento **FIFO (First In, First Out)**.

Esto garantiza que los reportes sean procesados exactamente en el orden en que fueron recibidos, evitando que reportes recientes se procesen antes que los más antiguos.

---

# Comparación de estructuras utilizadas

| Estructura | Tipo | Operaciones principales | Complejidad |
|------------|------|-------------------------|-------------|
| Lista Enlazada Simple | Dinámica | Insertar, Buscar, Eliminar, Recorrer | O(n) |
| Pila (Stack) | LIFO | Push, Pop | O(1) |
| Cola (Queue) | FIFO | Offer, Poll | O(1) |

---


 Detalle técnico: Recursividad

 Búsqueda recursiva de lugares

Permite encontrar un lugar específico comparando su nombre con cada elemento del
arreglo, mediante llamadas sucesivas al mismo método en lugar de un ciclo tradicional.

- **Caso base:** (1) el nombre buscado coincide con un lugar del arreglo, o
  (2) se llega al final del arreglo sin encontrar coincidencias.
- **Llamada recursiva:** ocurre cuando el lugar actual no coincide con el buscado;
  el método se llama de nuevo avanzando a la siguiente posición.

 Merge Sort (ordenamiento recursivo)

Organiza los lugares del campus según su distancia, de menor a mayor.

- **Funcionamiento:** divide el arreglo en dos mitades, ordena cada mitad de forma
  recursiva y luego combina ambas partes ya ordenadas.
- **Caso base:** cuando la parte del arreglo tiene un solo elemento o está vacía.
- **Llamada recursiva:** cuando el algoritmo divide el arreglo en dos y vuelve a
  ejecutar Merge Sort sobre cada mitad.
  
  Detalle técnico: Árbol de decisión (IA básica)

 Recomendación de ingreso según aforo — `ArbolDecisionAforo`

Se implementó un árbol de decisión que evalúa el nivel de aforo de un lugar y
recomienda una acción al usuario: ingresar, esperar o evitar la zona.

**Estructura del árbol:**
- Nodo raíz: ¿aforo > 200?
  - Si es verdadero → "Evitar zona: aforo muy alto"
  - Si es falso → siguiente pregunta: ¿aforo > 100?
    - Si es verdadero → "Esperar unos minutos antes de ingresar"
    - Si es falso → "Puede ingresar sin problema"

**Relación con IA básica:** el árbol de decisión es una de las técnicas más simples
de inteligencia artificial para clasificación: mediante reglas jerárquicas de tipo
"si-entonces", el sistema clasifica automáticamente cada situación y produce una
recomendación sin intervención humana directa.

**Decisión que produce:** una recomendación textual (evitar, esperar o ingresar)
según el nivel de aforo registrado en cada lugar del campus.

Cómo ejecutar el proyecto (módulo de estructuras estáticas)

1. Clonar el repositorio:
```bash
   git clone [link-del-repo]
```
2. Ubicarse en la carpeta del módulo:
```bash
   cd src/estructuras-estaticas
```
3. Compilar:
```bash
   javac AnalisisLinealEstatico.java
```
4. Ejecutar:
```bash
   java AnalisisLinealEstatico
```

 Evidencia de ejecución

<img width="725" height="615" alt="image" src="https://github.com/user-attachments/assets/2ac59c21-c6fb-4727-acf8-f6dc5c5419a6" />


 Video de exposición

🔗 [Ver video en YouTube](enlace-aqui)

Aporte de cada integrante

- Sandro Callañaupa Portal: Estructuras lineales estáticas (vector y matriz), recursividad, README, GitHub y sustentación
- Claudio Saldaña Isaac: Planteamiento del problema y modelado inicial - Estructuras lineales estáticas
- Alvaro Daniel Pino Chavez : Grafo y Busqueda
- favian andre hurtado carlos : listas enlazada, lifo y fifo
 










