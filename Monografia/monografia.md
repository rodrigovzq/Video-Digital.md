---
title: Sistemas de Transmision de Video para Drones
author : Rodrigo Mariano Vazquez
date: 17/12/2021
---
## Resumen
# Introducción
En los últimos años, los vehículos aéreos no tripulados (**VANT**) mejormente conocido como *drones* se han vuelto herramientas muy populares tanto para *hobbistas* como para profesionales. **VANT** es un término genérico para describir cualquier vehículo aéreo que sea controlado mediante control remoto. Esto incluye, aviones y helicópteros, conocidos en el ámbito del aeromodelismo y como más reciente integrante, el *drone*. Los drones profesionales tienen un amplio espectro de aplicación, las tomas aérea en deportes ya no requieren de costosos helicópteros y en la zona de *hobby*, el uso de drone encontró un espacio en la práctica de carreras, donde los pilotos utilizan un set de gafas que reciben una transmisión de video en vivo del punto de vista en *primera persona* del frente del drone (FPV). 
Esta última práctica será el foco de estudio, donde la transmisión de video desde el dron hasta el set de gafas (o *headset*) tiene unas particularidades que ponen en práctica y requieren de la última tecnología de transmisión digital y procesamiento en vivo.

# Drones y transmisión de video 

Los drones pueden ser piloteados de dos maneras, la de uso más frecuente en fotografía es la de vista desde la parte inferior del drone en una pantalla junto con un control remoto tipo *joystick*.
![[contro-drone.jpeg]]
La segunda forma de controlar un drone es con una vista en primera persona o FPV por su sigla en inglés. En este sistema la cámara del drone está apuntando en el mismo sentido que la dirección de vuelo. En este sistema la imagen de video proveniente de un circuito dentro del drone es transmitido por radio a una pantalla personal en tierra o bien en un *headset*.
![[drone-goggles.jpeg]]

## Tecnologías inalámbricas para transmisión de video

### Wi-Fi
El *Wi-Fi* puede ser usado para distancias muy cortas. El rango de la de la señal puede ir desde los 300 a 2000 metro, dependiendo del equipo y las condiciones ambientales. Es decir, el rango siempre depende de varios parámetros.
- Potencia de transmisión. Cuanto más grande la antena, más señal irradiará, con menor atenuación.
- La antena utilizada. En orden de importancia, la potencia de antena, tipo chip, calidad de PCB.
- La frecuencia utilizada. Generalmente, cuanto más baja sea la frecuencia, más lejos llegará la señal transmitida. La red de $5\ GHz$ tiene un rango más acotado que la de $2.4\ GHz$.
- Condiciones ambientales. Árboles cercanos, edificios, visión directa , condiciones atmosféricas, etc. Pueden afectar negativamente el rango de la señal Wi-Fi. Una visión directa en un día despejado es ciertamente una condición ambiental superior a un ambiente arbolado y en un día nublado.

A pesar de esto, la red de $5\ GHz$ suele ser la preferida debido a la menor interferencia que recibe esta banda en áreas urbanas.

### Banda sub 1 GHz

Una solución común para aquellos que vuelan FPV es, sencillamente, utilizar cámaras y un sistema de transmisión analógico en una banda de transmisión de $900\ MHz$. Con una transmisión de $1\ W$ y una antena tipo *cloverleaf* (usual en estos casos) y una antena receptora de $18\ dB$ dirigida al dron, puede alcanzar más de $8 km$ de alcance.

![[analog-drone.jpeg]]


### 3G/4G

También es posible el empleo de dispositivos transmisores de 3G/4G instalados en el drone para una transmisión inalámbrica de datos con una tasa muy alta. Esta solución es altamente dependiente de la cobertura de estas señales en las zonas de vuelo.

### Solución personalizada

