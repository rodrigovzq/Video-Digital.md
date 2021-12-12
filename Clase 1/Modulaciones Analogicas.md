# Que significa *modular*?
Es meter informacion en una señal que sea facil de transmitir
$s(t) = A cos \theta(t)$


## Por que se modula?
- Facilidad de radiacion
- Transmision simultanea de varias señales (FDM)
	- Sobre portadoras distintas, sumadas en tiempo, separadas en frecuencia -> Multiplex por Division de Frecuencias.
- Intercambio de SNR y BW
	- si BW_modulante< BW_altafrecuenca -> se intercambia SNR con BW.
	- Usando mas BW de lo necesario, al demodular vuelvo al BW original y gano en SNR.
	- En los que se puede modificar la parte angular de la portadora.
	- 

## Tipos de modulacion
### Analogica
- DBL-PS : Doble banda lateral, portadora suprimida.
	- La version en cuadratura se utiliza para enviar croma -> 2 de los 3 colores primarios.
	- Se transmiten defasadas en 90 grados
- BLU-PS: Banda lateral unica, portadora suprimida
- AM: Amplitud modulada
- BLV-CP: Banda Lateral Vestigial, con portadora. Variante de AM.
	- utilizado par transmitir luminancia. La parte de blanco y negro.
- FM: Frecuencia Modulada. Frecuencia = $\partial Fase$
	- utilizado para enviar sonido
- PM : Phase Modulated

### Digital
- ASK
- PSK: utilizado en satelite
- QAM: modulacion en cuadratura
	- Combinacion de amplitud y fase utilizado en Tv por cable
- FSK


## DBL 
![[Pasted image 20210915173302.png]]
Al modular la señal se corren todas las frecuencias de la informacion y se centra sobre la portadora.
![[Pasted image 20210915173438.png]]
USB: Upper Side Band (Banda lateral superior)
LSB: Lower Side Band (Banda lateral inferior)
Al usar DBL se duplico el ancho de banda.
![[Pasted image 20210915174030.png]]
**Deteccion Sincronica**
![[Pasted image 20210915174101.png]]
Circuito deteccion sincronica. 
![[Pasted image 20210915174317.png]]
e_o es la salida despues del filtro.
### Resumen
- Los sistemas de deteccion sincronica son muy sensibles a los errores de fase/frecuencia.
- Duplican ancho de banda

## BLU
![[Pasted image 20210915174607.png]]
Solo con una banda lateral me alcanza para recuperar la informacion entera.
![[Pasted image 20210915174941.png]]
Si la frecuencia central >> separacion frecuencias de bandas laterales, la demodulacion puede resultar en una atenuacion de la informacion.
El talon de aquiles es la separacion entre las bandas laterales.
La deteccion sigue siendo sincronica

## QAM : modulacion en cuadratura

![[Pasted image 20210915175339.png]]
$m_1 y m_2$ son la informacion de color, van defasadas en 90 grados.
![[Pasted image 20210915175527.png]]

Producto con cos y elimino el termino de 2wc, me queda m1
Si se introduce un error de fase, aparece una combinacion entre $m1$ y $m2$ (se intermodulan).
Tiene que haber un *enganche* entre el oscilador de transmisor y el receptor. Un pulso de sincronismo.
Se mandan rafagas de frecuencia $w_c$ (subportadora de color) para enganchar en el oscilador receptor.
Si armo asi, puedo detectar mas facil?
![[Pasted image 20210915180029.png]]
Envolvente de alta potencia
![[Pasted image 20210915180222.png]]
La frecuencia de deteccion sale del $RC$ del circuito.
![[Pasted image 20210915180328.png]]
$f_{corte}> f_{max modulante}$ y $< f_{portadora}$
Resumen:
Detectores faciles y baratos
Desperdicia potencia

## BLV-CP

![[Pasted image 20210915180614.png]]
BLU no uso porque distorsiona mucho frecuencias bajas
AM usa demasiado ancho de banda. 
Se usa algo intermedio.
Se transmite toda una banda lateral y parte de la otra
![[Pasted image 20210915180731.png]]
Se le agrega una portadora de alta potencia para poder usar detector de envolvente.
Todas las que tengan portadora de alta potencia pueden usar detector de envolvente.
Los demas requieren deteccion sincronica
![[Pasted image 20210915180822.png]]
gris: filtro de transmision
verde: filtro de recepcion

## PM y FM
Se cambian las caracteristicas angulares de la señal
![[Pasted image 20210915181006.png]]
Mejora el ancho de banda porque el corrimiento entre las frecuencias de info es mas chico.
Pero el ancho de banda es mas grande en general porque no solo depende de la separacion de frecuencias
pero...
![[Pasted image 20210915181408.png]]
achicando $k_f$ mejora el ancho de banda.
$\phi_{FM}$ tiene el mismo ancho de banda que en AM
$\beta$ es el indice de modulacion. Si es >1 el ancho de banda ocupado es cada vez mayor. $\Delta f$ es desplazamiento de frecuencia.
![[Pasted image 20210915181734.png]]
Descomposicion de Fourier para un tono puro. Un quilombo comparado con AM.
Mejora SNR, se usa para high fidelity.
![[Pasted image 20210915182306.png]]
Utiliza multiplicadores y conversores para una AM banda angosta y una FM con  beta y portadora apropiadas.
Detector
![[Pasted image 20210915182555.png]]
Laso de fijacion de fase, sale una señal proporcional a la diferencia de frecuencias
![[Pasted image 20210915182636.png]]
Efecto caputra. en FM hace malta menos diferencia de potencia para que la señal interferente se atenue. $35dB$ en AM vs $6dB$ en FM.
![[Pasted image 20210915183006.png]]
Como el ruido se vuelve mas fuerte a mas altas frecuencias. la SNR no es constante en el espectro. Por eso se usa el preenfasis y deenfasis, son filtros
![[Pasted image 20210915183052.png]]
Comparando con sistema de banda base, con ruido blanco no correlacionado
![[Pasted image 20210915183252.png]]
max SNR en AM es $\gamma/2$
![[Pasted image 20210915183503.png]]
existe un efecto de umbral en AM.
![[Pasted image 20210915183603.png]]
cuando $\beta$ es mas grande, SNR es ams grande
![[Pasted image 20210915183635.png]]
Existe un efecto de umbral en FM cuando el ruido es mas grande que la señal