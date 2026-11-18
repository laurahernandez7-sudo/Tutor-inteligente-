# Guía para explicar y defender el Tutor de Inglés Personalizado

## 1. Explicación en 45 segundos
El proyecto es un pequeño tutor adaptativo de inglés básico hecho en Python con Tkinter. Tiene un banco de preguntas en CSV, lecciones en JSON y una interfaz con cinco pestañas. Cada respuesta se guarda en un archivo local. El algoritmo primero busca temas sin evaluar y luego elige el tema con menos porcentaje de aciertos. Si el estudiante cumple el umbral de acierto configurado recibe preguntas de reto. No es aprendizaje automático: es inteligencia basada en reglas.

## 2. ¿Dónde está cada parte del código?
| Archivo | Función |
| --- | --- |
| `app.py` | Crea la ventana, botones, pestañas, presenta preguntas y resultados. |
| `logica.py` | Contiene las reglas de selección, evaluación y persistencia. |
| `preguntas.csv` | Datos de preguntas y respuestas correctas, fuera del programa. |
| `lecciones.json` | Explicaciones y ejemplos por tema. |
| `configuracion.json` | Parámetros modificables sin tocar el código. |
| `estudiantes.json` | Guarda el historial individual en el equipo. |
| `test_logica.py` | Comprueba la lógica con 8 pruebas. |

## 3. Explica la regla adaptativa paso a paso
1. Cada estudiante inicia un historial con su nombre.
2. Se muestra una pregunta de un tema que no haya respondido; esto permite explorar los cuatro temas.
3. Cuando todos los temas han aparecido, se calcula el porcentaje de aciertos por tema: `aciertos / intentos × 100`.
4. Se selecciona el tema de menor porcentaje para reforzarlo.
5. Si en el tema hay **2 intentos o más** y el porcentaje es **75 % o más**, se usa el nivel `reto`; en caso contrario el nivel `basico`.
6. Se elige primero una pregunta que ese estudiante aún no haya respondido dentro del nivel; si las agotó, se reutiliza una.
7. Se registra el resultado en JSON, aparece la explicación y se actualiza el progreso.

**Caso que demuestra adaptación:** un acierto en Pronouns, Articles y Present simple, pero un error en Verb to be. Los porcentajes son 100 %, 100 %, 100 % y 0 %, así que se recomienda Verb to be.

## 4. Preguntas posibles de la profesora

**1. ¿Por qué llaman inteligente al sistema?**  
Porque usa el historial del estudiante para decidir qué mostrar después, no una secuencia idéntica para todos. El sistema es adaptativo basado en reglas.

**2. ¿Usan redes neuronales o aprendizaje automático?**  
No. Utilizamos reglas deterministas y transparentes. Para cuarto semestre permite implementar, probar y explicar cada decisión.

**3. ¿Qué problema atiende?**  
Las diferencias de ritmo y las dificultades para dominar temas básicos de inglés. La aplicación ofrece práctica y feedback según errores; no diagnostica trastornos.

**4. ¿Qué tiene de Canvas o Moodle?**  
La estructura de aula: lecciones, actividades, resultados y vista docente. No implementa las funcionalidades avanzadas de esas plataformas ni es una página web.

**5. ¿Cómo se decide la siguiente pregunta?**  
Se priorizan temas sin evaluar, luego el de menor porcentaje de aciertos y, dentro del tema, un nivel básico o reto según el progreso.

**6. ¿Qué pasa si el estudiante siempre se equivoca?**  
Continuará recibiendo preguntas básicas del tema que necesita refuerzo, con explicaciones. Esto no garantiza aprendizaje, pero cambia la práctica propuesta.

**7. ¿Cómo avanza al nivel reto?**  
Cuando tiene al menos dos intentos en ese tema y un acierto igual o mayor a 75 %. Esos valores pueden cambiarse en el JSON de configuración.

**8. ¿Dónde están las constantes?**  
No declaramos constantes globales de reglas: los parámetros se leen de `configuracion.json` y las respuestas están en el CSV. Hay literales estructurales necesarios como las opciones A/B/C.

**9. ¿Por qué usan CSV?**  
Es sencillo de editar, compartir y recorrer con `csv.DictReader`; no exige instalar un servidor o base de datos.

**10. ¿Por qué usan JSON?**  
Permite guardar configuraciones, lecciones e historial con estructura legible sin una base de datos externa.

**11. ¿Qué librerías usa?**  
`tkinter` para interfaz, `csv` para preguntas, `json` para persistencia, `pathlib` para rutas y `unittest` en las pruebas. Todas son parte de Python estándar.

**12. ¿Cuántos datos tienen?**  
32 preguntas, cuatro temas, dos niveles por tema y cuatro lecciones. Son preguntas elaboradas para el prototipo, no datos de estudiantes reales.

**13. ¿Cómo midieron resultados?**  
Se ejecutaron ocho pruebas automáticas de lógica y funcionan. Eso valida comportamiento técnico, no efectividad educativa.

**14. ¿Cómo prueban que adapta el contenido?**  
Podemos responder mal un tema, bien los demás y observar que la siguiente pregunta viene del tema con menor porcentaje.

**15. ¿Qué es un porcentaje de acierto?**  
El cociente de respuestas correctas entre el total de respuestas de un tema, multiplicado por 100.

**16. ¿Qué limitaciones tiene?**  
Sin servidor, sin contraseñas, banco reducido y sin pruebas con estudiantes. Es un prototipo local de bajo costo.

**17. ¿Cómo evitaron escribir las respuestas en el programa?**  
Todas están en `preguntas.csv`; la lógica toma la letra correcta desde el archivo.

**18. ¿Qué harían como siguiente versión?**  
Mejorar acceso de usuarios, ampliar preguntas, añadir lectura y audio, y hacer una prueba con consentimiento de estudiantes.

**19. ¿Se guardan los datos al cerrar la app?**  
Sí. Después de cada respuesta se escribe `datos/estudiantes.json`, que se vuelve a leer al abrir el programa.

**20. ¿Qué aportó cada integrante?**  
Ambas deben describir solo el trabajo que realmente hicieron. Una división sugerida para la exposición es: María Fernanda explica problema y método; Laura Sofía explica archivos, interfaz y pruebas. No inventar actividades que no realizaron.

## 5. Demostración técnica concreta
1. `py app.py` y entrar con un nombre ficticio.
2. Visitar Lecciones y describir que vienen de `lecciones.json`.
3. Contestar 4 preguntas alternando un fallo y tres aciertos.
4. Verificar el tema recomendado.
5. Abrir `preguntas.csv` para mostrar que las respuestas no están fijas en el código.
6. Cambiar `preguntas_por_sesion` en el JSON a otro valor y explicar su efecto (reiniciar aplicación).
7. En la terminal ejecutar `py -m unittest discover -s pruebas -v`; señalar `OK`.
