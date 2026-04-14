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

---
## 🔴 Fallo crítico del modelo (clases de incumplimiento PPE)
El modelo presenta un fallo crítico en las clases "no helmet" y "no vest", con un AP cercano a 0.000.
Esto indica que el modelo no detecta correctamente casos donde los trabajadores NO llevan equipo de protección.
Impacto:
    • No se detectan situaciones de riesgo real en obra
    • Este error corresponde a un Falso Negativo crítico en contexto AECO
Posible causa:
    • Dataset desbalanceado (pocos ejemplos de "no helmet" y "no vest")
    • Dificultad visual para diferenciar presencia vs ausencia de PPE
    • Insuficiente variabilidad en los datos
Conclusión:
Este fallo cambia la valoración del prototipo.
Aunque el modelo puede detectar personas y algunos elementos de PPE, no cumple su objetivo principal de seguridad, ya que no identifica correctamente los casos de incumplimiento (no helmet / no vest).
Por tanto, el sistema no es válido como herramienta de monitorización de seguridad en su estado actual.

---

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


### 1. Balanceo de clases críticas:
    • +50 imágenes de trabajadores SIN casco (no helmet)
    • +50 imágenes de trabajadores SIN chaleco (no vest)
    • Asegurar distribución equilibrada entre clases PPE / no PPE

### 2. Mejora de detección de objetos pequeños:
    • +40 imágenes con cascos a larga distancia
    • Incluir anotaciones precisas de objetos pequeños
    • Aumentar resolución de entrenamiento (imgsz 640 → 800)

### 3. Robustez en condiciones reales de obra:
    • +30 imágenes en condiciones nocturnas
    • +30 imágenes con lluvia o baja visibilidad
    • +30 imágenes con oclusión parcial de trabajadores

### 4. Mejora de ejemplos negativos:
    • +30 imágenes con sombras, maquinaria y objetos similares a PPE
    • Objetivo: reducir falsos positivos

Total recomendado: +200 imágenes adicionales

# Evaluación final en contexto AECO
En el contexto de seguridad en obra, los resultados del modelo presentan limitaciones críticas.
    • El modelo muestra un rendimiento bajo en la detección de incumplimiento de PPE (no helmet / no vest)
    • Esto implica la presencia de Falsos Negativos de alto impacto

### Implicaciones:
    • No detectar trabajadores sin equipo de protección puede derivar en accidentes laborales
    • El sistema no es fiable como herramienta autónoma de seguridad

### Decisión técnica:
    • El modelo debe considerarse únicamente como un prototipo experimental
    • Es necesario mejorar el dataset antes de cualquier uso en entorno real

### Recomendación:
    • Priorizar la mejora del recall en clases críticas (PPE)
    • Reentrenar el modelo con dataset balanceado y mayor variabilidad
