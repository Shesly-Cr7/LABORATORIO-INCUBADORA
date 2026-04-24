# LABORATORIO-INCUBADORA

LABORATORIO-INCUBADORA
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

----------

# 1. INTRODUCCIÓN

Las incubadoras neonatales son dispositivos biomédicos fundamentales en las unidades de cuidado intensivo neonatal, diseñados para proporcionar un ambiente controlado que simule las condiciones del vientre materno. Estos sistemas permiten regular variables críticas como la temperatura, la humedad y la ventilación, con el objetivo de garantizar la supervivencia y el desarrollo adecuado de los recién nacidos, especialmente aquellos prematuros o con bajo peso al nacer [1][2][3].

Uno de los factores más importantes en este tipo de sistemas es el control térmico. Los neonatos, particularmente los prematuros, presentan una limitada capacidad de termorregulación debido a su baja cantidad de grasa subcutánea y a la inmadurez de su sistema nervioso, lo que los hace altamente vulnerables a cambios de temperatura. Por esta razón, las incubadoras deben mantener un rango térmico controlado entre aproximadamente 36.5 °C y 37.5 °C, considerado óptimo para evitar complicaciones como hipotermia o hipertermia [4][5][6][7].

El presente proyecto aborda el diseño e implementación de un sistema de monitoreo de temperatura para una incubadora neonatal a escala, utilizando sensores electrónicos y plataformas de adquisición de datos. Este sistema permite medir y visualizar la temperatura en tiempo real, integrando herramientas de instrumentación biomédica como microcontroladores y software de procesamiento de señales [1][8].

Desde el punto de vista de la instrumentación biomédica, este desarrollo permite aplicar conceptos de adquisición de señales, sensores, procesamiento de datos y visualización, los cuales son esenciales en el diseño de dispositivos médicos. Además, contribuye a comprender la importancia del control preciso de variables fisiológicas en aplicaciones clínicas [9][10].

----------

# 2. OBJETIVOS

## Objetivo General
Reconocer la importancia de las incubadoras neonatales en la salud del neonato.

## Objetivos Específicos 
• Identificar las partes principales que componen una incubadora neonatal. 
• Desarrollar un sistema que emule el modo de operación de una incubadora neonatal. 
• Evaluar cómo impacta el control de variables como temperatura, humedad y flujo de aire en la salud del neonato.

----------

# 3. MARCO TEORICO

## 3.1 Incubadora Neonatal

Una incubadora neonatal es un dispositivo médico que proporciona un ambiente controlado de temperatura, humedad y aislamiento para recién nacidos, especialmente prematuros. Su función principal es mantener condiciones térmicas estables y proteger al neonato de factores externos que puedan comprometer su salud [3][11][2].

Estas incubadoras funcionan mediante sistemas de calefacción por convección, donde el aire es calentado y distribuido de manera uniforme dentro de la cámara, reduciendo la pérdida de calor del neonato [12][3].

## 3.2 Importancia del Control de Temperatura

El control de temperatura es crítico en neonatología, ya que los recién nacidos no pueden regular eficientemente su temperatura corporal. Un entorno térmico inadecuado puede generar aumento en el consumo de oxígeno, alteraciones metabólicas y riesgo de mortalidad. Por ello, se recomienda mantener la temperatura corporal del neonato entre 36.5 °C y 37.5 °C [13][14].

El concepto de ambiente térmico neutro se refiere a las condiciones en las cuales el neonato mantiene su temperatura corporal con un gasto mínimo de energía, lo cual es esencial para su desarrollo adecuado [6][10].

## 3.3 Sensores de Temperatura DHT22

