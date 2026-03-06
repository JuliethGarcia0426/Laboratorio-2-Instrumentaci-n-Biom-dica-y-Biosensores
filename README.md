
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

## 1. ¿Por qué una inspiración profunda produce un aumento en la señal de GSR?

La inspiración profunda genera una activación del sistema nervioso autónomo, específicamente del sistema nervioso simpático. Este sistema es responsable de preparar al organismo para responder ante estímulos fisiológicos o emocionales, regulando funciones como la frecuencia cardíaca, la presión arterial y la actividad de las glándulas sudoríparas.

Cuando se produce esta activación simpática, las glándulas sudoríparas ecrinas aumentan su actividad, especialmente en regiones como las palmas de las manos y las yemas de los dedos, donde existe una alta densidad de estas glándulas. El incremento en la secreción de sudor modifica las propiedades eléctricas de la piel, aumentando su conductancia eléctrica y disminuyendo su resistencia.

Como consecuencia, en el circuito de medición se produce una variación en el divisor de voltaje, lo que se traduce en un cambio en el voltaje de salida medido por el microcontrolador. Este cambio es detectado por el sistema como una variación en la respuesta galvánica cutánea, reflejando el estado de activación fisiológica del sujeto.

Por esta razón, estímulos como la respiración profunda, el estrés, la atención o la carga cognitiva pueden generar incrementos medibles en la señal de GSR.

---

## 2. ¿Cuáles son las ventajas y limitaciones de utilizar la respuesta galvánica cutánea como indicador de estrés?

La respuesta galvánica cutánea es una de las señales fisiológicas más utilizadas en estudios de psicofisiología debido a que proporciona información indirecta sobre la actividad del sistema nervioso simpático. Una de sus principales ventajas es que se trata de una técnica no invasiva, de bajo costo y relativamente sencilla de implementar mediante sensores y microcontroladores. Esto permite desarrollar dispositivos portátiles o vestibles capaces de monitorear el estado fisiológico de una persona en tiempo real.

Otra ventaja importante es su alta sensibilidad ante cambios emocionales o cognitivos. La GSR puede responder rápidamente a estímulos relacionados con estrés, miedo, atención o carga mental, lo que la convierte en una herramienta útil para aplicaciones como monitoreo del estrés, investigación en neurociencia o interfaces humano-máquina.

Sin embargo, esta técnica también presenta algunas limitaciones. La señal puede verse afectada por múltiples factores externos, como la temperatura ambiente, la humedad de la piel, el movimiento del sujeto o incluso diferencias fisiológicas entre individuos. Además, la GSR no mide el estrés de manera directa, sino que detecta cambios en la actividad del sistema nervioso simpático, por lo que es necesario interpretar los resultados con cautela y, en muchos casos, complementarlos con otras señales fisiológicas como frecuencia cardíaca o respiración.

Por estas razones, aunque la GSR es una herramienta valiosa para la evaluación fisiológica del estrés, su uso requiere un adecuado procesamiento de señal y un análisis contextual de los datos obtenidos.

---

## 3. ¿Qué aspectos del diseño del dispositivo podrían mejorarse para aplicaciones clínicas o de monitoreo continuo?

Aunque el sistema desarrollado cumple con el objetivo de medir variaciones en la respuesta galvánica cutánea, existen varios aspectos que podrían mejorarse para su uso en aplicaciones clínicas o de monitoreo prolongado.

En primer lugar, el diseño de los electrodos podría optimizarse utilizando materiales biomédicos específicos, como electrodos de Ag/AgCl, los cuales ofrecen una mejor estabilidad electroquímica y reducen el ruido en la señal. Esto permitiría obtener mediciones más confiables y reproducibles.

En segundo lugar, el sistema podría incorporar un acondicionamiento de señal más avanzado, incluyendo amplificadores operacionales, filtros analógicos o técnicas de procesamiento digital para mejorar la relación señal-ruido. Esto es especialmente importante en señales fisiológicas de baja amplitud como la GSR.

Finalmente, desde el punto de vista del diseño vestible, se podrían desarrollar sensores integrados en guantes, bandas o dispositivos tipo smartwatch que mejoren la ergonomía y reduzcan el movimiento de los electrodos. También sería posible implementar algoritmos de análisis más sofisticados o técnicas de aprendizaje automático para clasificar de manera más precisa los niveles de estrés.

Estas mejoras permitirían que el sistema evolucione desde un prototipo experimental hacia una herramienta más robusta para aplicaciones biomédicas o de monitoreo fisiológico en tiempo real.

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