Transmisores RF integrados no solo son una solución muy utilizada en arquitecturas de radio definida por software (SDR) en estaciones de telefonía celular, como en el sistema de acceso distribuido multiservicio (MDAS) y una pequeña célula, pero también para la transmisión de video en HD para aplicaciones, comerciales, industriales y militares como los UAV (sigla en inglés de VANT).
Uno puede hacer uso de transmisores RF de la línea AD9361/AD9363 y armar el hardware adecuado basado en el espectro disponible para este uso. Hay disponibilidad de transmisores/receptores aptos para operar en bandas de hasta $6\ GHz$. Es frecuente el empleo de transmisión por banda lateral vestigial para procesamiento digital.

## Desafíos para la transmisión de video

El rango del enlace inalámbrico de video está limitado un número de factores. La perdida del camino entre el transmisor y el receptor en sí, aumentara con la distancia y los obstáculos en la línea de visión pueden aportar a la atenuación. Sin embargo, en un entorno natural existen algunos desafíos menos evidentes para el enlace de radio que requieren de soluciones inteligentes. Se verá a continuación las dos cuestiones principales para el vuelo FPV.

![[fpv-drone.jpeg]]
###  Compresión y transmisión de baja latencia
En el caso de usar un sistema de transmisión digital, existen varias formas de introducir latencia en un sistema de transmisión y compresión de video. Los procesos que forman parte desde la captura de la imagen hasta la recepción y decodificación forman una línea temporal donde típicamente la latencia es de los cientos de milisegundos.
![[latencia-total-digital.png]]

En este escenario se introduce una latencia inaceptablemente alta para este tipo de aplicaciones, ya que si el sistema aéreo está viajando a $15 m/s$, el dron ha viajado $1.8 m$ cuando el piloto detecta que hace falta maniobrar. Esto resulta en un comportamiento errático del dron, imposibilitando este sistema para uso de FPV.
Con  el objetivo de posibilitar la transmisión digital para FPV, el estándar H.264 incorpora el concepto de capas. Una capa está compuesta por varios bloques (un bloque es una unidad bidimensional de cuadro de video) y cada bloque es codificado independientemente, haciendo posible que se pueda decodificar cada bloque por si solo sin necesidad de un cuadro de referencia anterior.

![[latencia-mejorada.png]]
 
El sistema no tiene que esperar que un cuadro entero sea capturado para empezar a codificarlo. Tan pronto como una capa sea capturada, el proceso de codificación puede comenzar. De igual modo, tan pronto como una capa es codificada, su transmisión puede comenzar, así sucesivamente. El impacto de este sistema es que el proceso ya no es serializado sino que puede ser paralelizado con cierto solapamiento entre las operaciones.
 Existe una relación de compromiso entre el número de capas y la cantidad de compresión. Cuanto más alto sea el número de capas, más rápido se puede codificar y transmitir. Sin embargo, esto reduce la tasa de compresión y aumenta el número de bits usados para cada capa y haciendo que aumente el tiempo de transmisión para cada capa. El diseñador del drone deberá dimensionar la relación entre estos aspectos de manera de optimizar la latencia del sistema de punta a punta. Cualquier solución requiere de una flexibilidad que no limite las posibilidades del fabricante.


### Interferencia

Otras fuentes de transmisión de radio en el medio ambiente pueden interferir con la señal de video. Si las señales interferentes ocurren dentro de la misma banda de frecuencias en la que ocurre el enlace de video inalámbrico, estas actuaran como ruido de banda. Esto provoca una reducción en la relación señal a ruido, lo que resultara en una imagen de video con ruido y un alcance más limitado. Un interferente típico puede ser el transmisor de video de otro dron cercano, un punto de acceso Wi-Fi o mismo un teléfono móvil. El problema se puede minimizar seleccionando un canal lo más lejos posible en frecuencia del interferente, o moviendo el receptor de video y la antena. Si la fuente de interferencia es poderosa, pero fuera de la banda del enlace inalámbrico, se le llama *bloqueador*. La señal de bloqueo puede penetrar en el filtrado de entrada y disminuir la dinámica del amplificador de bajo ruido (LNA). En la figura se puede apreciar un diagrama simplificado de una cadena de señal receptora. Los bloqueadores típicos de alta potencia pueden ser radares, torres de transmisión o radios militares.  Las medidas técnicas para manejar interferencias pueden ser garantizar un buen filtrado del canal frontal del receptor de video y utilizar una antena direccional de tierra para minimizar la interferencia desde otras direcciones. Las antenas direccionales con un haz estrecho y una alta ganancia direccional también aumentarán la fuerza de recepción de la señal del dron. La antena incluso puede equiparse con un rastreador que dirige automáticamente la antena al dron en movimiento. 
![[diagrama-interferencia.png]]

