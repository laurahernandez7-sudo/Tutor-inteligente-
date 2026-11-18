# Tutor de Inglés Personalizado: prototipo adaptativo de refuerzo para estudiantes de nivel A1

**María Fernanda Rodríguez**  
Universidad de Ibagué, Programa de Ingeniería de Sistemas, Ibagué, Colombia  
maria.rodriguez22@estudiantesunibague.edu.co

**Laura Sofía Hernández**  
Universidad de Ibagué, Programa de Ingeniería de Sistemas, Ibagué, Colombia  
laura.hernandez7@estudiantesunibague.edu.co

**Alexandra La Cruz** (docente y autora final)  
Universidad de Ibagué, Ibagué, Colombia  
alexandra.lacruz@unibague.edu.co

## Resumen
En cursos introductorios de inglés, los estudiantes pueden necesitar tiempos y ejercicios de refuerzo diferentes, mientras que las plataformas generales suelen organizar el material por módulos comunes. Se diseñó un prototipo llamado **Tutor de Inglés Personalizado** que organiza cuatro lecciones A1 y ajusta la selección de preguntas de acuerdo con el desempeño individual. Se implementó únicamente con Python y bibliotecas estándar (`tkinter`, `csv`, `json` y `pathlib`). El banco de datos se construyó para este proyecto y contiene 32 preguntas con tres opciones, retroalimentación y dos niveles por tema. El sistema explora los contenidos todavía no evaluados, calcula el porcentaje de aciertos por tema, prioriza el tema con más errores y propone ejercicios de reto cuando se cumple un umbral configurable. Se ejecutaron ocho pruebas automáticas de lógica y todas fueron satisfactorias (8/8); también se comprobó el inicio de la interfaz en un entorno gráfico. Los resultados demuestran viabilidad técnica de esta regla adaptativa, pero no prueban mejoras de aprendizaje en estudiantes reales. El proyecto ofrece una base simple, revisable y extensible para practicar inglés elemental con mayor individualización.

**Palabras clave:** tutor inteligente, inglés A1, aprendizaje adaptativo, reglas, Python.

## 1. Introducción
El problema abordado es que estudiantes con ritmos y necesidades de refuerzo distintos reciben con frecuencia una secuencia común de ejercicios. Quien no domina un contenido, por ejemplo el verbo *to be*, puede requerir práctica adicional antes de avanzar. Por eso, este prototipo busca ofrecer una experiencia de práctica personalizada sin diagnosticar condiciones clínicas ni sustituir al docente. El objetivo general es **desarrollar un tutor de inglés básico capaz de ajustar las preguntas al desempeño de cada estudiante**. Los objetivos específicos son: (a) organizar lecciones y ejercicios de cuatro temas A1, (b) registrar aciertos y errores por tema, (c) recomendar refuerzo mediante reglas explícitas y (d) verificar el comportamiento con pruebas reproducibles.

El alcance se restringe a una aplicación local de escritorio que imita la organización de un aula virtual (lecciones, evaluación, progreso y vista docente). No pretende reproducir la plataforma web Canvas ni Moodle. El nivel A1 se toma como referencia curricular general del Marco Común Europeo de Referencia para las Lenguas (MCER) [3].

## 2. Trabajo relacionado y estado del arte
Brusilovsky [1] describe los sistemas hipermedia adaptativos como sistemas que modelan información del usuario y usan ese modelo para ajustar su interacción. Esta idea orienta el historial de respuestas por tema que usa nuestro programa. VanLehn [2] revisa comparaciones entre tutorías humanas y distintas clases de sistemas tutoriales; su trabajo fundamenta el interés educativo del feedback guiado, sin que implique que este prototipo tenga eficacia equivalente a sistemas estudiados. El Consejo de Europa [3] establece descriptores del nivel A1 que inspiran una selección reducida de contenidos elementales. La documentación oficial de Python [4] indica que Tkinter, CSV y JSON están disponibles en su biblioteca estándar y justifican una implementación manejable sin dependencias externas.

