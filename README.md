# LuxAI 


**if you want to read this same document but in [Spanish](https://github.com/yeriel/LuxAI/blob/main/Spanish.md)**

## Introduction

The night is dark and full of terrors. Two teams must fight off the darkness, collect resources, and advance through the ages. Daytime finds a desperate rush to gather the resources that can carry you through the impending night whilst growing your city. Plan and expand carefully -- any city that fails to produce enough light will be consumed by darkness.

The Lux AI Challenge is a competition where competitors design agents to tackle a multi-variable optimization, resource gathering, and allocation problem in a 1v1 scenario against other competitors.

![](https://github.com/Lux-AI-Challenge/Lux-Design-2021/raw/master/assets/daynightshift.gif)

## Getting Started

You will need Node.js version 12 or above. See installation instructions [here](https://nodejs.org/en/download/), you can just download the recommended version.

Open up the command line, and install the competition design with

```
npm install -g @lux-ai/2021-challenge@latest
```

You may ignore any warnings that show up, those are harmless. To run a match from the command line (CLI), simply run

```
npx lux-ai-2021 path/to/botfile path/to/otherbotfile
```

and the match will run with some logging and store error logs and a replay in a new errorlogs folder and replays folder. Logs stored in the errorlogs will include all error output and anything printed to standard error by your agent. You can watch the replay stored in the replays folder using the [visualizer](https://2021vis.lux-ai.org/). 

## Goal
To have the most CityTiles at the end of the game, which is determined by the win conditions. 

### Win Conditions

After 360 turns the winner is whichever team has the most CityTiles on the map. If that is a tie, then whichever team has the most units owned on the board wins. If still a tie, the game is marked as a tie.

A game may end early if a team no longer has any more Units or CityTiles. Then the other team wins.

To know the environment conditions and restrictions you saw this [link](https://www.lux-ai.org/specs-2021), along with API documentation see this [document](https://github.com/Lux-AI-Challenge/Lux-Design-2021/tree/master/kits)

##  Agents 
The repository has 5 types of agents, these are:

- **dummyAgent :** This agent does not perform any action during the whole game, it is the simplest agent that can be performed.

- **baseAgent :** This agent's strategy is to move to the adjacent tile to exploit a resource if it exists, otherwise it returns to its original tile. 

- **randomAgent :** This agent can perform all the actions that are described in the documentation of the competition (see here) only that the decision making is done randomly during the game. This allows the agent to explore rather than exploit, being one of the worst strategies to achieve the objective, not counting the dummyAgent. 

- **simulatingAnnealingAgent :** This agent uses simulating Annealing for decision making from a random approach to a more informed decision making based on manhattan distance. This agent presents an exploration behavior at the beginning of the game and as the turns progress it starts to focus its behavior on the map converging to a single point.

- **greedyAgent :** This agent makes decisions using as a heuristic the manhattan distance between the position of the units and the resources, it also has a strategy of construction of cities based on looking for the best loza so that this is self-supporting during the game. This agent from the beginning of the game presents a more localized behavior given its starting point but still explores enough to obtain resources.

## Algorithm explanation

### Greedy
A greedy algorithm is any algorithm that follows the problem-solving heuristic of making the locally optimal choice at each stage. In many problems, a greedy strategy does not produce an optimal solution, but a greedy heuristic can yield locally optimal solutions that approximate a globally optimal solution in a reasonable amount of time. [more theory](https://en.wikipedia.org/wiki/Greedy_algorithm)

### Simulating Annealing

Simulating Annealing is a probabilistic technique for approximating the global optimum of a given function. Specifically, it is a metaheuristic to approximate global optimization in a large search space for an optimization problem. It is often used when the search space is discrete. [more theory](https://en.wikipedia.org/wiki/Simulated_annealing)

**Pseudocode**

```
    Let s = s0
    For k = 0 through kmax (exclusive):
        T ← temperature( 1 - (k+1)/kmax )
        Pick a random neighbour, snew ← neighbour(s)
        If P(E(s), E(snew), T) ≥ random(0, 1):
            s ← snew
    Output: the final state s

```