El DHT22 (AM2302) es un sensor digital integrado de temperatura y humedad relativa que utiliza comunicación serial de un solo cable, entregando datos calibrados directamente sin necesidad de conversión analógica. Ofrece un rango de temperatura de -40 a 80 °C con precisión de ±0.5 °C (mejor que DHT11's ±2 °C), y humedad del 0 al 100% RH con ±2-5% de precisión, ideal para aplicaciones críticas como incubadoras neonatales [15].

Aunque su velocidad de muestreo máxima es de 0.5 Hz (una medición cada 2 segundos, menor que DHT11's 1 Hz), compensa con mayor estabilidad y resolución de 0.1 °C, siendo más confiable para monitoreo continuo de largo plazo. Integra un sensor capacitivo para humedad y termistor NTC para temperatura, con alimentación de 3.3-5V y bajo consumo (1-1.5 mA), perfecto para sistemas embebidos como ESP32 [15][16].

## 3.4 Conversión Analógica y Digital

Los sensores pueden clasificarse según el tipo de señal que generan:

Sensores analógicos (LM35): entregan un voltaje continuo proporcional a la variable medida. Sensores digitales (DHT22): entregan datos procesados en formato digital [12].

El ESP32 incorpora un convertidor analógico-digital (ADC) que permite transformar señales analógicas en valores digitales para su procesamiento.

## 3.5 Sistema de Monitoreo

El sistema desarrollado en este proyecto sigue una arquitectura básica de instrumentación biomédica:

Sensor → Adquisición → Procesamiento → Actuación → Visualización(OLED)

Este flujo permite medir, analizar y representar la temperatura en tiempo real, facilitando la toma de decisiones en sistemas biomédicos.

## 3.6 Comparación de estrategias de control

En el control de temperatura de incubadoras existen diferentes estrategias, entre las cuales destacan el control ON/OFF y el control proporcional.
El control ON/OFF, implementado en este proyecto, funciona mediante la activación o desactivación completa del actuador (bombillo) cuando la temperatura cruza ciertos umbrales. Este tipo de control es sencillo, pero genera oscilaciones alrededor del valor deseado, como se observó en el comportamiento del sistema.
Por otro lado, el control proporcional, comúnmente implementado mediante modulación por ancho de pulso (PWM), permite regular la potencia del actuador de forma gradual. En este caso, el sistema no solo enciende o apaga el bombillo, sino que ajusta la cantidad de energía suministrada según el error de temperatura.
Esto produce una respuesta más suave y reduce las oscilaciones, permitiendo mantener la temperatura más cercana al valor de referencia.
En comparación, el sistema desarrollado utiliza un control ON/OFF debido a su simplicidad y facilidad de implementación, siendo adecuado para fines académicos. Sin embargo, un control proporcional o PID sería más apropiado para aplicaciones reales en incubadoras neonatales.[20][21]

----------

# 4. Materiales y Componentes

## 4.1 Hardware

Para el desarrollo del prototipo se utilizaron los siguientes componentes: ESP32 como unidad de adquisición y procesamiento, sensor DHT22 para medición de temperatura y humedad, pantalla OLED SSD1306 para visualización local, módulo HX711 con celda de carga para medición de peso de 5Kg, módulo de relés para el control del bombillo calefactor y ventilador, fuente de alimentación, cables de conexión y estructura física de la incubadora a escala.

## 4.2 Software

Se realizó un código en Arduino IDE para el sistema de control ON/OFF y para la configuración de los sensores usados.

El sistema fue diseñado para medir variables relevantes dentro de una incubadora neonatal a escala. El sensor DHT22 mide la temperatura y humedad interna, mientras que la celda de carga permite estimar el peso colocado sobre la plataforma. El ESP32 recibe estas señales, las procesa y muestra los valores en la pantalla OLED.

Además, el sistema incluye una etapa de actuación mediante relés (Control del sistema). El bombillo funciona como fuente de calor y el ventilador permite distribuir o reducir la temperatura interna. La lógica de control se basa en umbrales de temperatura: cuando la temperatura disminuye, se activa el bombillo; cuando la temperatura aumenta por encima del límite establecido, se activa el ventilador.

----------

# 5. SEGURIDAD

Durante el desarrollo del proyecto se deben tener en cuenta las siguientes medidas de seguridad:

Verificar los niveles de voltaje antes de energizar el circuito. No exceder los 3.3 V en los pines del ESP32. Evitar cortocircuitos en la protoboard. Manipular correctamente los equipos electrónicos. Mantener ordenado el espacio de trabajo.

Estas recomendaciones son fundamentales para prevenir daños en los dispositivos y garantizar un desarrollo seguro de la práctica.

----------

# 6. Diseño del Sistema


## 6.1 Parte estructural

El diseño del sistema se realizó dividiendo el prototipo en **dos módulos principales**: una **cabina de incubación** y un **módulo lateral de control y electrónica**. Esta distribución permitió separar la zona donde se encuentra el espacio interno de la incubadora de la zona donde están ubicados la mayor parte del circuito, la alimentación y los elementos de visualización y control.

### 6.1.1 Cabina principal de incubación


<img width="800" height="450" alt="PHOTO-2026-04-23-09-32-01" src="https://github.com/user-attachments/assets/a104d7ea-a414-4e3d-9d09-5832b46efa79" />

La cabina principal corresponde a la estructura donde se simula el espacio interno de la incubadora neonatal. Esta parte está compuesta por una **cúpula transparente de plástico**, la cual permite observar el interior del sistema sin necesidad de abrirlo completamente. El uso de un material transparente fue importante porque facilita la supervisión visual del prototipo y ayuda a representar la idea de una incubadora real, donde es necesario mantener visibilidad sobre el neonato.

En la parte frontal de esta cúpula se construyó una **puerta de acceso principal** con marco negro, bisagras inferiores y manija, lo que permite abrir y cerrar la incubadora de manera sencilla para introducir o retirar elementos del interior. Esta puerta también facilita el mantenimiento y la revisión del sistema.

Además, en la parte superior inclinada de la cabina se observan **dos compuertas o ventanas de acceso**, también con marco y manija, que permiten una manipulación más localizada del interior sin necesidad de abrir completamente la puerta frontal. Estas aberturas ayudan a que el diseño sea más funcional y se asemeje más a la idea general de una incubadora con accesos parciales.


### 6.1.2 Base estructural
<img width="800" height="450" alt="PHOTO-2026-04-23-09-31-26" src="https://github.com/user-attachments/assets/07335bb1-0417-44f5-a817-940dc10c4bed" />

La cúpula se encuentra apoyada sobre una **base fabricada en cartón madera**, la cual sirve como soporte mecánico principal del sistema. Esta base cumple varias funciones importantes:

- sostener la estructura transparente de la incubadora,
- proporcionar estabilidad al prototipo,
- alojar internamente elementos como el bombillo,
- servir como superficie donde se ubica el espacio de apoyo del “bebé” o carga de prueba,
- integrar la **galga o celda de carga**, utilizada para la medición del peso.

El uso de cartón madera permitió construir una base rígida, económica y relativamente fácil de trabajar, lo cual fue adecuado para el desarrollo del laboratorio. Esta parte del sistema cumple entonces una función tanto **estructural** como **funcional**, ya que no solo sostiene la cabina, sino que también forma parte del montaje de medición y calentamiento.

### 6.1.3 Módulo lateral de electrónica y control

<img width="800" height="450" alt="PHOTO-2026-04-23-09-33-20" src="https://github.com/user-attachments/assets/070fbe35-4ca8-4fd7-a094-09d1b2b000f8" />

A un costado de la incubadora se ubicó una **caja de cartón independiente**, destinada a alojar la mayor parte del sistema electrónico. En esta caja se encuentran el circuito, el transformador, conexiones y otros elementos del sistema de control. Esta decisión de diseño fue útil porque permitió **separar físicamente la electrónica del interior de la incubadora**, reduciendo la exposición directa de los componentes al calor generado dentro de la cabina.

En la cara frontal de esta caja lateral se instaló una pequeña **interfaz de usuario**, compuesta por:

- una **pantalla OLED** para visualizar las variables del sistema,
- un **botón** de accionamiento,
- tres **LEDs indicadores**: azul, verde y rojo.

Esta disposición permite consultar el estado del prototipo desde el exterior de forma rápida y cómoda, sin intervenir directamente en la cabina principal.

### 6.1.4 Distribución funcional del sistema

Desde el punto de vista físico, el diseño del sistema quedó organizado de forma que cada módulo cumpliera una tarea específica:

- **Cabina transparente:** contiene el ambiente interno de incubación.
- **Base de cartón madera:** soporta la estructura y aloja elementos mecánicos y funcionales como la galga y la zona de apoyo. Además de contener el ventilador y el bombillo para el calor
- **Caja lateral de cartón:** contiene gran parte de la electrónica, alimentación y visualización.

Esta separación mejora la organización del prototipo, facilita el montaje y permite identificar con mayor claridad qué parte del sistema corresponde a la estructura mecánica y cuál corresponde al control electrónico.

### 6.1.5 Consideraciones del diseño estructural

El diseño construido priorizó aspectos como la **visibilidad**, la **facilidad de acceso**, la **distribución ordenada de componentes** y la **separación entre la zona térmica y la zona electrónica**. Aunque se trata de un prototipo académico y no de un equipo clínico real, la estructura desarrollada permite representar de forma clara el funcionamiento general de una incubadora neonatal a escala.

En conjunto, la parte estructural del sistema logró integrar una cabina visible, una base de soporte resistente y un módulo externo de control, permitiendo que el prototipo fuera funcional, entendible visualmente y adecuado para la implementación del laboratorio.

## 6.2 Funcionamiento

El ESP32 recibe los datos del sensor DHT22 y del módulo HX711, los procesa y los muestra en la pantalla OLED.

El sistema implementa un control ON/OFF basado en umbrales de temperatura. Cuando la temperatura desciende por debajo del valor mínimo, se activa el bombillo como fuente de calor. Cuando la temperatura supera el valor máximo, se activa el ventilador para reducirla.

Adicionalmente, se implementó un sistema de visualización mediante LEDs para indicar el estado térmico del sistema:

- LED azul: temperatura menor a 36°C (riesgo de hipotermia)
- LED verde: temperatura entre 36°C y 37.5°C (rango adecuado)
- LED rojo: temperatura mayor a 37.5°C (riesgo de sobrecalentamiento)

Este sistema permite una interpretación rápida del estado de la incubadora sin necesidad de observar la pantalla OLED.

----------

# 7. Implementación

## 7.1 Descripción general del sistema

La implementación del prototipo se realizó en **Arduino IDE** utilizando un **ESP32** como unidad principal de control. El sistema fue diseñado para monitorear variables importantes dentro de una incubadora neonatal a escala, específicamente **temperatura, humedad y peso**, y actuar sobre ellas mediante un sistema de control térmico simple.

Para ello se integraron los siguientes elementos:

- **Sensor DHT22**, encargado de medir la temperatura y la humedad interna.
- **Galga o celda de carga de 5 kg**, utilizada para estimar el peso colocado sobre la base.
- **Módulo HX711**, que amplifica y convierte la señal de la galga de carga en una lectura interpretable por el ESP32.
- **Pantalla OLED SSD1306**, donde se visualizan los valores medidos.
- **Dos relés**, uno para controlar el bombillo y otro para controlar el ventilador.
- **Tres LEDs**, usados como señalización visual rápida del estado térmico del sistema.
- **Botón de tara**, que permite reiniciar la referencia de peso cuando no hay carga sobre la plataforma.

En términos generales, el sistema funciona así: el ESP32 lee la temperatura y la humedad desde el DHT22, lee el peso desde la galga de carga con ayuda del HX711, muestra estos datos en la pantalla OLED y, dependiendo de la temperatura medida, activa el bombillo o el ventilador. Adicionalmente, enciende un LED de color diferente para indicar si la temperatura está baja, normal o alta.

---

## 7.2 Configuración inicial del programa

La primera parte importante del código corresponde a la importación de librerías y a la definición de pines. Esta etapa es importante porque establece la comunicación entre el ESP32 y cada módulo del sistema.

```cpp
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <DHT.h>
#include "HX711.h"
```
Estas librerías permiten manejar la pantalla OLED, leer el sensor DHT22 y adquirir los datos de la galga de carga mediante el módulo HX711.

Después de esto, se definen los pines utilizados:
```cpp
#define DHTPIN 41
#define DHTTYPE DHT22

#define SDA_OLED 8
#define SCL_OLED 9

#define RELAY_K1 14   // Bombillo
#define RELAY_K2 15   // Ventilador

#define LED_BAJA 16
#define LED_OK 17
#define LED_ALTA 18

#define HX_DT 11
#define HX_SCK 12
#define BOTON_TARA 10
```

Aquí se observa cómo quedó distribuido el sistema:

- El DHT22 se conecta al pin 41.
- La pantalla OLED usa comunicación I2C.
- El relé K1 controla el bombillo.
- El relé K2 controla el ventilador.
- Los tres LEDs indican el estado de temperatura.
- El HX711 se comunica con el ESP32 por dos pines digitales.
- El botón de tara permite recalibrar la lectura del peso.

## 7.3 Inicialización de variables y objetos principales

Una vez definidos los pines, el código crea los objetos necesarios para trabajar con cada dispositivo y declara las variables principales del sistema:

```cpp
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);
DHT dht(DHTPIN, DHTTYPE);
HX711 balanza;

float T_OFF = 37.5;
float T_ON = 36.0;

float peso = 0.0;
float pesoFiltrado = 0.0;
float factor_calibracion = 286.0;

float temperatura = 0.0;
float humedad = 0.0;

bool sistemaCalentando = true;
```

Aquí aparecen dos umbrales importantes:

- T_ON = 36.0 °C, umbral inferior.
- T_OFF = 37.5 °C, umbral superior.

Estos dos valores son la base del control térmico. Cuando la temperatura baja del umbral inferior, el sistema enciende el bombillo para calentar. Cuando la temperatura llega al umbral superior, el bombillo se apaga y el ventilador puede activarse para ayudar a enfriar.

También se define un factor de calibración para la galga de carga, ya que el HX711 no entrega el peso directamente en gramos, sino una señal que debe ajustarse experimentalmente

## 7.4 Inicialización del hardware en setup()

La función setup() se ejecuta una sola vez al encender el sistema. Su objetivo es dejar todos los módulos listos para funcionar correctamente.

```cpp
void setup() {
  Serial.begin(115200);

  pinMode(RELAY_K1, OUTPUT);
  pinMode(RELAY_K2, OUTPUT);
  pinMode(LED_BAJA, OUTPUT);
  pinMode(LED_OK, OUTPUT);
  pinMode(LED_ALTA, OUTPUT);
  pinMode(BOTON_TARA, INPUT_PULLUP);

  dht.begin();
  Wire.begin(SDA_OLED, SCL_OLED);

  if (!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println("OLED no detectada");
    while (true);
  }

  balanza.begin(HX_DT, HX_SCK);
  balanza.set_scale(factor_calibracion);
  delay(1500);
  balanza.tare(10);

  display.clearDisplay();
  display.setCursor(0, 20);
  display.println("Sistema listo");
  display.display();
  delay(1000);
}
```

En esta etapa se realizan varias acciones:

1. Se inicia la comunicación serial.
2. Se configuran como salida los pines de relés y LEDs.
3. Se configura el botón de tara con resistencia pull-up interna.
4. Se inicializa el sensor DHT22.
5. Se inicializa la pantalla OLED.
6. Se verifica si la OLED fue detectada correctamente.
7. Se inicializa el módulo HX711.
8. Se aplica el factor de calibración.
9. Se realiza una tara inicial para que la lectura de peso comience desde cero.
10. Se muestra en pantalla el mensaje “Sistema listo”.

Esta parte es importante porque garantiza que el sistema arranque en condiciones conocidas y no con valores erróneos.


## 7.5 Lectura de temperatura y humedad con el DHT22

La medición de temperatura y humedad se realiza mediante el sensor **DHT22**, el cual se encarga de entregar ambas variables en formato digital. Estas dos magnitudes son importantes dentro del prototipo, ya que permiten conocer el estado interno de la incubadora a escala y, especialmente en el caso de la temperatura, tomar decisiones de control sobre el bombillo y el ventilador.

En el programa, la lectura del sensor se implementó a través de una función específica:

```cpp
void leerDHT() {
  float t = dht.readTemperature();
  float h = dht.readHumidity();

  if (!isnan(t)) temperatura = t;
  if (!isnan(h)) humedad = h;
}
```

Esta función realiza primero la adquisición de la temperatura y la humedad, almacenándolas temporalmente en las variables t y h. Posteriormente, el programa verifica que los datos obtenidos sean válidos mediante la condición !isnan(...). Esto evita que una lectura errónea o incompleta reemplace el último valor correcto guardado en el sistema.

La variable más importante en esta etapa es la temperatura, ya que a partir de ella se define si el sistema debe activar el bombillo para calentar o el ventilador para enfriar. La humedad también se registra y se muestra al usuario, lo que permite tener una visión más completa del comportamiento interno de la incubadora.

De esta manera, el DHT22 actúa como el sensor principal de monitoreo ambiental del prototipo, entregando la información básica necesaria para supervisar el funcionamiento del sistema en tiempo real.


## 7.6 Medición de peso, visualización y funcionamiento general del sistema

Además de la lectura de temperatura y humedad, el sistema integra una **galga o celda de carga de 5 kg** conectada al módulo **HX711**, una **pantalla OLED** para mostrar las variables medidas, un **botón de tara** para reiniciar la referencia del peso y un sistema de **LEDs de estado** para indicar de forma rápida la condición térmica interna del prototipo. :contentReference[oaicite:2]{index=2}

La lectura del peso se realiza con el HX711, que toma la señal de la galga y la convierte en un valor que puede ser procesado por el ESP32. En el código se implementó un pequeño filtrado para suavizar la medición y evitar cambios bruscos por ruido o vibraciones:

```cpp
void leerPeso() {
  if (balanza.is_ready()) {
    float lectura = balanza.get_units(5);
    pesoFiltrado = 0.7 * pesoFiltrado + 0.3 * lectura;

    if (pesoFiltrado > -2.0 && pesoFiltrado < 2.0) {
      pesoFiltrado = 0.0;
    }

    peso = pesoFiltrado;
  }
}
```
Este filtrado hace que la lectura mostrada sea más estable. Además, si el valor está muy cerca de cero, el sistema lo ajusta a cero para evitar errores pequeños cuando no hay carga sobre la base.

Por otra parte, el prototipo cuenta con una función de tara, activada mediante un botón, que permite recalibrar la lectura del peso cuando la plataforma está vacía. Esto mejora la precisión de la medición durante el uso del sistema.

Las variables principales del prototipo se muestran continuamente en la pantalla OLED: temperatura, humedad y peso. Esto permite que el usuario observe en tiempo real el comportamiento general de la incubadora.

```cpp

void mostrarOLED() {
  display.clearDisplay();
  display.setTextColor(SSD1306_WHITE);
  display.setTextSize(1);

  display.setCursor(0, 0);
  display.println("Incubadora");

  display.setCursor(0, 12);
  display.print("Temp: ");
  display.print(temperatura, 1);
  display.println(" C");

  display.setCursor(0, 24);
  display.print("Hum : ");
  display.print(humedad, 1);
  display.println(" %");

  display.setCursor(0, 36);
  display.print("Peso: ");
  display.print(peso, 1);
  display.println(" g");

  display.display();
}
```
Como apoyo visual adicional, se implementó un sistema de tres LEDs para indicar rápidamente el estado térmico del prototipo:

- LED azul: temperatura baja
- LED verde: temperatura normal
- LED rojo: temperatura alta

Esta señalización permite interpretar de forma inmediata si la incubadora se encuentra por debajo, dentro o por encima del rango de funcionamiento esperado, sin necesidad de revisar únicamente la pantalla. Esa misma lógica de colores ya se describe en el borrador del proyecto.

Finalmente, todas las tareas del sistema se coordinan dentro del ciclo principal del programa. Allí se revisa el botón de tara, se leen los sensores, se actualiza la lógica de control, se encienden los LEDs correspondientes y se refresca la información mostrada en la OLED. En conjunto, esta etapa permite que el prototipo no solo mida variables, sino que también las procese, las muestre al usuario y actúe de acuerdo con el estado térmico interno de la incubadora

----------

# 8. Resultados


https://github.com/user-attachments/assets/d5ade555-2d3d-4e32-bd55-be28e650f263


Durante las pruebas realizadas, el sistema permitió registrar y visualizar en tiempo real las variables de temperatura, humedad y peso dentro del prototipo de incubadora neonatal a escala. La pantalla OLED mostró de forma continua estos valores, lo que facilitó la supervisión del comportamiento interno del sistema.

En términos de temperatura, se observó que el bombillo actuó correctamente como fuente de calor, incrementando la temperatura cuando esta descendía por debajo del umbral inferior (36 °C). De igual forma, el ventilador respondió adecuadamente al activarse cuando la temperatura superó el límite superior (37.5 °C), contribuyendo a su reducción.

El sistema de señalización mediante LEDs también funcionó correctamente, permitiendo identificar de manera inmediata el estado térmico: el LED azul indicó temperaturas bajas, el LED verde el rango adecuado y el LED rojo temperaturas elevadas. Esta representación visual complementó la información mostrada en la pantalla.

Respecto a la medición de peso, la celda de carga junto con el módulo HX711 permitió obtener lecturas funcionales del peso aplicado sobre la base. Aunque fue necesario un proceso de calibración, el sistema logró mostrar valores estables durante las pruebas.

En general, el prototipo logró representar de manera adecuada el funcionamiento básico de una incubadora neonatal, integrando medición, visualización y actuación en un mismo sistema.

# 9. Análisis de Resultados

Aunque el prototipo desarrollado cumplió con el objetivo académico de emular el funcionamiento básico de una incubadora neonatal a escala, el sistema presenta varias limitaciones importantes.

La principal limitación está en el tipo de control implementado. En este proyecto se utilizó un control **ON/OFF**, es decir, el bombillo se enciende completamente cuando la temperatura baja del límite definido y se apaga cuando alcanza el valor superior. Este método es sencillo, económico y fácil de programar, por lo que resulta muy útil en un prototipo de laboratorio. Sin embargo, su desventaja es que **no regula la potencia de manera gradual**, sino por cambios bruscos entre encendido y apagado. Por esta razón, la temperatura tiende a presentar pequeñas oscilaciones alrededor del rango deseado, en lugar de mantenerse completamente estable [8].

En comparación, una estrategia basada en **PWM (modulación por ancho de pulso)** permitiría controlar la cantidad de energía entregada al sistema de forma más progresiva. En vez de trabajar solo en dos estados, encendido o apagado, el actuador podría operar con distintos niveles de potencia promedio, lo que ayudaría a suavizar la respuesta térmica y a reducir las variaciones de temperatura. En otras palabras, mientras el control ON/OFF es más simple pero más brusco, el PWM ofrece una regulación más fina y eficiente. Aun así, para este laboratorio el control ON/OFF fue suficiente porque permitió demostrar claramente el principio de funcionamiento del sistema.

Otra limitación importante es que **no se trata de un dispositivo médico real**, sino de un montaje experimental con fines académicos. Por esta razón, no cuenta con certificaciones clínicas, alarmas de seguridad, materiales biomédicos especializados ni condiciones de validación equivalentes a las exigidas en una incubadora neonatal hospitalaria [18].

Además, aunque el sistema sí mide **temperatura, humedad y peso**, todavía **no incorpora otras variables críticas del monitoreo neonatal**, como saturación de oxígeno, frecuencia cardíaca, frecuencia respiratoria, concentración de CO₂ o un control más preciso del flujo de aire. Estas variables serían necesarias para acercar el prototipo a una incubadora neonatal más completa [17][18].

Finalmente, tanto la medición del peso como la de temperatura dependen de la calibración y de las características de los sensores empleados. La galga de carga de 5 kg y el DHT22 funcionaron adecuadamente para fines de laboratorio, pero su precisión y respuesta siguen siendo limitadas frente a sensores de uso biomédico real [15][16][18]

----------

# 10. Costos generales del sistema

| Componente           | Cantidad | Precio Unitario (COP) | Subtotal (COP) |
|:--------------------:|:--------:|:---------------------:|:--------------:|
| Transformador M-502 | 1        | 55,000                | 55,000         |
| Celda de carga 5 kg | 1        | 22,000                | 22,000         |
| Módulo HX711        | 1        | 7,500                 | 7,500          |
| MDF (pliego)        | 1        | 21,000                | 21,000         |
| Palo de balso 15x15 | 4        | 2,500                 | 10,000         |
| Sensor DHT22        | 1        | 9,000                 | 9,000          |
| Regulador LM7805    | 1        | 3,000                 | 3,000          |
| Bombillo 100W       | 1        | 4,000                 | 4,000          |
| Módulo relé         | 1        | 10,000                | 10,000         |
| Ventilador          | 1        | 8,000                 | 8,000          |
| **TOTAL**           |          |                       | **149,500**    |

**Nota:** Componentes como el ESP32 y la pantalla OLED no fueron incluidos en el cálculo de costos, ya que se contaba previamente con ellos para el desarrollo del proyecto.

----------

# 11. Limitaciones del Sistema

El prototipo desarrollado corresponde a un sistema experimental con fines académicos, por lo que no cumple con los requisitos necesarios para su uso clínico. No cuenta con certificaciones médicas, materiales biomédicos especializados ni condiciones de seguridad equivalentes a las de una incubadora neonatal real.

El sistema de control implementado es de tipo ON/OFF, lo que limita la precisión en la regulación de la temperatura. Este tipo de control no permite una modulación continua de la potencia, por lo que no es adecuado para aplicaciones que requieren alta estabilidad térmica.

El prototipo mide variables como temperatura, humedad y peso; sin embargo, no incorpora otros parámetros relevantes en el monitoreo neonatal, como saturación de oxígeno, frecuencia cardíaca, frecuencia respiratoria, concentración de CO₂ o control detallado del flujo de aire.

La medición de peso depende de la calibración de la celda de carga y puede verse afectada por factores mecánicos como la distribución de la carga, vibraciones o la estabilidad de la estructura.

Asimismo, el sensor DHT22 presenta limitaciones en precisión y velocidad de respuesta frente a sensores de uso biomédico, lo que restringe la exactitud del monitoreo térmico.

Finalmente, el sistema no incluye funcionalidades avanzadas como alarmas clínicas, registro de datos, comunicación remota ni estrategias de control más sofisticadas, lo que limita su alcance a un prototipo demostrativo.

----------

# Conclusiones

Se comprendió la importancia del control térmico en incubadoras neonatales y su impacto en el cuidado del recién nacido, especialmente en aquellos con baja capacidad de termorregulación como los bebés prematuros. A lo largo del desarrollo del laboratorio se reforzaron conceptos fundamentales de instrumentación biomédica, como la integración de sensores, la adquisición y procesamiento de datos, y el control de actuadores mediante un microcontrolador. Esto permitió entender cómo diferentes etapas de un sistema biomédico trabajan de manera conjunta para monitorear y regular variables fisiológicas.

El prototipo desarrollado funcionó de manera satisfactoria como una incubadora neonatal a escala, permitiendo medir temperatura, humedad y peso, así como visualizar estos datos en tiempo real a través de la pantalla OLED. El sistema de control térmico respondió adecuadamente mediante el uso del bombillo como fuente de calor y el ventilador para la regulación de la temperatura. Además, la implementación de LEDs facilitó la identificación rápida del estado térmico, permitiendo al usuario interpretar fácilmente si la temperatura se encontraba dentro o fuera del rango adecuado. En conjunto, el sistema cumplió su propósito académico al representar de forma clara el funcionamiento básico de una incubadora.

Como posibles mejoras, se recomienda implementar un sistema de control más preciso, como un controlador PID, que permita reducir las oscilaciones y mantener la temperatura más estable alrededor del valor deseado. Asimismo, sería conveniente utilizar sensores con mayor exactitud y mejorar la calibración del sistema de medición de peso. También se podrían incorporar variables adicionales relevantes en el monitoreo neonatal, así como funciones como alarmas, almacenamiento de datos o comunicación remota, con el objetivo de hacer el sistema más completo y acercarlo a una aplicación biomédica más realista.

----------

# Preguntas de Discusión

• Pregunta 1: ¿Qué otras variables (y por qué) además de las aquí mencionadas son críticas en el monitoreo neonatal?

Además de temperatura y humedad, son esenciales saturación de oxígeno (SpO2, para detectar hipoxia o cardiopatías, objetivo >90-95% post-nacimiento), frecuencia cardíaca (FC, ~120-160 lpm para estabilidad hemodinámica), presión arterial (PA), frecuencia respiratoria (FR ~40-60 rpm) y CO₂ transcutáneo (TcPCO₂, para ventilación no invasiva). Estas previenen hipoxia, acidosis y fallos cardiopulmonares en UCI neonatal [17].

• Pregunta 2: ¿Qué haría falta para convertir el sistema desarrollado en una incubadora neonatal real?

Se requiere control cerrado (servo-control PID con actuadores de calefacción/ventilación), cumplimiento IEC 60601-2-19 (precisión ±0.5°C, alarmas, ruido <60 dB(A), uniformidad térmica), materiales biocompatibles (sin VOCs), pruebas de seguridad eléctrica/biológica, esterilizabilidad, certificación FDA/INVIMA/CE y ensayos clínicos. Añadir redundancia en sensores, interfaz usuario y calibración anual [18].

• Pregunta 3: ¿Qué semejanzas hay entre una incubadora neonatal y una servo-cuna?

Ambas regulan temperatura (servo-control para neutral térmico), humedad y protegen neonatos prematuros de pérdida de calor, con calefacción radiante/convección y alarmas. Difieren en que incubadoras son cerradas (mejor aislamiento/humedad, primera semana), servo-cunas abiertas (acceso fácil para cuidados maternos) [19].

----------

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
20. M. H. Rashid, Power Electronics: Circuits, Devices and Applications, 4th ed. Pearson,(2014). https://share.google/Gdikp0bQ7nXfa68NM
21. R. Chura, “EJEMPLO DE ARTICULO CIENTIFICO.pdf,” Scribd. https://es.scribd.com/document/379178201/EJEMPLO-DE-ARTICULO-CIENTIFICO-pdf
