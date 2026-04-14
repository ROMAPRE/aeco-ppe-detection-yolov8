# Checklist de Gobernanza AECO

## 1. Procedencia de los Datos

- **Fuente:** Dataset de detección de Equipos de Protección Personal (PPE) obtenido a través de Roboflow.
- **Tipo de dataset:** Dataset público utilizado con fines educativos en el curso MAIC1125 – Visión Computacional.
- **Formato:** Exportado desde Roboflow en formato YOLOv8.
- **División del dataset:** 80% entrenamiento / 20% validación.
- **Propietario original:** Roboflow Universe / autores originales del dataset.

Nota: El dataset fue utilizado únicamente para fines educativos y experimentales en el contexto del curso.


---

# 2. Tratamiento de PII (Privacidad)

El dataset contiene imágenes de trabajadores en obra.

Posibles datos personales identificables (PII):

- Rostros de trabajadores
- Características físicas identificables

Medidas adoptadas:

- El modelo NO realiza reconocimiento de identidad.
- El objetivo es únicamente detectar el uso de Equipos de Protección Personal (PPE).
- En aplicaciones reales se recomienda aplicar:
  - desenfoque de caras
  - anonimización de personas
  - consentimiento de los trabajadores.

Esto sigue el principio de **minimización de datos**, recogiendo únicamente la información necesaria para detectar el uso de EPI.


---

# 3. Minimización de Datos

El sistema fue diseñado para detectar únicamente:

- casco de seguridad
- chaleco de seguridad
- persona

No se recopila ni se procesa:

- identidad de trabajadores
- datos biométricos
- información personal adicional

El modelo solo analiza **presencia o ausencia de equipo de protección**.


---
# 4.Marco Regulatorio (GDPR y EU AI Act)
Este sistema puede estar sujeto a regulación europea en materia de inteligencia artificial y protección de datos.
Normativas relevantes:
- GDPR (Reglamento General de Protección de Datos)
- EU AI Act (Regulación de sistemas de IA de alto riesgo)
Clasificación del sistema:
- Este sistema puede considerarse de "alto riesgo" si se utiliza en contextos reales de seguridad laboral.
Riesgos legales:
- Captura de imágenes de trabajadores (posible tratamiento de datos personales)
- Uso en toma de decisiones relacionadas con seguridad

Medidas de mitigación:
- El sistema NO identifica personas (solo detecta PPE)
- Se recomienda anonimización (blur de rostros)
- Uso limitado a "screening preliminar", no decisión final
- Supervisión humana obligatoria

Nota:
El sistema debe cumplir con la normativa aplicable antes de cualquier uso en entorno real.

---

# 5. Declaración de Limitaciones

Este modelo tiene limitaciones importantes y **NO debe utilizarse como sistema de seguridad autónomo**.

Casos donde el modelo puede fallar:

- iluminación baja
- lluvia o niebla
- oclusión parcial del trabajador
- trabajadores muy pequeños en la imagen
- objetos visualmente similares al casco o chaleco

El modelo es únicamente una **herramienta de apoyo para inspección visual preliminar**.

Debe existir siempre **revisión humana**.

##Limitación crítica identificada:
Durante la evaluación del modelo, las clases "no helmet" y "no vest" presentan un rendimiento extremadamente bajo (AP ≈ 0.000).
Esto implica que el modelo NO detecta correctamente casos de incumplimiento de PPE.

Impacto:
- El sistema no identifica trabajadores sin casco o chaleco
- Este fallo corresponde a un Falso Negativo de alto riesgo

Conclusión:
El modelo, en su estado actual, NO es adecuado para aplicaciones reales de seguridad laboral.
Debe considerarse únicamente como un prototipo experimental.

---

# 6. Declaración de Riesgos (FN vs FP)

En aplicaciones de seguridad en construcción existen dos tipos principales de errores.

## Falso Negativo (FN)
El modelo no detecta un trabajador sin casco.

Consecuencia potencial:
- riesgo de accidente laboral
- falsa sensación de seguridad

Este es el **riesgo más crítico** en este tipo de aplicación.

## Falso Positivo (FP)
El modelo detecta incorrectamente una falta de PPE.

Consecuencia potencial:
- falsas alarmas
- revisión manual innecesaria

En seguridad laboral se prefiere **tolerar más FP antes que FN**.


---

# 7. Humano en el Bucle

El sistema debe utilizarse solo como herramienta de apoyo.

Proceso recomendado:

1. El modelo detecta posibles incumplimientos de PPE.
2. Un supervisor de seguridad revisa las detecciones.
3. La decisión final la toma una persona.

El modelo **no sustituye a un inspector de seguridad**.


---

# 8. Licencia del Proyecto

Tipo de licencia del repositorio:

MIT License

Esto significa que:

- el código puede ser reutilizado
- el autor no asume responsabilidad por su uso
- el proyecto se publica con fines educativos.


---

# 9. Derechos del Dataset

El dataset utilizado en este proyecto:

- proviene de Roboflow / fuentes públicas
- se utiliza únicamente con fines educativos
- los derechos originales pertenecen a los creadores del dataset

Este repositorio **no redistribuye el dataset completo**, sino que referencia la versión disponible en Roboflow.


---

# Declaración Final

Este proyecto es un **prototipo académico de visión computacional aplicado al sector AECO**.

El modelo fue entrenado para demostrar el uso de YOLOv8 en la detección de Equipos de Protección Personal en obra.
El sistema debe considerarse únicamente como una herramienta de **screening preliminar y no debe utilizarse como único sistema de verificación de seguridad.**
Descargo de responsabilidad:
Este modelo es una herramienta asistiva para screening preliminar.
Produce falsos negativos y falsos positivos.
**NO** debe utilizarse como único sistema de verificación en decisiones críticas de seguridad.
