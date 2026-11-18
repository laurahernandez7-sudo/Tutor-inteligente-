# Descripción del conjunto de datos: Tutor de Inglés Personalizado

**Tipo:** banco sintético de preguntas y lecciones escritas para este prototipo académico. No contiene respuestas de participantes humanos ni información de personas reales.

- `datos/preguntas.csv`: 32 preguntas originales del prototipo (4 temas × 8 preguntas). Cada tema incluye 4 preguntas básicas y 4 de reto.
- Campos: `id` (identificador), `tema`, `nivel`, `pregunta`, `a`, `b`, `c` (opciones), `correcta` (letra A/B/C), `explicacion` (justificación para retroalimentación).
- `datos/lecciones.json`: 4 temas, cada uno con objetivo, explicación y 4 ejemplos.
- `configuracion.json`: 5 preguntas por sesión, 2 intentos mínimos y 75 % de aciertos para llegar al nivel reto en un tema.

**Origen:** material construido específicamente para la actividad, tomando como orientación general el inglés elemental A1 del MCER (Consejo de Europa, 2020), sin copiar un banco protegido de terceros.

**Uso:** evaluación local, ajuste de la siguiente pregunta según el porcentaje de aciertos de cada tema, feedback inmediato y resumen de progreso. **No** se trata de una muestra estadística, un experimento con estudiantes ni un dataset de entrenamiento de modelos de IA.
