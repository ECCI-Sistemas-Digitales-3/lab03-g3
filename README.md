[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=19144135&assignment_repo_type=AssignmentRepo)
# Lab03: Visualización de Datos en Raspberry Pi Zero W

## Integrantes
[Julieth Alejandra Sandoval Estupiñan](https://github.com/Julieth-Sandoval)

[Jose Angel Campo Vargas](https://github.com/Jose-Angel-Campo-Vargas)

[David Leonardo Castaño Madrigal](https://github.com/IngleonardocM)

## Documentación
# 📈 Monitor de Temperatura en Raspberry Pi

Este proyecto consiste en un sistema de monitoreo **en tiempo real** de la temperatura del procesador de una Raspberry Pi. Utiliza un comando del sistema para obtener la temperatura, la guarda en un archivo CSV y la representa gráficamente con `matplotlib`.

---

## 🧰 Tecnologías y Librerías Usadas

- Python 3
- `matplotlib` – Para la visualización en tiempo real
- `subprocess` – Para ejecutar comandos del sistema
- `csv` – Para guardar los datos
- `os` – Para manejo de archivos
- `time` – Para el control del tiempo

---

## ⚙️ Cómo Funciona

El script:

1. Lee la temperatura del CPU usando el comando `vcgencmd measure_temp`.
2. Guarda la lectura con su timestamp en un archivo CSV.
3. Muestra una gráfica que se actualiza en tiempo real.
4. Mantiene visible solo los últimos segundos de datos (configurable).

---

## 📄 Estructura del Código

### Clase `MonitorTemperaturaRPI`

- `__init__(duracion_max=60, intervalo=0.5, archivo_csv="temperaturas.csv")`:  
  Inicializa las variables, prepara el archivo CSV y la gráfica.

- `leer_temperatura()`:  
  Ejecuta el comando para leer la temperatura del CPU.

- `actualizar_datos()`:  
  Guarda el tiempo y temperatura, y elimina datos antiguos.

- `graficar()`:  
  Dibuja la gráfica en tiempo real.

- `guardar_csv(tiempo, temperatura)`:  
  Escribe los datos en el archivo CSV.

- `ejecutar()`:  
  Ejecuta el ciclo principal del programa hasta que se cierre la gráfica.
---
## 📁 Archivos del Proyecto

- `taller.py`: script principal que realiza la lectura de temperatura, guarda los datos en un archivo `.csv` y grafica la información.
- `temperaturas.csv`: archivo generado con los datos de temperatura (fecha, hora y valor).
- `parte2.py`: módulo o script complementario relacionado con el tratamiento o visualización de los datos.

---

## 📊 Gráfica de Temperatura

La siguiente imagen representa cómo se ve la gráfica de temperatura generada por el script `taller.py`:

![Gráfica Temperatura CPU](/IMAGENES/Grafica.jpeg)

---

## 📋 Visualización del Archivo CSV

A continuación, se muestra una captura del archivo `temperaturas.csv` con los datos recolectados:

![Archivo CSV](/IMAGENES/Datos.jpeg)

---

## ⚙️ ¿Cómo se ejecutó?

Este proyecto se ejecutó desde **Visual Studio Code** utilizando una conexión remota vía **SSH** a la Raspberry Pi.

Pasos generales:
1. Se estableció una conexión SSH desde VS Code.
2. Se ejecutó el script Python en la Raspberry Pi.
3. El script generó los archivos `temperaturas.csv` y la gráfica.
4. Las imágenes resultantes se visualizaron y documentaron para su análisis.

## ❓ Preguntas

**1. ¿Qué hace este script?**  
Este proyecto es un monitor en tiempo real de la temperatura de la Raspberry Pi. Mide la temperatura del CPU y la grafica en una ventana interactiva usando matplotlib. Además, guarda los datos en un archivo `.csv` para análisis posteriores.

---

**2. ¿Qué hace `plt.fignum_exists(self.fig.number)`?**  
Sirve para revisar si la ventana del gráfico sigue abierta. Si el usuario cierra la ventana, esta función devuelve `False`, y el ciclo principal del programa se detiene automáticamente. Así el script no sigue corriendo innecesariamente.

---

**3. ¿Por qué usamos `time.sleep(self.intervalo)`?**  
Le da un respiro al programa entre cada lectura de temperatura.  
Si no lo ponemos, el código corre en un bucle sin parar, usando más CPU y generando lecturas a lo loco.  
Con esto, el programa espera 0.5 segundos (o el valor que pongas) entre cada muestra.

---

**4. ¿Para qué sirve el `__init__`?**  
Es el constructor de la clase. Ahí inicializamos todo lo que el programa necesita al empezar: listas, variables, la figura del gráfico, etc.  
Usar `__init__` hace que el código esté más limpio y organizado, porque solo se inicializa una vez y luego ya puedes usar todo eso en otros métodos de la clase.

---

**5. ¿Qué hace `self.inicio = time.time()`?**  
Guarda la hora exacta en que se inició el monitoreo.  
Después, se calcula el tiempo transcurrido (en segundos) usando `time.time() - self.inicio`, lo cual se usa para el eje X del gráfico.

---

**6. ¿Qué hace `subprocess.check_output(...)`?**  
Ese comando ejecuta un comando del sistema (en este caso, `vcgencmd measure_temp`) y devuelve el resultado.  
Ese resultado lo limpiamos un poco para que nos quede solo el número de la temperatura. Es como abrir una terminal desde Python y leer lo que devuelve.

---

**7. ¿Por qué no se usa directamente `time.time()` para graficar?**  
Porque eso daría un número enorme (como `1682197123.348...`), que es difícil de interpretar.  
En cambio, graficar el tiempo desde que se inició el monitoreo es más útil para análisis:  
_"A los 10 segundos subió la temperatura"_ es más comprensible que _"A las 3:12:43 PM UTC..."_

---

**8. ¿Por qué se usa `self.ax.clear()`?**  
Cada vez que se actualiza el gráfico, se borra lo anterior para no dibujar encima.  
Si no lo hicieras, tendrías líneas repetidas o datos duplicados sobre el mismo gráfico.