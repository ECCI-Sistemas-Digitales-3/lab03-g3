[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=19144135&assignment_repo_type=AssignmentRepo)
# Lab03: Visualización de Datos en Raspberry Pi Zero W

## Integrantes


## Documentación

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