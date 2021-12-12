---
title: Sistemas de Transmision de Video para Drones
author : Rodrigo Mariano Vazquez
date: 17/12/2021
---
## Resumen
# Introduccion
En los ultimos años, los vehiculos aereos no tripulados (**VANT**) mejormente conocido como *drones* se han vuelto herramientas muy popoulares tanto para *hobbistas* como para profesionales. **VANT** es un termino generico para describir cualquier vehiculo aereo que sea controlado mediante control remoto. Esto incluye, aviones y helicopteros, conocidos en el ambito del aeromodelismo y como mas reciente integrante, el *drone*. Los drones profesionales tienen un amplio espectro de aplicacion, las tomas aerea en deportes ya no requieren de costosos helicopteros y en la zona de *hobbie*, el uso de drone encontró un espacio en la practica de carreras, donde los pilotos utilizan un set de gafas que reciben una transmision de video en vivo del punto de vista en *primera persona* del frente del drone (FPV). 
Esta ultima practica será el foco de estudio, donde la transmision de video desde el dron hasta el set de gafas (o *headset*) tiene unas particularidades que ponen en practica y requieren de la ultima tecnologia de transmision digital y procesamiento en vivo.

# Desarrollo
Los drones pueden ser piloteados de dons maneras, la de uso mas frecuente en fotografia es la de vista desde la parte inferior del drone en una pantalla junto con un control remoto tipo *joystick*.
![[contro-drone.jpeg]]
La segunda forma de controlar un drone es con una vista en primera persona o FPV por su sigla en inglés. En este sistema la camara del drone esta apuntando en el mismo sentido que la direccion de vuelo. En este sistema la imagen de video proveniente de un circuito dentro del drone es transmitido por radio a una pantalla personal en tierra o bien en un *headset*.
![[drone-goggles.jpeg]]

## Teconologias inalambricas para transmision de video

### Wi-Fi
El *Wi-Fi* puede ser usado para distancias muy cortas. El rango de la de la  señal puede ir desde los 300 a 2000 metro, dependiendo del equipo y las condiciones ambientales. Es decir, el rango simpre depende de varios parametros.
- Potencia de transmision. Cuanto mas grande la antena, mas señal irradiará, con menor atenuacion.
- La antena usada. En orden de importancia, la potencia de antena, tipo chip, calidad de PCB.
- La frecuencia usada. Generalmente cuanto mas baja sea la frecuencia, mas lejos llegará la señal transmitida. La red de $5\ GHz$ tiene un rango mas acotado que la de $2.4\ GHz$.
- Condiciones ambientales. Arboles cercanos, edificioes, vision directa , condiciones atmosfericas, etc. Pueden afectar negativamente el rango de la señal Wi-Fi. Una visión directa en un dia despejado es ciertamente una condicion ambiental superior a un ambiente arbolado y en un dia nublado.

A pesar de esto, la red de $5\ GHz$ suele ser la preferida debido a la menor interferencia que recibe esta banda en areas urbanas.

### Banda sub 1GHz

Una solucion común para aquellos que vuelan FPV es, sencillamente, utilizar camaras y un sistema de transmision analogico en una banda de transmision de $900\ MHz$. Con un transmision de $1\W$ y una antena tipo *cloverleaf* (de uso común en estos casos) y una antena receptora de $18\ dB$ dirigida al dron, puede alcanzar mas de $8 km$ de alcance.

![[analog-drone.jpeg]]

### 3G/4G

Tambien es posible el uso de dispositivos transmisores de 3G/4G instalados en el drone para una transmision inalambrica de datos con una tasa muy alta. Esta solucion es altamente dependiente de la cobertura de estas señales en las zonas de vuelo.

### Solucion personalizada

Transmisores RF integrados no solo son una  una solucion muy utilizada en arquitecturas de radio definida por software (SDR) en estaciones de telefonia celular, como en el sistema de acceso distribuido multiservicio (MDAS) y una pequeña celula, pero tambien para la transmision de video en HD para aplicaciones, comerciales, industriales y militares como los UAV (sigla en ingles de VANT ).
Uno puede hacer uso de transmisores RF de la linea AD9361/AD9363 y armar el hardware adecuado basado en el espectro disponible para este uso. Hay disponibilidad de transmisores/receptores aptos para operar en bandas de hasta $6\ GHz$. Es frecuente el uso de transmision por banda lateral vestigual para procesameinto digital.

# Desafios para la transmision de video

El rango del enlace inalambrico de video esta limitado un numero de factores. La perdida del camino entre el transmisor y el receptor en si, aumentara con la distancia y los obstaculos en la linea de visión pueden aportar a la atenuación. Sin embargo, en un entorno natural existen algunos desafios menos evidentes para el enlace de radio que requieren de soluciones inteligentes. Se verá a continuacion las dos cuestiones principales para el vuelo FPV.

![[fpv-drone.jpeg]]

## Interferencia