### Atenuación multi-trayecto debido a reflexión

Incluso con una fuerte señal de transmisión y libre de ruido, un enlace puede sufrir de cortes repentinos, especialmente en entornos urbanos. Esto pude deberse a que la ruta de propagación reflejada cancela a la ruta de propagación directa. La cancelación se produce debido al cambio de fase asociado con distintas diferencias en el retraso de propagación. Esto ocurre en un punto específico del espacio receptor, y puede desaparecer simplemente moviendo la antena menos de una longitud de onda. Además, 
de la cancelación de la señal, la atenuación multi-trayecto también resulta en la propagación del *delay* del símbolo. Los símbolos de diversas rutas llegan en diferentes momentos, causando errores de bits si el retraso es significativo. La siguiente figura muestra el principio de atenuación multi-trayecto y propagación del *delay*.

![[multipath-propagation.png]]

Las dos estrategias principales para hacer frente a esta atenuación son evitar o combinar constructivamente las señales reflejadas. Esto es, utilizando un enfoque direccional en la línea de visión o bien, emplear un circuito que combine las señales reflejadas utilizando múltiples antenas espaciadas por una distancia aproximada de una longitud de onda o más.

![[diversity-receiver.png]]

## Superar los desafíos

Actualmente, la industria tuvo un dominio de la transmisión analógica causada prácticamente por necesidad, este tipo de transmisión presenta unas ventajas que hasta hace menos de un año sencillamente no se encontraban en el plano digital. La casi nula latencia, los pequeños circuitos y el bajo costo hicieron que la transmisión analógica sea el estándar de facto. Aun así la inevitable desventaja de la calidad de imagen sirvió de motor para que hoy se esté viviendo una transición de sistemas de transmisión de video en el uso del vuelo FPV. 

### Cámara FPV

Las cámaras usadas en las configuraciones FPV suelen ser ligeras y compactas, pero robustas y muy sensibles a la luz. Aparte de la óptica, el sensor de imagen es la parte más crítica para un video de alta calidad. Actualmente hay dos tipos principales de sensores de imagen: *Complementary Metal Oxide Semiconductor* o **CMOS** y *Charge Coupled Device* o **CCD**. Los sensores CMOS se emplean más comúnmente, son más baratos, requieren de una baja tensión operativa y. tienen un menor consumo de energía que los CCD. La mayoría de los pilotos de drones exigen video de alta calidad, incluso cuando se mueven rápido y durante las vibraciones, necesario por la dificultad de controlarlos en esas situaciones. En esta área, los sensores de imagen CMOS tienen algunas deficiencias. Las imágenes del sensor se escanean línea por línea y hay un límite a esta velocidad de escaneo. Esta forma de capturar la imagen se llama *obturador rodante*. En un dron de rápido movimiento con vibración de alta frecuencia debido a los motores y hélices, se notarán artefacto y distorsión al utilizar este tipo de escaneo. 
![[Rolling-Shutter.png]]
*Efecto de "obturador rodante" expuesto exageradamente*

