# DEBER3
##Cargar y corregir datos

Carga datos de imágenes de moda, los procesa para el entrenamiento y las pruebas de un modelo de aprendizaje automático, y los prepara en un formato adecuado para ser utilizado por el modelo, normalizando los valores de píxeles y remodelando las matrices de píxeles.

#Construccion del modelo

Convolucional: Esta capa convolucional tiene 32 filtros de tamaño 3x3. Utiliza la función de activación ReLU (Rectified Linear Unit). La capa espera una entrada de imágenes en formato (28, 28, 1), que es el tamaño de las imágenes de entrada para este modelo.
Capa MaxPooling2D (Agrupación Máxima): Después de cada capa de convolución, se utiliza una capa de agrupación máxima para reducir el tamaño espacial de la representación, lo que ayuda a reducir el número de parámetros y la computación en la red, y también a hacer que el modelo sea más robusto.
Capa Conv2D (Convolucional): Esta capa convolucional tiene 64 filtros de tamaño 3x3, nuevamente con la función de activación ReLU.
Otra Capa MaxPooling2D (Agrupación Máxima): Otra capa de agrupación máxima para reducir el tamaño de la representación.
Otra Capa Conv2D (Convolucional): Otra capa convolucional con 64 filtros de tamaño 3x3 y función de activación ReLU.
Capa Flatten (Aplanamiento): Esta capa transforma los datos de salida de las capas convolucionales en un vector unidimensional antes de pasarlos a las capas densamente conectadas.
Capa Dense (Totalmente Conectada): Capa densa con 64 unidades y función de activación ReLU.
Capa Dense (Totalmente Conectada): Capa de salida con 10 unidades (una para cada clase), sin función de activación específica (especificada más adelante en el modelo.compile). Esta capa es la capa de salida cruda, antes de aplicar la activación softmax.

#Entrenamiento del modelo

En resumen, este código define, compila y entrena un modelo de CNN para clasificar imágenes de moda en 10 clases diferentes.

#Realizar Predicciones y Evaluar con las Matrices de Confusión

Utiliza el modelo entrenado (model) para predecir las etiquetas de clase para las imágenes de prueba (test_images) utilizando el método predict. Esto devuelve las probabilidades de pertenencia a cada clase para cada imagen.
Convierte estas probabilidades en etiquetas de clase predichas (y_test_labels_pred) utilizando np.argmax, que selecciona el índice con el valor más alto en cada fila (es decir, la clase con la mayor probabilidad).
Calcula la matriz de confusión entre las etiquetas reales de las imágenes de prueba (test_labels) y las etiquetas predichas (y_test_labels_pred) utilizando la función confusion_matrix de scikit-learn.
Visualiza la matriz de confusión utilizando matplotlib y seaborn, mostrando los valores reales en el eje y y las predicciones en el eje x. Los valores en la matriz muestran la frecuencia con la que se predicen las diferentes clases en comparación con las clases reales.

![image](https://github.com/Danielsp1/DEBER3/assets/157714894/7be6d698-f9c3-4244-9942-4ca2e8001082)

#Descripcion de matriz de confusión

Diagonal Principal: Los números en la diagonal principal (de arriba a la izquierda a abajo a la derecha) representan el número de predicciones correctas para cada clase. Por ejemplo, el modelo predijo correctamente la clase 0 (que podría ser, por ejemplo, camisetas) 893 veces.
Fuera de la Diagonal Principal: Cualquier número fuera de la diagonal principal indica el número de veces que una clase fue mal clasificada como otra. Por ejemplo, los elementos que son realmente de la clase 0 fueron incorrectamente clasificados como clase 2, 25 veces.
Clases bien clasificadas: Puedes ver que para algunas clases, como la clase 1 y la clase 7, el modelo tiene un alto número de predicciones correctas (980 y 953 respectivamente), lo que sugiere que el modelo es muy bueno al clasificar estas categorías.
Clases confundidas: Para otras, como la clase 4 y la clase 6, hay una cantidad significativa de confusiones, como se puede ver en los valores fuera de la diagonal principal. Por ejemplo, la clase 6 fue confundida con la clase 0, 119 veces, y la clase 4 fue confundida con la clase 2, 105 veces. Esto puede sugerir que estas clases son más difíciles de diferenciar para el modelo, o que hay características visuales similares que están llevando al modelo a confundirse.
Potencial para Mejora: Las clases que tienen un alto número de falsos positivos o falsos negativos son áreas donde el modelo podría mejorar. Por ejemplo, la clase 6 parece tener más dificultades que las otras, así que podrías investigar más a fondo qué está causando la confusión.
Balance de Clases: La matriz también puede mostrarte si hay un desequilibrio en el número de muestras para cada clase. En este caso, todas las clases parecen tener una cantidad similar de muestras reales, lo cual es bueno para el rendimiento general del modelo.
Exactitud General: Si sumas todos los valores de la diagonal principal y los divides por el total de predicciones, obtendrás la exactitud general del modelo. En este caso, parece ser relativamente alta, lo que indica un buen rendimiento general.
