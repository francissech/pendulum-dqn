# Control de Pendulum-v1 mediante DQN

Autor: Francis Segovia Chaves

## Objetivo
Entrenar y evaluar un agente Deep Q-Network (DQN) para
levantar un péndulo y mantenerlo en posición vertical.

## Entorno
Se utiliza Pendulum-v1 de Gymnasium.

La observación contiene tres valores:
- Coseno del ángulo del péndulo.
- Seno del ángulo del péndulo.
- Velocidad angular.

El entorno original permite aplicar un torque continuo
entre -2 y 2. Para utilizar DQN, se discretizó el torque
en nueve valores:
-2, -1.5, -1, -0.5, 0, 0.5, 1, 1.5 y 2.

## Recompensa
La recompensa penaliza la desviación respecto a la posición
vertical, la velocidad angular y el torque aplicado.
Un retorno menos negativo representa un mejor desempeño.

## Duración del episodio
Cada episodio se trunca a los 200 pasos.
Alcanzar la posición vertical no finaliza el episodio.

## Red neuronal
La red recibe las tres variables de observación.
Tiene dos capas ocultas de 128 neuronas con activación ReLU
y nueve salidas, una por acción.

Cada salida estima el retorno esperado de seleccionar
esa acción.

## Flujo de entrenamiento
1. Obtener la observación del entorno.
2. Seleccionar una acción mediante exploración epsilon-greedy.
3. Convertir la acción en un torque.
4. Aplicar el torque y obtener la recompensa.
5. Guardar la transición en la memoria de repetición.
6. Actualizar la red con lotes de experiencias.
7. Actualizar periódicamente la red objetivo.
8. Evaluar y guardar el modelo.

## Archivos
- Pendulum_DQN.ipynb: código y explicaciones.
- requirements.txt: dependencias utilizadas.
- results/: gráficas y evaluaciones.
- models/: modelos entrenados.

## Cómo ejecutar
1. Descargar el repositorio y descomprimirlo.
2. Instalar las dependencias de requirements.txt.
3. Abrir Pendulum_DQN.ipynb en Jupyter.
4. Ejecutar las celdas en orden.

## Resultados
## Resultados del entrenamiento

Se entrenó un agente DQN en Pendulum-v1 durante 200 000 pasos
de interacción. Para adaptar el entorno al algoritmo, se
discretizó el torque en nueve acciones entre -2 y 2.
La red neuronal utilizó tres entradas y dos capas ocultas
de 128 neuronas, con una salida por acción.

La curva de evaluación muestra una mejora importante.
Al inicio, el retorno medio fue aproximadamente -1450.
Durante los primeros 25 000 pasos aumentó hasta valores
cercanos a -180. Sin embargo, alrededor de los 30 000 pasos
se observó una caída temporal hasta aproximadamente -530,
lo que evidencia fluctuaciones durante el aprendizaje.

A partir de unos 45 000 pasos, el retorno medio se mantuvo
principalmente entre -100 y -200. Al finalizar el
entrenamiento, alcanzó aproximadamente -160.
Estos valores se estimaron visualmente de la gráfica.

## Reflexión sobre los resultados

El aumento del retorno hacia valores menos negativos indica
que el agente aprendió una política que reduce la penalización
asociada con la desviación angular, la velocidad y el torque.
El mayor avance ocurrió durante la primera etapa del
entrenamiento; posteriormente, el desempeño se estabilizó
con mejoras adicionales limitadas.

La banda de variación se estrecha después de las primeras
etapas, lo que sugiere mayor consistencia entre los episodios
evaluados. Esta banda representa variabilidad entre episodios,
no entre entrenamientos independientes.

La curva, por sí sola, no demuestra que el péndulo permanezca
vertical durante todo el episodio. Para comprobarlo se requiere
observar su comportamiento o analizar la evolución del ángulo
y la velocidad angular. También se necesita la comparación
final con torque cero y acciones aleatorias para cuantificar
la ventaja del agente entrenado.

## Retos del proceso y limitaciones

Una particularidad central fue adaptar un espacio de acciones
continuo a DQN mediante la discretización del torque.
Esta decisión permite aplicar el algoritmo, pero limita
la precisión del control a los valores disponibles.

Otra dificultad del aprendizaje fue la variabilidad inicial:
la mejora no fue monótona y se presentó una caída temporal
del retorno. Por ello, se realizaron evaluaciones periódicas
y se guardó el mejor modelo observado durante el entrenamiento.

Como continuación del estudio, se propone comparar diferentes
cantidades de acciones discretas y repetir el entrenamiento
con varias semillas. Esto permitirá evaluar si el desempeño
observado es reproducible y si una discretización más fina
mejora el control.

## Referencias
- https://gymnasium.farama.org/environments/classic_control/pendulum/