Nuestra propuesta se diferencia de un curso estático porque cada pregunta depende del historial del estudiante. A diferencia de sistemas complejos, no entrenamos una red neuronal ni usamos modelos generativos. El enfoque es un conjunto de reglas claras que pueden estudiarse, modificarse y verificarse.

## 3. Métodos y desarrollo
### 3.1. Arquitectura y tecnologías
La **Figura 1** resume el flujo. El estudiante usa la interfaz `app.py` (Tkinter). La lógica `logica.py` lee las lecciones y preguntas, revisa el historial individual, decide el siguiente tema y guarda el resultado en archivos JSON. La biblioteca CSV carga las preguntas; JSON almacena configuraciones, lecciones y avances. Todo el programa principal utiliza exclusivamente bibliotecas estándar de Python [4].

**Figura 1.** Flujo lógico del prototipo: estudiante → interfaz → selección adaptativa → CSV/JSON → progreso y siguiente pregunta.

### 3.2. Conjunto de datos
El conjunto es un banco **creado para el prototipo**, no una muestra de estudiantes reales ni un conjunto para entrenar algoritmos. La **Tabla 1** detalla su composición: 4 temas, 8 preguntas por tema, 4 básicas y 4 de reto; total 32. Cada fila contiene identificador, tema, nivel, enunciado, opciones A/B/C, respuesta correcta y explicación. `lecciones.json` reúne un objetivo, una explicación y cuatro ejemplos por tema. Se inspiró en contenidos elementales compatibles con el MCER A1 [3], sin reclamar evaluación certificada del nivel.

**Tabla 1.** Distribución del banco de preguntas por tema: Verb to be (4 básicas, 4 reto), Personal pronouns (4, 4), Articles a/an (4, 4) y Present simple (4, 4). Total: 16 básicas, 16 reto, 32 preguntas.

### 3.3. Reglas de adaptación
1. Se identifica el estudiante por su nombre local y se carga su historial.
2. Mientras existan temas sin ninguna respuesta, se selecciona uno no evaluado; así se consigue una exploración inicial.
3. Cuando todos los temas tienen respuestas, se calcula el rendimiento por tema: **porcentaje = 100 × aciertos / intentos**. Se selecciona el de menor porcentaje.
4. En el tema elegido, si existen al menos **2 intentos** y el acierto es **75 % o más**, se selecciona nivel `reto`; de otro modo se usa `basico`. Son valores editables en `configuracion.json`, no constantes globales fijadas en el código.
5. Primero se elige una pregunta no usada de ese tema y nivel. Cuando se agotan, se permite repetir una.
6. Al responder, se registra acierto/error, aparece la explicación y se recalculan los resultados. Cada sesión contiene **5 preguntas** (también configurable).

Estas reglas representan personalización por errores observados. Su simplicidad permite explicar su decisión sin entrenamiento de modelos. Si dos temas empatan, el algoritmo utiliza la cantidad de intentos y el orden del banco para decidir de forma determinista.

### 3.4. Interfaz y almacenamiento
Como muestra la **Figura 2**, el prototipo usa cinco pestañas: Inicio, Lecciones, Quiz adaptativo, Mi progreso y Vista docente. El archivo `datos/estudiantes.json` guarda localmente los registros; se excluye de GitHub para evitar publicar avances personales. La Vista docente es solo demostrativa, sin autenticación, y por ello no debe usarse con datos sensibles ni con estudiantes reales en una instalación compartida. Se recomienda usar nombres ficticios en la presentación.

**Figura 2.** Captura de la ventana de inicio del Tutor de Inglés Personalizado ejecutado con Tkinter.

