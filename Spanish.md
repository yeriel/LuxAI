# LuxAI

## Introducción

La noche es oscura y está llena de terrores. Dos equipos deben luchar contra la oscuridad, recoger recursos y avanzar a través de los días. El día se convierte en una carrera desesperada para reunir los recursos que te permitan atravesar la inminente noche mientras haces crecer tu ciudad. Planifica y expande con cuidado: cualquier ciudad que no produzca suficiente luz será consumida por la oscuridad.

El Desafío Lux AI es una competición en la que los competidores diseñan agentes para abordar un problema de optimización, recolección de recursos y asignación de múltiples variables en un escenario 1v1 contra otros competidores.

![](https://github.com/Lux-AI-Challenge/Lux-Design-2021/raw/master/assets/daynightshift.gif)

## Para empezar

Necesitarás Node.js versión 12 o superior. Consulta las instrucciones de instalación [aquí](https://nodejs.org/en/download/), puedes simplemente descargar la versión recomendada.

Abre la línea de comandos, e instala el diseño de la competición con

```
npm install -g @lux-ai/2021-challenge@latest
```

Puedes ignorar las advertencias que aparezcan, son inofensivas. Para ejecutar una partida desde la línea de comandos (CLI), simplemente ejecute

```
npx lux-ai-2021 ruta/del/botA ruta/del/botB
```

La partida se ejecutará  y almacenará los registros de errores y una repetición en una nueva carpeta de registros de errores y una carpeta de repeticiones. Los registros almacenados en los errores incluirán toda la salida de errores y cualquier cosa impresa en el error estándar por su agente. Puede ver la repetición almacenada en la carpeta de repeticiones utilizando el [visualizador](https://2021vis.lux-ai.org/). 

## Objetivo
Tener la mayor cantidad de CityTiles al final del juego, lo cual está determinado por las condiciones de victoria. 

### Condiciones de victoria

Después de 360 turnos, el ganador será el equipo que tenga más CityTiles en el mapa. Si hay un empate, gana el equipo que tenga más unidades en el tablero. Si sigue habiendo un empate, la partida se marca como un empate.

Una partida puede terminar antes de tiempo si un equipo ya no tiene más unidades o CityTiles. Entonces el otro equipo gana.

Para conocer las condiciones del entorno y las restricciones viste este [enlace](https://www.lux-ai.org/specs-2021), junto con la documentación de la API vea este [documento](https://github.com/Lux-AI-Challenge/Lux-Design-2021/tree/master/kits)

## Agentes 
El repositorio tiene 5 tipos de agentes, estos son

- **AgenteDummy :** Este agente no realiza ninguna acción durante todo el juego, es el agente más simple que se puede realizar.

- **AgenteBase :** La estrategia de este agente es moverse a la casilla adyacente para explotar un recurso si existe, de lo contrario vuelve a su casilla original. 

- **AgenteRandom :** Este agente puede realizar todas las acciones que se describen en la documentación de la competición sólo que la toma de decisiones se realiza de forma aleatoria durante la partida. Esto permite al agente explorar en lugar de explotar, siendo una de las peores estrategias para conseguir el objetivo, sin contar el dummyAgent. 

- **simulatingAnnealingAgent :** Este agente utiliza simulación de recocido para la toma de decisiones desde un enfoque aleatorio hasta una toma de decisiones más informada basada en la distancia manhattan. Este agente presenta un comportamiento de exploración al principio del juego y a medida que avanzan los turnos comienza a centrar su comportamiento en el mapa convergiendo a un único punto.

- **AgenteGreedy :** Este agente toma decisiones usando como heurística la distancia manhattan entre la posición de las unidades y los recursos, además tiene una estrategia de construcción de ciudades basada en buscar la mejor loza para que esta se auto sostenga durante el juego. Este agente desde el principio del juego presenta un comportamiento más localizado dado su punto de partida pero sigue explorando lo suficiente para obtener recursos.

## Explicación del algoritmo

### Greedy
Un algoritmo codicioso es cualquier algoritmo que sigue la heurística de resolución de problemas de hacer la elección localmente óptima en cada etapa. En muchos problemas, una estrategia codiciosa no produce una solución óptima, pero una heurística codiciosa puede producir soluciones localmente óptimas que se aproximan a una solución globalmente óptima en un tiempo razonable. [más teoría](https://en.wikipedia.org/wiki/Greedy_algorithm)

### Simulating Annealing

El recocido de simulación es una técnica probabilística para aproximar el óptimo global de una función dada. Específicamente, es una metaheurística para aproximar el óptimo global en un gran espacio de búsqueda para un problema de optimización. Se suele utilizar cuando el espacio de búsqueda es discreto. [más teoría](https://en.wikipedia.org/wiki/Simulated_annealing)

**Pseudocódigo**

```
    Sea s = s0
    Para k = 0 hasta kmax (exclusivo):
        T ← temperatura( 1 - (k+1)/kmax )
        Escoge un vecino al azar, snew ← vecino(s)
        Si P(E(s), E(snew), T) ≥ random(0, 1):
            s ← snew
    Salida: el estado final s

```