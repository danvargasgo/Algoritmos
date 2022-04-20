Laboratorio 4

ANÁLISIS DE COMPLEJIDAD

ALGORITMO BASADO EN FUERZA BRUTA


def eval(x):
    y = x**5-59*x**4+35*x**3-250*x**2+x-70
    return y

def fuerza_bruta():
    inicio = timeit.default_timer()
    error = 0.0001                                      #error de y
    x0 = -1000
    x1 = -999
    y0 = eval(x0)
    y1 = eval(x1)
    aumentador = 1                                      #tamaño del paso inicial
    cont = 0
    while abs(y1) > error and x1 <= 1000:
        if (y0 < 0 and y1 > 0) or (y0 > 0 and y1 < 0):  #búsqueda de cambio de signo
            aumentador *= 10 ** -1                      #cambio en el tamaño del paso
            x1 = x0 + aumentador                        #actualización del rango
        else:
            x0 += aumentador                            #actualización del rango
            x1 += aumentador
        y0 = eval(x0)
        y1 = eval(x1)
        cont += 1                                       #conteo de iteraciones
    fin = timeit.default_timer()
    print("Raíz aproximada:", str(x1))
    print("f(raíz):", str(y1))
    print("Iteraciones:", str(cont))
    print("Tiempo:", fin-inicio, 'segundos')
    
Este algoritmo itera inicialmente con pasos de a una unidad desde el inicio del rango dado, evaluando la función en dos puntos consecutivos. Cuando se detecta un cambio de signo,  se cambia el paso a 0.1 y se itera entre estos dos puntos buscando nuevamente el cambio de signo. El algoritmo se repite, dividiendo en 10 el tamaño del paso cada vez que se identifique el cambio de signo, hasta que el valor evaluado caiga en el rango de tolerancia del error.

Para el cálculo de la complejidad se corrió el algoritmo varias veces aumentando cada vez el rango en el que se evalúa la función en un orden de 10^x. Se graficaron los tiempos que se demoró el algoritmo contra el tamaño del rango (n)  y dicha gráfica se comparó con otras gráficas conocidas (n, log n) para aproximar su comportamiento. Se concluyó que el algoritmo tiene una complejidad menor a log n hasta valores de n=6'000.000; a partir de este punto la gráfica del algoritmo supera la de log n y se acerca más a la de n. Por esto se concluye que en general  (y para valores de n más grandes) la complejidad del algoritmo es n.


ALGORITMO BASADO EN EL MÉTODO DE BISECCIÓN (PUNTO MEDIO)

def voraz():
    inicio = timeit.default_timer()
    error = 0.0001                                        #error de y
    x0 = -1000
    x1 = 1000
    y0 = eval(x0)
    y1 = eval(x1)
    xr = (x0+x1)/2                                        #primer punto medio
    yr = eval(xr)                                         #evaluación del primer punto medio
    cont = 0
    while abs(yr) > error:
        if (y0 < 0 and yr < 0) or (y0 > 0 and yr > 0):    #comprobación del cambio de signo
            x0 = xr                                       #actualización del rango
            y0 = yr
        else:
            x1 = xr                                       #actualización del rango
            y1 = yr
        xr = (x0 + x1) / 2                                #nuevo punto medio
        yr = eval(xr)
        cont += 1                                         #conteo iteraciones
    fin = timeit.default_timer()

    print("Raíz aproximada:", str(xr))
    print("f(raíz):", str(yr))
    print("Iteraciones:", str(cont))
    print("Tiempo:", fin - inicio, 'segundos')
    
voraz()
    
########## Complejidad = O(1)+O(n)*O(n)+O(1)+O(1)+O(1) = O(1)+O(n^2)+O(1)+O(1)+O(1) = O(n^2)



ALGORITMO VORAZ BASADO EN EL MÉTODO DE NEWTON RAPHSON

## Algoritmo voraz basado en el método de Newton Raphson para aproximar raíces del polinomio dado.

import time
errAbs = 0 # Contador de precisión que debe ser menor a +/-0.0001
contIteraciones = 0 # Contador de iteraciones.
numero = float(input('Digite cualquier número para comenzar a buscar raíces: '))

 # Función que recibe como parámetro principal el número digitado por el usuario para buscar la raíz.
def raiz (errAbs, contIteraciones, numero):

    tic = time.time()       # Inicia la medición de tiempo
    while True:
        # Función sin derivar evaluada en el punto. 
        fxi = pow(numero, 5)-59*pow(numero, 4)+35*pow(numero, 3)-250*pow(numero, 2)+numero - 70 
        # Función derivada evaluada en el punto.
        fxxi = 5*pow(numero, 4)-236*pow(numero, 3)+105*pow(numero, 2)-(500*numero) + 1  
        
        Xi = numero-(fxi/fxxi)      # Paso recursivo que halla la diferencia con base en un cálculo anterior.
        errAbs = abs((Xi - numero)/Xi*100) # Cálculo del error absoluto para compararlo con la resolución exigida de 10^-4.
        print('La precisión es:', errAbs)   # Imprime cómo se va reduciendo el error conforme se aproxima.
        contIteraciones += 1    
        
        if (errAbs > 0.0001):   # La ejecución sigue mientras el error supere 10^-4.
            numero = numero - (fxi/fxxi)    # Nuevo Xi basado en el cálculo anterior (recursivo).
        else:            # Si el error baja de 10^-4 la ejecución termina.
            print('La raíz aproximada es:', numero)
            print('Iteraciones:', contIteraciones)
            break
    toc = time.time()       # Finaliza la medición de tiempo
    timeTotal = toc-tic
    print( f"Tiempo: {timeTotal:0.4f} segundos.")

raiz (errAbs, contIteraciones, numero)

Complejidad = O(1)+O(n)*O(n)+O(1)+O(1)+O(1) = O(1)+O(n^2)+O(1)+O(1)+O(1) = O(n^2)



Desarrollado por:
- Santiago Rodríguez Camargo
- Fredy Alexander Gonzalez Pobre
- Víctor Manuel Torres
- Daniel Leonardo Sánchez
- Daniel Felipe Vargas Gómez

Se programó algoritmo de búsqueda por fuerza bruta y se hace el análisis de complejidad correspondiente.
Fecha: 19-04-2022