## 4. Resultados
Se ejecutaron **8 pruebas de software** con `unittest`. La **Tabla 2** muestra las situaciones cubiertas y los resultados. Todas terminaron correctamente (8/8). Adicionalmente, se abrió la aplicación en un entorno gráfico y se capturó la pantalla de inicio de la Figura 2. Estos resultados son pruebas técnicas de funcionamiento y no resultados de impacto pedagógico.

**Tabla 2.** Pruebas automáticas: (1) primer tema sin evaluar — OK; (2) siguiente tema no evaluado — OK; (3) prioridad a más errores — OK; (4) paso a nivel reto — OK; (5) registro y resumen de respuestas — OK; (6) porcentaje por tema — OK; (7) guardado y carga JSON — OK; (8) lectura del banco de 32 preguntas — OK.

**Escenario ilustrativo (simulado, sin participantes):** un estudiante contesta mal `Verb to be` y bien los otros tres temas. Los porcentajes quedan 0 % en `Verb to be` y 100 % en los demás. Cuando vuelve a elegir pregunta, el algoritmo prioriza `Verb to be`. En otro escenario controlado, dos aciertos sobre dos intentos equivalen a 100 %, y, si el tema vuelve a ser seleccionado, el nivel disponible pasa a `reto`. Ambos comportamientos están cubiertos por la lógica y sus pruebas.

## 5. Discusión y limitaciones
El prototipo cumple el objetivo de adecuar la secuencia de práctica con una regla comprensible. Su principal ventaja es que no requiere internet, instalación de paquetes externos ni bases de datos complejas. Como limitaciones, el historial depende del nombre (sin contraseña), la vista docente no protege la privacidad de registros, el banco de 32 preguntas puede agotarse y la interfaz no funciona desde un navegador. Además, porcentajes calculados con pocos intentos pueden ser inestables. No hay validación con estudiantes, medición de rendimiento a largo plazo ni diagnóstico de trastornos de aprendizaje. Una evaluación educativa real exigiría un diseño experimental y consentimiento informado.

## 6. Conclusiones
Se implementó un prototipo de tutor adaptativo para inglés A1 con Python básico y datos editables. El sistema combina cuatro lecciones, 32 preguntas, retroalimentación inmediata y un historial por estudiante. Las ocho pruebas automatizadas verifican la lógica definida; sin embargo, no permiten afirmar que el uso del software mejore las calificaciones. La contribución del proyecto es una propuesta pequeña y defendible de personalización educativa, que puede ampliarse con más temas, autenticación, seguimiento longitudinal y pruebas con usuarios.

## 7. Disponibilidad del código, los datos y el video
- **Código GitHub:** https://github.com/laurahernandez7-sudo/Tutor-inteligente-de-ingles (verificar que incluya los archivos antes de la entrega).
- **Conjunto de datos Drive:** [PEGAR AQUÍ ENLACE REAL COMPARTIDO CON LA PROFESORA].
- **Video promocional de 3 minutos:** [PEGAR AQUÍ ENLACE REAL DEL VIDEO].

**Nota:** Los dos últimos enlaces no pueden completarse hasta subir los materiales a las cuentas del equipo. Antes de enviar, reemplazar los campos anteriores.

## Referencias
[1] P. Brusilovsky, “Adaptive Hypermedia,” *User Modeling and User-Adapted Interaction*, vol. 11, pp. 87–110, 2001. https://doi.org/10.1023/A:1011143116306

[2] K. VanLehn, “The Relative Effectiveness of Human Tutoring, Intelligent Tutoring Systems, and Other Tutoring Systems,” *Educational Psychologist*, vol. 46, no. 4, pp. 197–221, 2011. https://doi.org/10.1080/00461520.2011.611369

[3] Council of Europe, *Common European Framework of Reference for Languages: Learning, Teaching, Assessment - Companion Volume*, 2020. https://www.coe.int/en/web/common-european-framework-reference-languages/documents

[4] Python Software Foundation, *The Python Standard Library: tkinter, csv, json*, documentación oficial. https://docs.python.org/3/library/
