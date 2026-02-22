# Deep Reinforcement Learning – Assault (DQN)

## Descripción del Proyecto

Este proyecto implementa un agente de **Aprendizaje por Refuerzo Profundo (Deep RL)** para el entorno **ALE/Assault-v5** utilizando **Deep Q-Network (DQN)** con Stable-Baselines3.

---

## ¿Qué es Assault?

**Assault** es un videojuego clásico de Atari en el que el jugador controla una nave que debe defender su posición frente a oleadas de enemigos que disparan proyectiles desde la parte superior de la pantalla. El objetivo es eliminar enemigos y sobrevivir el mayor tiempo posible acumulando puntos.

Desde la perspectiva de aprendizaje por refuerzo, Assault presenta varios desafíos técnicos:

- Observaciones visuales de alta dimensionalidad (frames RGB del juego).
- Espacio de acción discreto.
- Recompensas frecuentes pero dependientes de precisión en disparo.
- Entorno dinámico con múltiples enemigos simultáneos.
- Necesidad de coordinación entre movimiento lateral y disparo.

Estas características lo convierten en un entorno adecuado para evaluar la capacidad de aprendizaje visual y la estabilidad del algoritmo DQN.

---

## Objetivo del Proyecto

Entrenar un agente capaz de aprender una política superior al comportamiento aleatorio a partir de observaciones visuales crudas (frames del juego), empleando:

- Redes neuronales convolucionales (CnnPolicy)
- Experience Replay
- Target Network
- Frame Stacking (4 frames)

---

## Algoritmo Implementado

### Deep Q-Network (DQN)

DQN combina redes neuronales profundas con Q-Learning para aproximar la función de valor Q(s,a). Utiliza:

- **Experience Replay** para romper correlaciones temporales.
- **Target Network** para estabilizar las actualizaciones.
- Aprendizaje por lotes desde un replay buffer.

Este enfoque permite estimar valores Q a partir de imágenes y tomar decisiones en espacios de acción discretos.

---

## Configuración del Entrenamiento

- Total timesteps: **500,000**
- Replay buffer: **100,000**
- Learning starts: **10,000**
- Batch size: **32**
- Gamma (discount factor): **0.99**
- Exploración (ε decay ≈ 20%)
- Frame stacking: **4 frames**
- Dispositivo: **GPU (CUDA)**

---

## Resultados

El agente DQN logró:

- Recompensa promedio: **2,773.20 puntos**
- Desviación estándar: **647.61**
- Política aleatoria: **235.20 puntos**

Esto representa una mejora sustancial frente al comportamiento aleatorio, confirmando que el agente logró aprender una política efectiva dentro del entorno.

La evolución de recompensas puede visualizarse mediante los logs de TensorBoard incluidos en este repositorio.

---

## Contenido de la Carpeta

```
Assault/
│
├── dqn_assault.zip
├── videos.mp4 (Rederización del comportamiento en entrenamiento y final)
├── logs/
└── Problema_dificultad_media_Assault.ipynb
```

### Carpeta logs/

Incluye:

- Archivos de eventos de TensorBoard
- Checkpoints intermedios
- Métricas de entrenamiento

---

### Comparación Experimental

El modelo DQN demostró una mejora clara frente a la política aleatoria. Sin embargo, en comparación con variantes como DDQN (implementada en BattleZone), puede presentar mayor volatilidad en la estimación de valores Q debido al sesgo de sobreestimación característico del método original.

---

### Hardware Utilizado

- Google Colab
- GPU NVIDIA (CUDA)
- Stable-Baselines3 v2.x
