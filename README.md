# Entrega 4 - Diseño del reticulado

## Casos de Análisis

* Se considera el siguiente reticulado de largo 15 m, ancho 2 m y alto 3,5 m compuesto por barras de sección circular hueca, inicialmente de radio R = 8 cm y espesor t = 5 mm

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/ret.png)

* Se considera que además de la carga muerta (D) de peso propio, este se diseña para una sobrecarga de uso (L) que corresponde a una carga distribuida sobre el tablero central de   qL = 400 kg / m^2

* Con esto se analizan las tensiones producidas en 2 casos:



![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/ret_caso1.png)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/ret_caso2.png)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/FU_caso1.png)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/FU_caso2.png)




* Inicialmente se tiene un peso del reticulado de 24197 kg

## Rediseño total del reticulado



![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/ret_caso1_redisenototal.jpg)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/ret_caso2_redisenototal.jpg)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/FU_caso1_redisenototal.jpg)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/FU_caso2_redisenototal.jpg)


## Rediseño de 5 barras



* Para el rediseño se escogieron las barras 0, 1, 2, 28 y 29

* La función de rediseño de cada barra es la siguiente:

```
def rediseñar(self, Fu, ϕ=0.9):
		"""Para la fuerza Fu (proveniente de una combinacion de cargas)
		re-calcular el radio y el espesor de la barra de modo que
		se cumplan las disposiciones de diseño lo más cerca posible
		a FU = 1.0.
		"""
		f = 1.
		p = 1e-4

		while f > 0:
			
			self.R = self.R * f
			self.t = self.t * f	
			
			if self.obtener_factor_utilizacion(Fu, ϕ=0.9) < 0.99:
				self.R = self.R / f
				self.t = self.t / f	
				f = f - p
			
			elif self.obtener_factor_utilizacion(Fu, ϕ=0.9) > 1.:
				self.R = self.R / f
				self.t = self.t / f	
				
				f = f + p
				
				self.R = self.R * f
				self.t = self.t * f
				break
			
			else:
				break

		"""Aqui se cambia R y t para que tengan un valor entero"""
		
		R = ceil(self.R * 100)
		t = ceil(self.t * 1000)
		
		self.R = R/100
		self.t = t/1000
		
		return self.R, self.t 
    
```

* Donde inicialmente se determina el valor de el factor de amplificación "f" y el paso "p". "p"    comienza a modificar el valor de "f" dependiendo de el nuevo valor del factor
  de utilización "FU", es decir, si FU es menor a 1 entonces "f" continua disminuyendo hasta que supera el FU = 1.0. Finalmente, una vez que FU está lo más cercano a 1.0, se
  ajusta el valor de "R" y "t" de la barra, de modo que sean valores enteros, por ejemplo 2.3 cm = 3.0 cm.
  
  
  
  
### Nuevos factores de utilización, fuerzas en las barras y deformada para cada combinación de carga




* Los criterios de rediseño que se tomaron en cuenta fueron que cuando el factor de utilización era menor a 1 entonces “f” comenzaba a disminuir lo cual hace que aumente el FU
  hasta llegar lo mas cercano a un FU = 1. 
  Luego cuando FU se acerca a 1 se va ajustando el valor de R y t en la barra, este a su vez se va considerando como el valor entero del radio y grosor que se calcula.


![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/ret_caso1rediseno.jpg)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/ret_caso2rediseno.jpg)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/FU_caso1rediseno.jpg)

![Alt Text](https://github.com/raimolid/MCOC2020-P2-3/blob/main/FU_caso2rediseno.jpg)


  
* De esta manera el peso del reticulado disminuyo de 24197 kg a 20021 kg lo que afecta en la tensión del caso 2: 1.2 D + 1.6 L en donde se puede apreciar un cambio en las
  tensiones de las barras 0, 1, 2, 28 y 29 en casi el doble de la original. A su vez los factores de utilización en el caso 2 de las barras a estudiar aumentan en el doble de lo
  que se veían originalmente.
  
* En el caso 1 ni la  tensión  ni el factor de utilización  cambiara, debido a que no hay carga viva que afecte en la combinación de carga por lo que solo se considerara la
  carga muerta.





### Desplazamientos verticales

* Se obtuvieron los siguientes desplazamientos para los nodos del tablero:

Desplazamiento nodal nodo 0: [0. 0. 0.]

Desplazamiento nodal nodo 1: [ 6.30641050e-06  1.50681106e-06 -1.02143151e-04]

Desplazamiento nodal nodo 2: [ 1.79948890e-05  1.50681106e-06 -1.02143151e-04]

Desplazamiento nodal nodo 3: [2.43012995e-05 0.00000000e+00 0.00000000e+00]

Desplazamiento nodal nodo 7: [0. 0. 0.]

Desplazamiento nodal nodo 8: [ 6.30641050e-06 -1.50681106e-06 -1.02143151e-04]

Desplazamiento nodal nodo 9: [ 1.79948890e-05 -1.50681106e-06 -1.02143151e-04]

Desplazamiento nodal nodo 10: [2.43012995e-05 0.00000000e+00 0.00000000e+00]


* Luego del rediseño se obtuvieron los siguientes desplazamientos:

Desplazamiento nodal nodo 0: [0. 0. 0.]

Desplazamiento nodal nodo 1: [-1.16154987e-06 -1.26739481e-05 -2.81815982e-04]

Desplazamiento nodal nodo 2: [ 1.88956319e-05 -2.09908203e-05 -2.82807775e-04]

Desplazamiento nodal nodo 3: [3.18798593e-05 0.00000000e+00 0.00000000e+00]

Desplazamiento nodal nodo 7: [0. 0. 0.]

Desplazamiento nodal nodo 8: [ 8.39924747e-06 -1.55197345e-05 -2.81815982e-04]

Desplazamiento nodal nodo 9: [ 1.44652111e-05 -2.43204931e-05 -2.82807775e-04]

Desplazamiento nodal nodo 10: [1.64690789e-05 0.00000000e+00 0.00000000e+00]

### Comentarios

* La nueva distribución del FU del reticulado muestra que aumento al doble el factor de utilización en el caso 2 debido a que el peso del reticulado disminuye de 24197 kg a
  20021 kg.
* Algunos cambios globales que se pueden hacer para mejorar aun mas el peso del reticulado es el de acercarse aun mas a un factor de utilización igual a 1, de esta manera el
  peso disminuiría en cada barra haciendo el reticulado mas económico. Para esto se pueden cambiar la altura de los nodos y de esta manera cortar las barras.