Las cámaras CCD, por otro lado, tienen una manera diferente de capturar la imagen. La carga inducida por la luz en cada pixel se recoge de todas las líneas simultáneamente. Esto se conoce como *obturador global* y es la razón principal por las que las cámaras CCD pueden manejar rápidos movimientos y altas vibraciones sin distorsiones en la imagen. Las celdas o píxeles requieren pequeñas cantidades de luz y, por lo tanto, el muestreo del fotograma completo puede ser más rápido. Dado que la lectura del CCD y la conversión de señal requieren menos circuitos activos en el propio sensor, las imágenes en crudo contendrán menos ruido que la salida de un CMOS. Los sensores CCD también tendrán un rango dinámico más alto, es decir, una mayor latitud entre el umbral de poca luz y la saturación de un píxel. Las mejores cámaras CCD para las configuraciones FPV de consumo son lo suficientemente sensibles a la luz incluso para vuelos nocturnos, con solo unas pocas fuentes de luz presentes. Sin embargo, las cámaras CCD son más caras y requieren de una tensión operativa más alta para hacer funcionar las celdas en el sensor. El circuito de conversión también consume más potencia que su equivalente en CMOS.


### Transmisión FPV analógica

La mayoría de los sistemas FPV de hobbistas e incluso profesionales, todavía utilizan transmisión de video analógica, con sistemas muy compactos  y de bajo costo. La siguiente figura muestra un sistema de transmisor FPV analógico completo que da aproximadamente 1 km de alcance (la pila AA esta como referencia del tamaño).

![[transmision-analogica.jpeg]]

El video analógico es en tiempo real y no requiere de compresión de imágenes ni procesamiento avanzado. Esto resulta en una latencia muy cercana a cero entre la imagen capturada por la cámara y la vista por el piloto. La latencia de solamente decenas de milisegundos que a menudo es muy notable cuando se vuela a las altas velocidades que alcanzan los FPV (pueden llegar a cerca de 200 km/h) y los cientos de milisegundos que frecuentemente se ven en los sistemas digitales de HD para uso del consumidor plantean un riesgo para la seguridad.
Otra propiedad sorprendentemente favorable del video analógico es el aumento gradual del ruido de la imagen cuando el enlace de video comienza a descomponerse. Esto ocurre cuando se alcanzan los límites del rango de radio, o se encuentran con interferencias u obstáculos. Un piloto con experiencia, instintivamente sabe que tiene que dar la vuelta al dron o evitar un obstáculo. Lo más probable es que con un enlace de video digital de calidad accesible a consumidor, un rápido decrecimiento de la relación señal a ruido provocará un parpadeo y cuadros congelados.


### Transmisión FPV digital

En los últimos dos años, el intenso desarrollo se ha dedicado a crear enlaces de video HD compactos y de baja latencia. El sistema de transmisión de radio digital necesita robustez para preservar una velocidad de fotogramas aceptable incluso en condiciones de radio que se deterioran rápidamente. Se aplican esquemas de modulación dinámica de rápida adaptación, para reducir el ancho de banda requerido durante un periodo, con una calidad de señal reducida. Se mantiene una velocidad de fotogramas razonable mientras se restringe la resolución de video. Un enlace de video en HD inalámbrico y de alta velocidad de fotogramas requiere de velocidades de bits muy altas y, por lo tanto, se necesita una modulación avanzada.
Esto pone un estricto requisito en la relación señal a ruido, por lo que se aplica una variante del concepto **MIMO** de antena explicando anteriormente (combinación constructiva de señales), junto con la multiplexación por división de frecuencia ortogonal (OFDM). El OFDM es muy efectivo para la comunicación a través de canales con atenuación selectiva de frecuencia. Con una portadora tradicional de banda ancha única, la atenuación selectiva es difícil de manejar. OFDM ayuda a mitigar el problema convirtiendo los datos serie de alta velocidad en subportadoras paralelas de bajo ancho de banda cada una. Algunas subportadoras están reservadas como portadoras piloto (utilizadas para la estimación/ecualización del canal y para combatir los errores de magnitud y fase en el receptor) y algunas no se utilizan para dejar como bandas de guardia. La reserva de subportadoras a bandas de protección ayuda a reducir la radiación fuera de banda y, por lo tanto, facilita los requisitos en los filtros frontales del transmisor. En el receptor, se aplica una corrección de atenuación para cada subportadora. El principio de OFDM es bien conocido en los sistemas Wi-Fi  y la radiodifusión DAB. La siguiente figura muestra un diagrama en bloques simplificado del concepto OFDM

