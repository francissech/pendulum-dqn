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
Completar con los resultados reales del notebook:
- Número de pasos de entrenamiento:
- Retorno medio de DQN:
- Retorno medio de la política aleatoria:
- Retorno medio con torque cero:

## Reflexión sobre los resultados
Completar indicando si DQN mejoró frente a las políticas
de referencia y qué limitaciones se observaron.

## Principales dificultades
Completar describiendo las dificultades realmente encontradas
y cómo se resolvieron.

## Referencias
- https://gymnasium.farama.org/environments/classic_control/pendulum/
- https://stable-baselines3.readthedocs.io/en/master/modules/dqn.html
