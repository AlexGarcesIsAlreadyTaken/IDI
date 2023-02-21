# INTERACCIÓ I DISSENY D'INTERFÍCIES
## INTRODUCCIÓN

**Informática Gráfica**: Comunicar información usando imágenes por computador a partir de *modelos de datos* e interactuar con los mismos datos y su visualizacion

**Esquema Sistema Gráfico**
	
	         +--------+    +--------------+
	Datos -> | MODELO | -> | VISUALIZADOR | -> PERIFERICO
	         +--------+    +--------------+
	                  \       |
	                    \     |
	                  INTERACCIÓN (usuario)

> La ultima fase de impresión se reduce a *de qué color se pinta cada pixel*

## MODELOS GEOMÉTRICOS

Solidos: \
	- Limitados por superficie \
	- Movimientos sobre el modelo no modifican su forma \
Modelos geométricos: \
	- Modelo de Fronteras
	- Caras planas / TRIANGULOS

Almacenamos los solidos a partir de los *vértices* que lo conforman
> Un vértice sera representado con las coordenadas *x, y, z*.

La forma en que almacenamos los vertices nos ha de permitir saber cuales forman un triangulo entre sí.

**TOPOLOGÍA IMPLÍCITA**: Almacenamos en una tabla los vertices de tal forma que cada 3 forman un triangulo. Este metodo plantea la repetición de vertices ya que uno solo puede pertenecer a varios triangulos. \
	
	+-x---y---z-+ 
	|   |   |   | +
	| a | b | c | 3
	|   |   |   | +
	|...........|
	| a | b | c |
	+-----------+

**TOPOLOGÍA EXPLICITA**: Usamos dos tablas,\
	1. Tabla de caras [normal, IdVertices] \
	2. Tabla de vertices [x, y, z] 

> *Normal* da la dirección y el sentido de la perpendicular a la cara.\
> *IdVertices* es conformado por tres elementos que apuntan a entradas de la tabla de vertices.