![[OFDM.png]]

La modulación subyacente se selecciona dinámicamente dependiendo de la relación señal a ruido disponible del canal. La modulación de cuadratura (QAM) es una forma de modulación donde cada constelación representa una cierta amplitud y fase de la señal de radio. A 64QAM, un símbolo equivalente a 6 bits y produce una alta tasa de bits por subportadora, pero esta constelación solo se puede utilizar bajo una buena SNR. En condiciones de canal en deterioro, la modulación baja a 16QAM y continúa simplificando las constelaciones si el canal empeora. Para condiciones muy malas, se emplea la modulación binaria por desplazamiento de fase (BPSK) con únicamente dos constelaciones, donde cada constelación representa un cambio de fase. 
Con un solo bit por símbolo, da una tasa de bits muy modesta, pero correspondientemente robusto para condiciones ruidosas. En este estado, la resolución de video y la velocidad de fotogramas son suficientes para volar de forma segura durante un corto periodo de tiempo. Las siguientes figuras muestran una simulación de como la interferencia fuera y dentro del canal afectan a una constelación de 16QAM. 

![[Interference-outside-the-channel.png]]
*Interferencia fuera del canal*

![[Interference-inside-the-channel.png]]
*Interferencia dentro del canal*

![[video-feo.jpeg]]
*Vídeo preservado durante la intensidad de señal reducida*

![[video-lindo.jpeg]]
*Calidad de imagen en modo normal*

A diferencia de los enlaces de radio WiFi, un enlace FPV de baja latencia no puede depender de una señal de reconocimiento/confirmación (*acknowledge*) para cada fotograma de datos, y no admite el reenvío de fotogramas de datos fallidos. En su lugar, se emplea la codificación de corrección de errores adelante (FEC), para manejar la mayoría de los errores de bits que ocurren. Los pocos fotogramas erróneos restantes formarán parte del flujo de video mostrado. Esto se puede observar como bloqueo ocasional en la imagen, pero no afectará mucho la calidad de la imagen si la modulación adaptativa reacciona rápidamente durante el empeoramiento de las condiciones de radio. Las imágenes de las figuras anteriores muestran capturas de video tomadas durante una prueba de conducción de un enlace de vídeo HD inalámbrico digital. Son un buen ejemplo de un esquema de modulación adaptativa funcionando.



# Conclusión
## El futuro del desarrollo FPV


Los drones prometen posibilitar nuevas aplicaciones y ser el sustento de un aumento de productividad económica. Sin embargo, requieren modos de operación solamente posibles con conexiones inalámbricas robustas y video de ultra baja latencia.
El vídeo inalámbrico para el pilotaje de drones FPV sigue siendo una tecnología inmadura, queda pendiente ver que surjan sistemas HD FPV compactos y de bajo costo en un futuro cercano. La clave para reducir el costo es una mayor integración de los sistemas en chip (SoC) y un alto volumen de producción para bajar los costos. Los cambios de paradigma ocurrirán cuando surjan conceptos totalmente nuevos de radio, cámara o pantalla. La próxima generación de tecnología celular y Wi-Fi, denominada 5G, explotará la formación dinámica de haces para aumentar la ganancia del sistema y mantener la interferencia baja (onda milimétrica). Junto con un MIMO más sofisticado, esto aumentará aún más el rendimiento y el ancho de banda de transmisión. Es probable que estos conceptos se apliquen para futuros sistemas FPV cuando madure la tecnología, como es posible ver en los más recientes lanzamientos de la empresa DJI. Esto resultará en un mayor rendimiento con un rango extendido, una mayor calidad de imagen y una mejor fiabilidad. Permitirá a los drones manejar más de nuestros desafíos actuales, y aquellos en los que aún no hemos llegado a pensar.
