Laboratorio 4

ANÁLISIS DE COMPLEJIDAD

ALGORITMO BASADO EN FUERZA BRUTA


def eval(x):
    y = x**5-59*x**4+35*x**3-250*x**2+x-70
    return y

def fuerza_bruta():
    inicio = timeit.default_timer()
    error = 0.0001                                      #O(1)
    x0 = -1000                                          #O(1)
    x1 = -999                                           #O(1)
    y0 = eval(x0)                                       #O(1)
    y1 = eval(x1)                                       #O(1)
    aumentador = 1                                      #O(1)                                     
    cont = 0
    while abs(y1) > error and x1 <= 1000:               #O(n)
        if (y0 < 0 and y1 > 0) or (y0 > 0 and y1 < 0):  #O(1)
            aumentador *= 10 ** -1                      #O(1)             
            x1 = x0 + aumentador                        #O(1)               
        else:
            x0 += aumentador                            #O(1)                  
            x1 += aumentador                            #O(1)
        y0 = eval(x0)                                   #O(1)
        y1 = eval(x1)                                   #O(1)
        cont += 1                                       #O(1)                              
    fin = timeit.default_timer()                        #O(1)
    print("Raíz aproximada:", str(x1))
    print("f(raíz):", str(y1))
    print("Iteraciones:", str(cont))
    print("Tiempo:", fin-inicio, 'segundos')
    
Complejidad = O(7)+O(n)*O(6)=O(n)
    
Este algoritmo itera inicialmente con pasos de a una unidad desde el inicio del rango dado, evaluando la función en dos puntos consecutivos. Cuando se detecta un cambio de signo,  se cambia el paso a 0.1 y se itera entre estos dos puntos buscando nuevamente el cambio de signo. El algoritmo se repite, dividiendo en 10 el tamaño del paso cada vez que se identifique el cambio de signo, hasta que el valor evaluado caiga en el rango de tolerancia del error.

Para el cálculo de la complejidad se corrió el algoritmo varias veces aumentando cada vez el rango en el que se evalúa la función en un orden de 10^x. Se graficaron los tiempos que se demoró el algoritmo contra el tamaño del rango (n)  y dicha gráfica se comparó con otras gráficas conocidas (n, log n) para aproximar su comportamiento. Se concluyó que el algoritmo tiene una complejidad menor a log n hasta valores de n=6'000.000; a partir de este punto la gráfica del algoritmo supera la de log n y se acerca más a la de n. Por esto se concluye que en general  (y para valores de n más grandes) la complejidad del algoritmo es n.


ALGORITMO BASADO EN EL MÉTODO DE BISECCIÓN (PUNTO MEDIO)

def voraz():
    inicio = timeit.default_timer()
    error = 0.0001                                        
    x0 = -1000                                              #O(1)
    x1 = 1000                                               #O(1)
    y0 = eval(x0)                                           #O(1)
    y1 = eval(x1)                                           #O(1)
    xr = (x0+x1)/2                                          #O(1)                                      
    yr = eval(xr)                                           #O(1)                                      
    cont = 0                                                #O(1)
    while abs(yr) > error:                                  #O(log n)
        if (y0 < 0 and yr < 0) or (y0 > 0 and yr > 0):      #O(1)
            x0 = xr                                         #O(1)                              
            y0 = yr                                         #O(1)
        else:
            x1 = xr                                         #O(1)                                   
            y1 = yr                                         #O(1)
        xr = (x0 + x1) / 2                                  #O(1)                         
        yr = eval(xr)                                       #O(1)
        cont += 1                                           #O(1)                              
    fin = timeit.default_timer()                            #O(1)

    print("Raíz aproximada:", str(xr))
    print("f(raíz):", str(yr))
    print("Iteraciones:", str(cont))
    print("Tiempo:", fin - inicio, 'segundos')
    
voraz()
    
Complejidad = O(8)+O(log n)*O(6)=O(log n)



ALGORITMO VORAZ BASADO EN EL MÉTODO DE NEWTON RAPHSON

## Algoritmo voraz basado en el método de Newton Raphson para aproximar raíces del polinomio dado.

import time
errAbs = 0
contIteraciones = 0
numero = float(input('Digite cualquier número para comenzar a buscar raíces: '))

def raiz (errAbs, contIteraciones, numero):

    tic = time.time()
    while True:                                                                                         #O(log n)
        fxi = pow(numero, 5)-59*pow(numero, 4)+35*pow(numero, 3)-250*pow(numero, 2)+numero - 70         #O(1)
        fxxi = 5*pow(numero, 4)-236*pow(numero, 3)+105*pow(numero, 2)-(500*numero) + 1                  #O(1)
        
        Xi = numero-(fxi/fxxi)                                                                          #O(1)
        errAbs = abs((Xi - numero)/Xi*100)                                                              #O(1)
        contIteraciones += 1                                                                            #O(1)
        
        if (errAbs > 0.0001):                                                                           #O(1)
            numero = numero - (fxi/fxxi)
        else:                                                                                           #O(1)
            print('La raíz aproximada es:', numero)                                                     #O(1)
            print('Iteraciones:', contIteraciones)                                                      #O(1)
            break
    toc = time.time()
    timeTotal = toc-tic                                                                                 #O(1)
    print( f"Tiempo: {timeTotal:0.4f} segundos.")                                                       #O(1)

raiz (errAbs, contIteraciones, numero)

Complejidad = O(log n)*O(9)+O(1)=O(log n)



Desarrollado por:
- Santiago Rodríguez Camargo
- Fredy Alexander Gonzalez Pobre
- Víctor Manuel Torres
- Daniel Leonardo Sánchez
- Daniel Felipe Vargas Gómez

Se programó algoritmo de búsqueda de raíces por Fuerza bruta y dos algoritmos voraces: Método de bisección y de Newton Raphson y se hace el análisis de complejidad correspondiente.
Fecha: 19-04-2022
