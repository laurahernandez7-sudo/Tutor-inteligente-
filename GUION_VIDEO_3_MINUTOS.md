# Guion del video promocional (aprox. 3 minutos)

**Título en pantalla:** Tutor de Inglés Personalizado - Universidad de Ibagué

## 0:00-0:30 | Presentación (María Fernanda)
> Hola. Somos María Fernanda Rodríguez y Laura Sofía Hernández. Nuestro proyecto de Sistemas Inteligentes se llama **Tutor de Inglés Personalizado**. Su propósito es apoyar a estudiantes que necesitan reforzar temas de inglés básico a su propio ritmo. La idea surgió porque una plataforma tradicional suele mostrar el mismo contenido a todos, mientras que algunos estudiantes necesitan más práctica en contenidos específicos.

**Pantalla:** título y pestaña Inicio.

## 0:30-1:02 | Solución (Laura Sofía)
> Construimos un aula virtual sencilla, inspirada en la organización de plataformas como Canvas y Moodle, pero desarrollada como aplicación de escritorio usando únicamente Python. Tiene lecciones, un cuestionario, resultados individuales y una vista para el profesor. Trabajamos con cuatro temas del nivel A1: verbo to be, pronombres, artículos y presente simple.

**Pantalla:** abrir Lecciones y mostrar dos temas.

## 1:02-1:55 | Demostración de adaptación (María Fernanda)
> Ahora ingresamos como un estudiante de prueba. Cada pregunta tiene tres opciones y una explicación. El programa registra si la respuesta fue correcta o incorrecta. Primero hace preguntas de temas que todavía no se han evaluado. Cuando ya tiene respuestas de todos los temas, calcula cuál necesita más refuerzo. Por ejemplo, si el estudiante falla en el verbo to be, prioriza ese tema en las preguntas siguientes. Si demuestra buen desempeño, puede recibir ejercicios de reto.

**Pantalla:** ingresar, contestar una pregunta incorrecta, otras correctas, y mostrar cómo se recomienda el tema débil.

## 1:55-2:25 | Progreso (Laura Sofía)
> Aquí vemos los aciertos y los intentos de cada tema. La información queda almacenada en archivos locales para retomar la práctica. También incluimos una vista docente con un resumen. La adaptación no usa inteligencia artificial generativa: es un sistema de reglas sencillo y explicable, adecuado para el alcance del proyecto.

**Pantalla:** pestañas Mi progreso y Vista docente.

## 2:25-3:00 | Cierre (ambas)
> El prototipo cuenta con 32 preguntas, cuatro lecciones y ocho pruebas automáticas de funcionamiento. Su valor está en personalizar el refuerzo sin complicar la experiencia del usuario. Es una primera versión; en el futuro se podrían añadir más temas y una evaluación real con estudiantes. Muchas gracias.

**Pantalla:** resultado de `python -m unittest discover -s pruebas -v` y cierre.

**Consejo:** ensayen el texto a velocidad normal y ajusten pausas para que dure cerca de 3 minutos. No afirmen que comprobaron mejoras en notas porque no hay estudio de usuarios.
