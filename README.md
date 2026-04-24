# LABORATORIO-ENCUBADORA

LABORATORIO-ENCUBADORA
Integrantes 
- Shesly Colorado - 5600756
- Santiago Mora - 5600775
- Daniel Herrera - 5600588
-------
## Requisitos
Software:
- Arduino IDE
  
Hardware:
- ESP32
- Sensor de temperatura y humedad DHT22
- Pantalla OLED SSD1306 OLED Display
- Módulo HX711 (amplificador para celda de carga)
- Celda de carga 5kg (sensor de peso)
- Módulo de relé
- Bombillo (fuente de calor)
- Ventilador 5v
- Transformador M-502
- Puente de diodos
- Capacitor de 2200 µF / 25 V
- Regulador de voltaje LM7805
- Resistencias
- LEDs
----

# INTRODUCCIÓN

Las incubadoras neonatales son dispositivos biomédicos fundamentales en las unidades de cuidado intensivo neonatal, diseñados para proporcionar un ambiente controlado que simule las condiciones del vientre materno. Estos sistemas permiten regular variables críticas como la temperatura, la humedad y la ventilación, con el objetivo de garantizar la supervivencia y el desarrollo adecuado de los recién nacidos, especialmente aquellos prematuros o con bajo peso al nacer [1][2][3].

Uno de los factores más importantes en este tipo de sistemas es el control térmico. Los neonatos, particularmente los prematuros, presentan una limitada capacidad de termorregulación debido a su baja cantidad de grasa subcutánea y a la inmadurez de su sistema nervioso, lo que los hace altamente vulnerables a cambios de temperatura. Por esta razón, las incubadoras deben mantener un rango térmico controlado entre aproximadamente 36.5 °C y 37.5 °C, considerado óptimo para evitar complicaciones como hipotermia o hipertermia [4][5][6][7].

El presente proyecto aborda el diseño e implementación de un sistema de monitoreo de temperatura para una incubadora neonatal a escala, utilizando sensores electrónicos y plataformas de adquisición de datos. Este sistema permite medir, visualizar y analizar la temperatura en tiempo real, integrando herramientas de instrumentación biomédica como microcontroladores y software de procesamiento de señales [1][8].

Desde el punto de vista de la instrumentación biomédica, este desarrollo permite aplicar conceptos de adquisición de señales, sensores, procesamiento de datos y visualización, los cuales son esenciales en el diseño de dispositivos médicos. Además, contribuye a comprender la importancia del control preciso de variables fisiológicas en aplicaciones clínicas [9][10].

# OBJETIVOS

## Objetivo General
Reconocer la importancia de las incubadoras neonatales en la salud del neonato.

## Objetivos Específicos 
• Identificar las partes principales que componen una incubadora neonatal. 
• Desarrollar un sistema que emule el modo de operación de una incubadora neonatal. 
• Evaluar cómo impacta el control de variables como temperatura, humedad y flujo de aire en la salud del neonato.

# MARCO TEORICO

## 3.1 Incubadora Neonatal

Una incubadora neonatal es un dispositivo médico que proporciona un ambiente controlado de temperatura, humedad y aislamiento para recién nacidos, especialmente prematuros. Su función principal es mantener condiciones térmicas estables y proteger al neonato de factores externos que puedan comprometer su salud [3][11][2].

Estas incubadoras funcionan mediante sistemas de calefacción por convección, donde el aire es calentado y distribuido de manera uniforme dentro de la cámara, reduciendo la pérdida de calor del neonato [12][3].

## 3.2 Importancia del Control de Temperatura

El control de temperatura es crítico en neonatología, ya que los recién nacidos no pueden regular eficientemente su temperatura corporal. Un entorno térmico inadecuado puede generar aumento en el consumo de oxígeno, alteraciones metabólicas y riesgo de mortalidad. Por ello, se recomienda mantener la temperatura corporal del neonato entre 36.5 °C y 37.5 °C [13][14].

El concepto de ambiente térmico neutro se refiere a las condiciones en las cuales el neonato mantiene su temperatura corporal con un gasto mínimo de energía, lo cual es esencial para su desarrollo adecuado [6][10].

## 3.3 Sensore de Temperatura DHT22

