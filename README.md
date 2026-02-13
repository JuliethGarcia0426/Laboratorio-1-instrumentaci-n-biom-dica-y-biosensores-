# Laboratorio 1

Este documento presenta el desarrollo de un sistema para la medición y análisis de la respiración humana utilizando un micrófono como sensor indirecto. Se adquiere la señal respiratoria, se procesa en MATLAB y se analiza tanto en el dominio del tiempo como en el dominio de la frecuencia.

El sistema permite diferenciar patrones de respiración relajada y respiración mientras se habla, a partir del comportamiento temporal y espectral de la señal.

---

## Objetivo

Diseñar e implementar un algoritmo capaz de:
- Adquirir la señal respiratoria mediante un micrófono
- Procesar la señal para reducir ruido y offset
- Detectar automáticamente las respiraciones
- Calcular la frecuencia respiratoria
- Analizar la señal en frecuencia mediante FFT
- Comparar dos condiciones respiratorias distintas

---

## Descripción general del código

El código fue desarrollado en MATLAB y se divide en cuatro etapas principales: configuración del sistema, adquisición de la señal, procesamiento y análisis de resultados.

---

## Configuración del sistema

Inicialmente se configuran los parámetros de comunicación serial entre MATLAB y el microcontrolador Arduino, estableciendo el puerto, la velocidad de transmisión y la duración de la adquisición.  
Además, se definen la frecuencia de muestreo y el número total de muestras que se van a adquirir durante la evaluación.

---

## Adquisición de la señal

Durante la ejecución, MATLAB recibe en tiempo real los datos enviados por el Arduino. Cada dato corresponde a una muestra de la señal captada por el micrófono.  
La señal se grafica en tiempo real para visualizar el comportamiento respiratorio durante la adquisición.

---

## Procesamiento de la señal

Para obtener una señal respiratoria interpretable, se aplican las siguientes etapas de procesamiento:

- **Eliminación de offset:**  
  Se utiliza una ventana móvil para estimar el valor promedio de la señal y eliminar desplazamientos debidos al sensor o a condiciones ambientales.

- **Rectificación:**  
  Se toma el valor absoluto de la señal para facilitar la detección de los ciclos respiratorios.

- **Ajuste de ganancia:**  
  Se normaliza la amplitud de la señal para trabajar con valores manejables.

- **Filtrado pasa bajas:**  
  Se implementa un filtro Butterworth de cuarto orden con frecuencia de corte de 0.1 Hz, con el objetivo de aislar las componentes de baja frecuencia asociadas a la respiración y eliminar ruido de alta frecuencia, especialmente el generado por la voz.

---

## Detección automática de respiraciones

Una vez procesada la señal, se identifican los picos correspondientes a cada ciclo respiratorio.  
Se establecen criterios de distancia mínima entre picos y prominencia mínima para evitar la detección de ruido como respiraciones.

A partir de los picos detectados se calcula:
- El número total de respiraciones
- La frecuencia respiratoria en respiraciones por minuto (rpm)
- El periodo respiratorio promedio

---

## Análisis en frecuencia

Se aplica la Transformada Rápida de Fourier (FFT) a la señal respiratoria para obtener su espectro de frecuencia.  
El análisis permite identificar la frecuencia dominante, asociada al ritmo respiratorio, y comparar el contenido espectral entre respiración relajada y respiración mientras se habla.

---

## Resultados

A continuación se presentan las cuatro señales analizadas:

### Respiración relajada – Dominio del tiempo
<img width="717" height="456" alt="SEÑAL RESP RELAX" src="https://github.com/user-attachments/assets/7e21f708-01a3-45ea-ba7d-de0dad6323f4" />


---

### Respiración relajada – Dominio de la frecuencia
![WhatsApp Image 2026-02-12 at 8 20 22 PM](https://github.com/user-attachments/assets/c515455c-9955-41cc-8ae7-3689d007970b)


---

### Respiración hablando – Dominio del tiempo
<img width="690" height="449" alt="SEÑAL RESP HAB" src="https://github.com/user-attachments/assets/2223ec61-4269-4879-9e4b-cd3a927caa15" />


---

### Respiración hablando – Dominio de la frecuencia
![WhatsApp Image 2026-02-12 at 8 20 22 PM (2)](https://github.com/user-attachments/assets/9a525f0a-b537-470e-8765-a5ce18c305db)


---

## Análisis de resultados

En la respiración relajada se observa un patrón más periódico y estable, con una frecuencia dominante bien definida.  
En la respiración mientras se habla, la señal presenta mayor variabilidad y un espectro más disperso debido a la superposición de componentes de la voz.

Estos resultados evidencian que el algoritmo permite diferenciar entre distintos patrones respiratorios a partir de una señal acústica.

---

## Conclusiones

- El micrófono puede utilizarse como un sensor indirecto para la medición de la respiración.
- El procesamiento digital es fundamental para obtener una señal respiratoria interpretable.
- El análisis temporal y espectral permite caracterizar distintos patrones respiratorios.
- El sistema es de bajo costo y adecuado para fines académicos en ingeniería biomédica.

---

## Autores
Julieth Paola García Padilla ~ 5600769
Yader Steeven Ortiz Mendez ~ 5600782
Andres Felipe Torres Morales ~ 5600825
Ingeniería Biomédica
