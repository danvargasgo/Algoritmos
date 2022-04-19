Laboratorio 3

ANÁLISIS DE COMPLEJIDAD

def buscaGen(secuencia1, gen4):
    tic = time.time()                          #O(1)
    for i in range(len(secuencia1)-len(gen4)): #O(n)
        if(secuencia1[i:i+len(gen4)] == gen4): #O(n)
            print('Índice inicial:',str(i), ', índice final:', str(i+len(gen4))) #O(1)
    toc = time.time()                          #O(1)
    timeTotal = toc-tic                        #O(1)
    print( f"Tiempo: {timeTotal:0.4f} segundos.") #O(1)
    
Complejidad = O(1)+O(n)*O(n)+O(1)+O(1)+O(1) = O(1)+O(n^2)+O(1)+O(1)+O(1) = O(n^2)


Desarrollado por:
- Santiago Rodríguez Camargo
- Fredy Alexander Gonzalez Pobre
- Víctor Manuel Torres
- Daniel Leonardo Sánchez
- Daniel Felipe Vargas Gómez

Se programó algoritmo de búsqueda por fuerza bruta y se hace el análisis de complejidad correspondiente.
Fecha: 19-04-2022
