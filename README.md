
# Estimación del nivel de estrés mediante Respuesta Galvánica Cutánea (GSR)

**Autores**

- Yader Steeven Ortiz  
- Andres Felipe Torres  
- Julieth Paola García  

---

# Introducción

La **actividad electrodérmica (EDA)** corresponde a los cambios en las propiedades eléctricas de la piel producidos por la actividad del sistema nervioso autónomo. Uno de los indicadores más utilizados para medir esta actividad es la **respuesta galvánica cutánea (GSR)**, la cual refleja variaciones en la conductancia de la piel asociadas principalmente con la actividad de las glándulas sudoríparas.

Cuando una persona experimenta estímulos emocionales, cognitivos o fisiológicos, el sistema nervioso simpático se activa, generando cambios en la sudoración y, por lo tanto, en la conductancia eléctrica de la piel. Estas variaciones pueden medirse mediante electrodos colocados sobre la superficie cutánea.

En esta práctica se diseñó y construyó un **dispositivo vestible capaz de medir variaciones de la GSR**, permitiendo estimar el nivel de estrés de un individuo mediante la adquisición de la señal y su visualización en un dispositivo móvil.

---

# Objetivos

## Objetivo general

Desarrollar un sistema vestible capaz de estimar el nivel de estrés de una persona mediante la medición de la respuesta galvánica cutánea.

## Objetivos específicos

- Diseñar un circuito seguro para la medición de la conductancia de la piel.
- Construir un dispositivo vestible para adquisición de la señal GSR.
- Analizar las variaciones de la señal en reposo y ante estímulos fisiológicos.
- Implementar un sistema de clasificación del nivel de estrés basado en umbrales de voltaje.

---

# Diseño del dispositivo vestible

El sistema fue diseñado para permitir la medición continua de la respuesta galvánica cutánea mientras el sujeto se encontraba en reposo o realizando tareas cognitivas.

## Ubicación de los electrodos

Los electrodos se colocaron sobre la **huella digital de los dedos índice y medio**, debido a que esta zona presenta una alta densidad de glándulas sudoríparas, lo que permite detectar con mayor sensibilidad los cambios en la conductancia de la piel.

## Implementación de los electrodos

Para la construcción de los electrodos se utilizaron materiales de fácil acceso:

- Monedas de **50 pesos colombianos**
- **Papel aluminio** para mejorar la conductividad
- **Velcro** para fijarlos a los dedos

Las monedas fueron recubiertas con papel aluminio para aumentar la superficie conductiva y mejorar el contacto con la piel.

---

# Arquitectura del sistema

El dispositivo vestible fue implementado utilizando los siguientes componentes:

- Protoboard
- Microcontrolador **ESP32**
- Powerbank como fuente de alimentación
- Resistencia de **68 kΩ**
- Capacitor de **1 µF**
- Electrodos conductivos

La **protoboard fue fijada a la muñeca del sujeto mediante velcro**, lo que permitió reducir el movimiento de los cables y mejorar la estabilidad de la señal.

La **powerbank se ubicó en el bolsillo del sujeto**, alimentando la ESP32 mediante cable USB.

---

# Circuito de medición

La medición de la respuesta galvánica cutánea se realizó mediante un **divisor de voltaje**, donde la resistencia fija y la resistencia de la piel determinan el voltaje de salida.

## Diagrama del circuito
  <img width="266" height="295" alt="image" src="https://github.com/user-attachments/assets/9106313f-53ca-46b1-a79d-50966197e91c" />



## Componentes

| Componente | Valor |
|---|---|
| Resistencia | 68 kΩ |
| Capacitor | 1 µF |
| Voltaje de alimentación | 3.3 V |

El capacitor se utiliza como **filtro para reducir ruido y estabilizar la señal fisiológica**.

---

# Cálculos del circuito

Uno de los requerimientos del diseño es garantizar que la corriente que atraviesa el cuerpo sea menor a **1 mA**.

## Corriente máxima

En el caso extremo se considera que la resistencia de la piel es aproximadamente **0 Ω**.

Ley de Ohm:
I = V / R ->
I = 3.3 / 68000 ->
I = 4.85 × 10⁻⁵ A ->
I = 0.0485 mA

Por lo tanto:
0.0485 mA < 1 mA

El circuito cumple con los requisitos de seguridad.

---

