# Guía exacta para entregar el proyecto

## 1. Abrir el programa
1. Descarga el ZIP del proyecto, haz clic derecho > **Extraer todo**.
2. Abre la carpeta del proyecto donde aparece `app.py`.
3. Arriba, en la barra de dirección de la carpeta, escribe `cmd` y Enter.
4. Ejecuta `py app.py` (o `python app.py`). **No abras solamente el `.py` dentro del ZIP**.
5. Ingresa el nombre `Prueba Clase` y revisa las cinco pestañas.
6. Completa al menos 5 preguntas del quiz; inspecciona **Mi progreso** y la recomendación.
7. Ejecuta las pruebas: `py -m unittest discover -s pruebas -v`.
8. Si la consola informa `No module named tkinter`, instala Python desde python.org con soporte Tcl/Tk. En Windows suele venir incluido.

## 2. Grabar el video de 3 minutos
En Windows presiona `Windows + Alt + R` si está disponible la Xbox Game Bar, o usa la herramienta de grabación de pantalla de Windows. Muestra la ventana de la aplicación y lee el texto preparado en `GUION_VIDEO_3_MINUTOS.md`. El video debe mostrar: inicio, lecciones, preguntas, error, adaptación y progreso. Grabar con datos ficticios.

## 3. Crear o actualizar GitHub
1. Accede a https://github.com con tu cuenta.
2. Crea un repositorio llamado `tutor-de-ingles-personalizado` **o utiliza el repositorio vacío existente del equipo**.
3. En el repositorio abre **Add file > Upload files**.
4. Arrastra `app.py`, `logica.py`, `configuracion.json`, `README.md`, `.gitignore` y las carpetas `datos` y `pruebas` manteniendo la estructura.
5. **No publiques `datos/estudiantes.json` cuando contenga estudiantes reales**. Si subes un archivo vacío `{}`, no contiene información privada.
6. Haz clic en **Commit changes**.
7. Verifica en GitHub que puedes abrir `app.py`, `logica.py`, `datos/preguntas.csv`, `datos/lecciones.json` y `pruebas/test_logica.py`.
8. Copia el enlace de la página principal del repositorio y pégalo donde el PDF marca **GitHub**.
9. Descarga el repositorio desde **Code > Download ZIP** y ejecuta `py app.py` para comprobar que no faltan archivos.

**Importante:** GitHub es un repositorio de código; no hace funcionar automáticamente esta aplicación de escritorio en una página web. Para evaluarla, el profesor debe descargarla y ejecutarla con Python.

## 4. Compartir el conjunto de datos en Google Drive
1. Entra a https://drive.google.com.
2. Crea la carpeta **Tutor de Inglés Personalizado - Datos A1**.
3. Sube `preguntas.csv`, `lecciones.json`, y opcionalmente `configuracion.json` y `DESCRIPCION_DATOS.md`.
4. Clic derecho sobre la carpeta > **Compartir**.
5. Agrega `alexandra.lacruz@unibague.edu.co` como **Lector** o configura acceso por enlace si así lo solicita.
6. Copia el enlace y pégalo donde dice **Drive** en el informe.
7. Comprueba el acceso en una ventana de incógnito o con la cuenta autorizada.

## 5. Compartir el video
1. Graba el video, idealmente 3:00 min.
2. Súbelo a YouTube como **No listado** o a Drive.
3. Si lo subes a Drive, comparte acceso de lectura con la docente.
4. Pega la URL en la sección de enlaces del informe.
5. Prueba el enlace en una ventana de incógnito o desde la cuenta de la profesora.

## 6. Preparar el PDF final
El PDF contiene los elementos del documento requerido. **Antes de entregarlo, añade las tres URL reales en la sección de enlaces**. Para no tener que editar el PDF, abre el archivo de texto `Informe_Tecnico_Editable.md`, coloca los enlaces, y utiliza un editor Markdown / procesador de texto para exportarlo a PDF. También puedes añadir una última página al PDF existente con los tres enlaces, siempre que queden claramente identificados.

## 7. Lista de verificación para la profesora
- [ ] Título informativo del problema.
- [ ] Autoras, afiliación, correos; Alexandra La Cruz como autora final.
- [ ] Resumen, introducción, estado del arte, métodos, resultados, conclusiones y referencias.
- [ ] Tablas y figuras numeradas, tituladas y citadas en el texto.
- [ ] Cada referencia bibliográfica citada dentro del informe.
- [ ] Repositorio GitHub con código real y archivo README.
- [ ] Carpeta Drive con dataset y acceso para la docente.
- [ ] Video promocional de 3 minutos con enlace.
- [ ] Demostración en Windows, resultados guardados y 8 pruebas OK.
