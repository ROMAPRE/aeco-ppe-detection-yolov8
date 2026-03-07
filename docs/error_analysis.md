# Análisis de errores del modelo

## Falsos positivos

Un falso positivo ocurre cuando el modelo detecta un objeto que en realidad no corresponde a la clase predicha.

### 1. Sombra detectada como persona
En algunas imágenes el modelo detecta sombras en el suelo como si fueran personas.

**Posible causa:**  
Las sombras tienen formas similares al contorno de un trabajador y el dataset contiene pocos ejemplos negativos.

### 2. Objetos de obra detectados como PPE
Algunos objetos de obra con colores brillantes pueden ser detectados como casco o chaleco.

**Posible causa:**  
Similitud visual entre objetos de obra y elementos de protección personal.

### 3. Partes de maquinaria detectadas como persona
Algunas estructuras o maquinaria pueden ser detectadas erróneamente como personas.

**Posible causa:**  
Formas verticales similares al cuerpo humano.

---

## Falsos negativos

Un falso negativo ocurre cuando el modelo no detecta un objeto que sí está presente en la imagen.

### 1. Cascos pequeños no detectados
En algunas imágenes los cascos no son detectados.

**Posible causa:**  
El tamaño del objeto es muy pequeño en la imagen.

### 2. Trabajadores parcialmente ocultos
Personas parcialmente ocultas detrás de estructuras o materiales no son detectadas.

**Posible causa:**  
Oclusión parcial del objeto.

### 3. Chalecos en condiciones de iluminación baja
En escenas con poca iluminación el modelo no detecta chalecos reflectantes.

**Posible causa:**  
Variaciones de iluminación no suficientemente representadas en el dataset.

---

## Mejoras prioritarias del dataset

Para mejorar el rendimiento del modelo se proponen las siguientes acciones:

### 1. Aumentar el tamaño del dataset
Agregar más imágenes de obras con trabajadores utilizando PPE.

### 2. Incluir más ejemplos de objetos pequeños
Incorporar más imágenes donde cascos y botas aparezcan a diferentes escalas.

### 3. Mejorar la diversidad del dataset
Añadir imágenes con distintas condiciones de iluminación, ángulos de cámara y tipos de obra.