El DHT22 (AM2302) es un sensor digital integrado de temperatura y humedad relativa que utiliza comunicación serial de un solo cable, entregando datos calibrados directamente sin necesidad de conversión analógica. Ofrece un rango de temperatura de -40 a 80 °C con precisión de ±0.5 °C (mejor que DHT11's ±2 °C), y humedad del 0 al 100% RH con ±2-5% de precisión, ideal para aplicaciones críticas como incubadoras neonatales [15].

Aunque su velocidad de muestreo máxima es de 0.5 Hz (una medición cada 2 segundos, menor que DHT11's 1 Hz), compensa con mayor estabilidad y resolución de 0.1 °C, siendo más confiable para monitoreo continuo de largo plazo. Integra un sensor capacitivo para humedad y termistor NTC para temperatura, con alimentación de 3.3-5V y bajo consumo (1-1.5 mA), perfecto para sistemas embebidos como ESP32 [15][16].

## 3.4 Conversión Analógica y Digital

Los sensores pueden clasificarse según el tipo de señal que generan:

Sensores analógicos (LM35): entregan un voltaje continuo proporcional a la variable medida. Sensores digitales (DHT22): entregan datos procesados en formato digital [12].

El ESP32 incorpora un convertidor analógico-digital (ADC) que permite transformar señales analógicas en valores digitales para su procesamiento.

## 3.5 Sistema de Monitoreo

El sistema desarrollado en este proyecto sigue una arquitectura básica de instrumentación biomédica:

Sensor → Adquisición (ESP32) → Procesamiento → Visualización (OLED)

Este flujo permite medir, analizar y representar la temperatura en tiempo real, facilitando la toma de decisiones en sistemas biomédicos.

# Materiales y Componentes

## 4.1 Hardware

Para el desarrollo del prototipo se utilizaron los siguientes componentes: ESP32 como unidad de adquisición y procesamiento, sensor DHT22 para medición de temperatura y humedad, pantalla OLED SSD1306 para visualización local, módulo HX711 con celda de carga para medición de peso de 5Kg, módulo de relés para el control del bombillo calefactor y ventilador, fuente de alimentación, cables de conexión y estructura física de la incubadora a escala.

## 4.2 Software

Se realizo un codigo en Arduino IDE para el sistema te control ON/OFF y para la configuración de los sensores usados.

El sistema fue diseñado para medir variables relevantes dentro de una incubadora neonatal a escala. El sensor DHT22 mide la temperatura y humedad interna, mientras que la celda de carga permite estimar el peso colocado sobre la plataforma. El ESP32 recibe estas señales, las procesa y muestra los valores en la pantalla OLED.

Además, el sistema incluye una etapa de actuación mediante relés (Control del sistema). El bombillo funciona como fuente de calor y el ventilador permite distribuir o reducir la temperatura interna. La lógica de control se basa en umbrales de temperatura: cuando la temperatura disminuye, se activa el bombillo; cuando la temperatura aumenta por encima del límite establecido, se activa el ventilador.

# SEGURIDAD

Durante el desarrollo del proyecto se deben tener en cuenta las siguientes medidas de seguridad:

Verificar los niveles de voltaje antes de energizar el circuito. No exceder los 5 V en los pines del ESP32 S3. Evitar cortocircuitos en la protoboard. Manipular correctamente los equipos electrónicos. Mantener ordenado el espacio de trabajo.

Estas recomendaciones son fundamentales para prevenir daños en los dispositivos y garantizar un desarrollo seguro de la práctica .

# Diseño del Sistema

Parte estructural: 



## 6.1 Sistema de fuente 
Sensor → ESP32 → OLED 
## 6.2 Distema de temperaturaa y peso 
Conexión del sensor Conexión de la OLED 
## 6.3 Funcionamiento 
## 6.3 Funcionamiento

El ESP32 recibe los datos del sensor DHT22 y del módulo HX711, los procesa y los muestra en la pantalla OLED.

El sistema implementa un control ON/OFF basado en umbrales de temperatura. Cuando la temperatura desciende por debajo del valor mínimo, se activa el bombillo como fuente de calor. Cuando la temperatura supera el valor máximo, se activa el ventilador para reducirla.

Adicionalmente, se implementó un sistema de visualización mediante LEDs para indicar el estado térmico del sistema:

- LED azul: temperatura menor a 36°C (riesgo de hipotermia)
- LED verde: temperatura entre 36°C y 37.5°C (rango adecuado)
- LED rojo: temperatura mayor a 37.5°C (riesgo de sobrecalentamiento)

Este sistema permite una interpretación rápida del estado de la incubadora sin necesidad de observar la pantalla OLED.

# Implementación 

## 7. Código Arduino Lectura del sensor Envío serial Visualización OLED

# Resultados

Durante las pruebas realizadas, el sistema registró temperaturas entre < 36°C y > 38°C. Se observó que el bombillo permitió incrementar la temperatura interna de la incubadora, mientras que el ventilador ayudó a disminuirla.

El sistema logró mantener la temperatura cercana al rango deseado (36.5°C - 37.5°C), presentando pequeñas oscilaciones debido al control ON/OFF implementado.

La celda de carga permitió medir el peso, aunque fue necesario realizar un proceso de calibración para mejorar la precisión de las mediciones.

# Análisis de Resultados
¿La temperatura es estable? ¿Hay ruido en la señal? ¿Qué tan preciso es el sensor? Comparación entre sensores (LM35 vs DHT22)

# Costos 
Lista de componentes con precio Costo total Comparación con incubadoras reales

# Limitaciones del Sistema

No es sistema real médico Falta control automático No mide otras variables (flujo, peso, etc.)

# Conclusiones

Qué aprendiste Qué funcionó Qué mejorarías

# Preguntas de Discusión
• Pregunta 1: ¿Qué otras variables (y por qué) además de las aquí mencionadas son críticas en el monitoreo neonatal?

Además de temperatura y humedad, son esenciales saturación de oxígeno (SpO2, para detectar hipoxia o cardiopatías, objetivo >90-95% post-nacimiento), frecuencia cardíaca (FC, ~120-160 lpm para estabilidad hemodinámica), presión arterial (PA), frecuencia respiratoria (FR ~40-60 rpm) y CO2 transcutáneo (TcPCO2, para ventilación no invasiva). Estas previenen hipoxia, acidosis y fallos cardiopulmonares en UCI neonatal [17].

• Pregunta 2: ¿Qué haría falta para convertir el sistema desarrollado en una incubadora neonatal real?

Se requiere control cerrado (servo-control PID con actuadores de calefacción/ventilación), cumplimiento IEC 60601-2-19 (precisión ±0.5°C, alarmas, ruido <60 dB(A), uniformidad térmica), materiales biocompatibles (sin VOCs), pruebas de seguridad eléctrica/biológica, esterilizabilidad, certificación FDA/INVIMA/CE y ensayos clínicos. Añadir redundancia en sensores, interfaz usuario y calibración anual [18].

• Pregunta 3: ¿Qué semejanzas hay entre una incubadora neonatal y una servo-cuna?

Ambas regulan temperatura (servo-control para neutral térmico), humedad y protegen neonatos prematuros de pérdida de calor, con calefacción radiante/convección y alarmas. Difieren en que incubadoras son cerradas (mejor aislamiento/humedad, primera semana), servo-cunas abiertas (acceso fácil para cuidados maternos) [19].

# Bibliografía
1. Bustamante, J. B. (2013, July). DISEÑO e IMPLEMENTACIÓN DE UN PROTOTIPO DE INCUBADORA NEONATAL EN CUMPLIMIENTO CON LA NORMA UNE-EN-60601-2-19. dspace.ups.edu.ec. https://dspace.ups.edu.ec/bitstream/123456789/5091/1/UPS-CT002691.pdf
2. Incubadora Neonatal: Funciones y Principios de Operación. (2023, July 27). Studocu. https://www.studocu.com/latam/document/universidad-nacional-experimental-del-magisterio-samuel-robinson/bioquimica/incubadora-neonatal-apuntes/65902438
3. Pardell, X. (n.d.). Incubadora Neonatal - Apuntes de Electromedicina. https://www.pardell.es/incubadora-neonatal.html
4. Ruiz, M. (2024, August 2). Importancia de la termorregulación en recién nacidos. https://hightech.leexmedical.com/termorregulacion-en-recien-nacidos
5. Investigación, R. (2021, April 20). Termorregulación en el recién nacido pretérmino: una revisión bibliográfica. ▷ RSI - Revista Sanitaria De Investigación. https://revistasanitariadeinvestigacion.com/termorregulacion-en-el-recien-nacido-pretermino-una-revision-bibliografica/
6. Zamorano-Jiménez, C. A., Cordero-González, G., Flores-Ortega, J., Baptista-González, H. A., & Fernández-Carrocera, L. A. (n.d.). Control térmico en el recién nacido pretérmino. https://www.scielo.org.mx/scielo.php?script=sci_arttext&pid=S0187-53372012000100007
7. Sac, E. S. (2025, January 25). Guía Completa de Todo Sobre la Incubadora Neonatal » Emergency Survival. Emergency Survival. https://survivalperu.com/guia-completa-sobre-la-incubadora-neonatal/
8. Dugarte, E., Dugarte, N., & Raimonid, V. (n.d.). Diseño de un control de temperatura inteligente para incubadoras de recién nacidos. https://ve.scielo.org/scielo.php?script=sci_arttext&pid=S0798-04772011000200005
9. Bioinstrumentación avanzada: Instrumentación & bioseñales. (n.d.). StudySmarter ES. https://www.studysmarter.es/resumenes/ingenieria/ingenieria-biomedica/bioinstrumentacion-avanzada/
10. Tapia, V. B., Victoria, V. T., Medina, J. M. R., Mendoza, G. R. P., & Zenil, M. S. C. (2023). Sistema de transferencia de datos biomédicos con protocolos de comunicación de bajo consumo. Revista De Ciencias Tecnológicas, 6(4), e284. https://doi.org/10.37636/recit.v6n4e284
11. Team, K. (2023, May 11). ¿Cómo funciona una incubadora neonatal? Kalstein. https://kalstein.co.cr/como-funciona-una-incubadora-neonatal/
12. Perez, M. D. (n.d.). Incubadora. Scribd. https://es.scribd.com/document/345556833/Incubadora
13. De Aquino, A. R. G., Da Silva, B. C. O., Barreto, V. P., De Aquino, A. R. G., Trigueiro, E. V., & Feijão, A. R. (2021). Perfil de recém-nascidos de risco relacionado à termorregulação em Unidade de Terapia Intensiva Neonatal. Enfermería Global, 20(1), 59–97. https://doi.org/10.6018/eglobal.414201
14. Vygon, C., & Vygon, C. (2025, September 29). Hipotermia en recién nacidos, ¿cómo prevenirla? Campus Vygon España. https://campusvygon.com/es/hipotermia-rn/
15. Tutorial sensor de temperatura y humedad DHT11 y DHT22. (n.d.). Naylamp Mechatronics - Perú. https://naylampmechatronics.com/blog/40_tutorial-sensor-de-temperatura-y-humedad-dht11-y-dht22.html
16. He, S. (2025, January 20). DHT11 vs DHT22 Sensor Temperature and Humidity tutorial. PCBMay. https://www.pcbmay.com/es/dht11-frente-a-dht22/
17. Medición de la saturación de oxígeno durante la recepción neonatal, con el fin de establecer parámetros estándar de saturación en el Hospital Gineco Obstétrico Luz Elena Arismendi (2018:Quito). (2018). docs.bvsalud.org. Retrieved April 23, 2026, from https://docs.bvsalud.org/biblioref/2019/08/1010310/revista-pediatria-vfinal-18-22.pdf
18. Denetim. (n.d.). TS EN 60601-2-19 Equipo médico eléctrico - Parte 2-19: Características específicas para la seguridad básica y el rendimiento requerido de las incubadoras de bebés. https://www.denetim.com/es/laboratuvar/medikal-cihaz-testleri/ts-en-60601-2-19-elektrikli-tibbi-donanim-bolum-2-19-bebek-kuvozlerinin-temel-guvenligi-ve-gerekli-performansi-icin-belirli-ozellikler/
19. Cochrane. (2025). Atención en la cuna versus atención en incubadora para niños prematuros. Cochrane. https://www.cochrane.org/es/evidence/CD003062_cot-nursing-versus-incubator-care-preterm-infants
