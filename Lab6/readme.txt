SOLUCIÓN LABORATORIO 6
Grupo 4

- Santiago Rodríguez Camargo
- Fredy Alexander Gonzalez Pobre
- Daniel Leonardo Sánchez
- Daniel Felipe Vargas Gómez

Se realizó la adaptación para implementación del perceptron simple eligiendo algunos datasets. Sobre el análisis, ubicado en seguida citamos:

ANÁLISIS
Dentro de las características que se pueden observar en la representación gráfica del data set utilizado, podemos ver como los diagnósticos de tumores malignos se encuentran agrupados en mayor medida en la parte superior derecha del gráfico, mientras que los diagnósticos de tumores benignos, se encuentran agrupados en la parte inferior izquierda, Esto ayuda en gran medida al perceptrón, ya que, si bien no existe una separabilidad lineal en los datos, existe una tendencia lo suficientemente marcada en los mismos para que el perceptrón pueda acertar, al menos, la mitad de las veces a la hora de realizar una clasificación tomando en cuenta los datos de perímetro y textura de los tumores presentes en el cáncer de mama, esta característica por el mismo motivo nos muestra, por qué el error es tan alto, ya que, al haber partes de los datos que se encuentran dentro de las características que deberían representar al diagnóstico opuesto, para el perceptrón es imposible acertar con un nivel de error bajo.

COMPLEJIDAD
La complejidad de este algoritmo depende principalmente de la cantidad de parámetros que usaremos y sus iteraciones.  Sea n el número de parámetros e i el número de iteraciones.  Para calcular delta_w es necesario realizar tantas multiplicaciones comp parámetros se tengan; el nuevo w requiere esta misma cantidad de multiplicaciones (como es estándar, no se cuentan las sumas).  Esta operación se repite tantas veces como datos haya en el set de entrenamiento y a este número lo llamaremos m. Por último, todo esto se repite tantas veces como iteraciones se tengan, esto es O(imn). Si asumimos i = n = n, se tiene O(n^3).

SEPARABILIDAD DE DATOS
Cuando se usan todas las variables, resulta complejo definir la separabilidad de los datos. Sin embargo, por el índice que se obtuvo al evaluar las predicciones del perceptrón, se infiere que los datos son separables.


CÁLCULO BÁSICO DE COMPLEJIDAD

class Perceptron:
    def __init__(self, eta=0.1, n_iter=10):      
        self.eta = float(eta)                                                          o(1)
        self.n_iter = n_iter                                                           O(1)

    def train(self, X, y):
        # inicializar los pesos en 0
        self.w = np.zeros(len(X[1])+1)                                                 O(1)
        #vector de errores acumulados
        self.errors = []                                                               O(1)

        #ciclo de entrenamiento
        for i in range(self.n_iter):                                                   O(n^2)
            errors = 0
            for x_i, target in zip(X,y):                                               O(n)
                #calcular el nuevo valor de los pesos
                delta_w = np.array((target - self.predict(x_i)) * self.eta)            o(1)
                #actualizar el valor de los pesos
                self.w[1:] += delta_w * x_i                                            o(1)
                #actualizar el valor del bias
                self.w[0] += delta_w                                                   o(1) 
                if (delta_w!=0):                                                       o(1)
                    errors += 1                                                        o(1)
            self.errors.append(errors)                                                 o(1)
 

    def predict(self, X):
        #combinacion lineal, w[0] = bias
        v = np.dot( X, self.w [1:]) + self.w[0]                                        o(1)
        #funcion de activación 
        if v > 0.0:
            return 1                                                                   o(1)
        return -1                                                                      o(1)

Calculo
o(1)+o(1)+o(1)+o(1)+o(n)*o(n)*o(n)+o(1)+o(1)+o(1)=o(n^3)


Fecha: 15-06-2022