## Constante de tiempo del circuito RC
τ = R × C ->
τ = 68000 × 1×10⁻⁶ ->
τ = 0.068 s

Esto corresponde a **68 ms**, adecuado para señales fisiológicas lentas como la GSR.

---

# Adquisición de la señal

Inicialmente se realizaron pruebas utilizando **Arduino Uno** para validar el funcionamiento del circuito.

Posteriormente el sistema fue implementado con **ESP32**, lo que permitió transmitir los datos a un **celular Android**.

El dispositivo móvil mostraba el estado fisiológico del sujeto según **umbrales de voltaje previamente definidos**.

---

# Protocolo experimental

El experimento se realizó en dos fases.

## Fase 1 – Reposo

El sujeto permaneció relajado durante un periodo de tiempo para registrar la señal basal de la GSR.

## Fase 2 – Estímulo fisiológico

Posteriormente se solicitó al sujeto realizar una **respiración profunda**, lo cual activa el sistema nervioso simpático y produce un incremento en la conductancia de la piel.

---

# Clasificación del nivel de estrés

Los niveles de estrés fueron definidos mediante los siguientes umbrales:

| Voltaje | Nivel de estrés |
|---|---|
| < 0.25 V | Bajo |
| 0.25 – 0.35 V | Moderado |
| > 0.35 V | Alto |

Estos valores fueron utilizados para mostrar en el celular si el sujeto se encontraba o no en un estado de estrés.

---

# Análisis de resultados

El sistema desarrollado permitió detectar variaciones en la señal GSR asociadas con cambios fisiológicos del sujeto. Durante las pruebas se observó un incremento en la señal cuando el sujeto realizó una respiración profunda, lo cual confirma la relación entre la actividad del sistema nervioso simpático y la conductancia de la piel.

El dispositivo puede ser útil para el monitoreo de estrés en entornos como:

- Oficinas
- Aulas universitarias
- Hogares

Sin embargo, la señal también puede verse afectada por factores externos como:

- Movimiento del sujeto
- Temperatura ambiente
- Humedad de la piel

---

# Preguntas de discusión

## ¿Por qué una inspiración profunda aumenta la GSR?

La inspiración profunda activa el **sistema nervioso simpático**, lo que incrementa la actividad de las glándulas sudoríparas. Este aumento en la sudoración produce un incremento en la conductancia eléctrica de la piel, lo que se refleja como un aumento en la señal GSR.

---

## Ventajas y desventajas de utilizar GSR como indicador de estrés

### Ventajas

- Técnica no invasiva  
- Bajo costo de implementación  
- Sensible a cambios en el sistema nervioso autónomo  
- Fácil integración con microcontroladores  

### Desventajas

- Sensible a temperatura y movimiento  
- Variabilidad entre individuos  
- No mide estrés directamente sino respuestas fisiológicas asociadas  

---

# Conclusiones

Durante esta práctica se desarrolló un sistema vestible capaz de medir la respuesta galvánica cutánea utilizando un circuito basado en un divisor de voltaje. Los cálculos realizados garantizaron que la corriente que atraviesa el cuerpo se mantuviera dentro de los límites de seguridad.

Los resultados obtenidos evidencian que la GSR es una señal fisiológica útil para detectar cambios en la activación del sistema nervioso autónomo. Sin embargo, la interpretación de esta señal debe considerar factores externos que pueden influir en la medición.

En conclusión, la respuesta galvánica cutánea representa una herramienta prometedora para el monitoreo fisiológico del estrés, aunque su aplicación clínica requiere sistemas más robustos y métodos adicionales de análisis.

---

# Bibliografía

[1] Boucsein, W. *Electrodermal Activity*. Springer Science & Business Media, 2012.

[2] Loggia, M. L., Juneau, M., & Bushnell, C. M. (2011). Autonomic responses to heat pain: Heart rate, skin conductance, and their relation to verbal ratings and stimulus intensity. *Pain*, 152(3), 592–598.

[3] Breimhorst, M., Sandrock, S., Fechir, M., Hausenblas, N., Geber, C., & Birklein, F. (2011). Do intensity ratings and skin conductance responses reliably discriminate between different stimulus intensities in experimentally induced pain? *The Journal of Pain*, 12(1), 61–70.

[4] Figner, B., & Murphy, R. O. (2011). Using skin conductance in judgment and decision making research. En *A Handbook of Process Tracing Methods for Decision Research*. Psychology Press.
